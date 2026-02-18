# Navegação no SUAP IFPR

Mapa global de navegação do SUAP IFPR e guia de boas práticas para automação via browser.

## URLs Base

| Finalidade | URL |
|---|---|
| Página inicial | `https://suap.ifpr.edu.br` |
| Login | `https://suap.ifpr.edu.br/accounts/login/` |

## Login

Para autenticar no SUAP, acessar a URL de login e preencher os campos:

| Campo | Seletor | Descrição |
|---|---|---|
| Usuário | `#id_username` | Matrícula ou CPF do servidor |
| Senha | `#id_password` | Senha do SUAP |

Após preencher, submeter o formulário. O login é bem-sucedido quando a URL muda para a página inicial (`/`) e o menu lateral do SUAP aparece na tela.

## Boas Práticas

### Estratégia Geral

Preferir **sempre** navegação via URL direta ao invés de clicar em elementos via seletores CSS. O SUAP é uma aplicação Django com muitos elementos JS/AJAX que dificultam a interação por seletores.

### Abas

A maioria das abas do SUAP **não** funciona via parâmetro `?tab=` na URL. Elas usam JavaScript para carregar conteúdo dinamicamente. Nos fluxos de automação, sempre verificar se a aba desejada suporta acesso via URL.

#### Abas que funcionam via URL (`?tab=`)

| Contexto | Abas disponíveis |
|---|---|
| Servidor (`/rh/servidor/{matricula}/`) | `ferias`, `contracheques`, `ocorrencias_afastamentos`, `historico_funcional` |
| Projeto de Ensino (`/projetos_ensino/projeto/{id}/`) | `equipe`, `conclusao` |

#### Abas que NÃO funcionam via URL

| Contexto | Abas (requerem interação JavaScript) |
|---|---|
| Projeto de Ensino | `dados_do_edital`, `metas_atividades`, `plano_de_desembolso`, `plano_de_aplicacao`, `caracterizacao_dos_beneficiarios`, `anexos`, `fotos`, `registros_de_frequencia_atividade_diaria`, `pendencias` |

### Seletores CSS

#### Seletores que funcionam

| Seletor | Descrição |
|---|---|
| `a[class*='view']` | Ícones de visualização (olho verde) nas tabelas de listagem |
| `table, h1, h2` | Tags HTML simples para verificação de conteúdo |

#### Seletores problemáticos

| Seletor | Problema |
|---|---|
| `select[name='edital'], input[name='edital']` | Filtros autocomplete não são selects/inputs padrão do HTML |
| `a[href*='/projetos_ensino/projeto/']` | Primeiro match é link invisível no breadcrumb do menu lateral |
| `.action-links a:first-child` | Pega link de "Reportar erro" no rodapé, não ações da tabela |
| `table.dataTable, td.acoes, .tab-panel` | Classes CSS não existem no SUAP — não usa DataTables nem essas classes |

#### Dica sobre múltiplos matches

Quando um seletor retorna múltiplos matches, a ferramenta de automação pega o primeiro, que pode ser invisível (breadcrumb, menu colapsado). Usar seletores mais específicos ou navegar via URL quando possível.

## Padrões de URL

| Padrão | URL |
|---|---|
| Listagem admin | `/admin/<app>/<model>/` |
| Detalhe de entidade | `/<app>/<model>/{id}/` |
| Aba via URL | `/<app>/<model>/{id}/?tab=<nome_aba>` |
| Servidor | `/rh/servidor/{matricula}/` |
| Servidor (aba) | `/rh/servidor/{matricula}/?tab=<nome_aba>` |
| Editais abertos | `/projetos_ensino/editais_abertos/` |
| Adicionar projeto | `/projetos_ensino/adicionar_projeto/{edital_id}/` |

## Menus Principais

### Ensino

| Submenu | URL |
|---|---|
| Projetos | `/admin/projetos_ensino/projeto/` |
| Adicionar projeto (editais abertos) | `/projetos_ensino/editais_abertos/` |
| Diários | `/edu/diarios/` |
| Turmas | `/edu/turmas/` |

### Extensão

| Submenu | URL |
|---|---|
| Projetos de Extensão | `/extensao/projetos/` |
| Estágios | `/estagios/` |

### Pesquisa

| Submenu | URL |
|---|---|
| Projetos de Pesquisa | `/pesquisa/projetos/` |

### Gestão de Pessoas

| Submenu | URL |
|---|---|
| Férias | `/rh/ferias/` |
| Frequência | `/ponto/` |
| Contracheque | `/rh/contracheque/` |

### Administração

Sem submenus documentados.

### Documentos

Sem submenus documentados.

---

## Permissões e Diagnóstico de Acesso

O SUAP controla o acesso por **Grupos de Usuário**, organizados por módulo. Cada grupo concede permissões específicas dentro do módulo. Sem o grupo adequado, o usuário pode encontrar erros de acesso ou simplesmente não ver determinados menus/botões.

### Como verificar permissões

**URL:** `/comum/grupos_usuario/{id_do_usuario}/`

A página lista todos os grupos atribuídos ao usuário, organizados por módulo. Para encontrar o ID do usuário, acessar o perfil do servidor: o ID aparece na URL da página de grupos.

### Sinais de falta de permissão

| Sintoma | Causa provável |
|---|---|
| Página retorna erro 403 (Forbidden) | Usuário não possui o grupo necessário para acessar aquela funcionalidade |
| Menu ou submenu não aparece no painel lateral | Nenhum grupo do módulo correspondente está atribuído ao usuário |
| Botão de ação não aparece (ex: "Adicionar projeto") | Grupo atribuído é de nível inferior (ex: Visualizador quando precisa de Coordenador) |
| Mensagem "Você não tem permissão para realizar esta ação" | Ação requer grupo específico que o usuário não possui |
| Tabela de listagem aparece vazia mesmo havendo registros | Filtro de campus ou grupo restringe a visibilidade dos registros |

### Diagnóstico passo a passo

Quando uma ação falha por possível falta de permissão:

1. **Verificar os grupos do usuário** — acessar `/comum/grupos_usuario/{id_do_usuario}/` e identificar se o grupo necessário está na lista
2. **Comparar com a pré-condição do fluxo** — cada fluxo documenta a permissão necessária no campo "**Permissão:**" das pré-condições
3. **Se o grupo não estiver na lista** — orientar o usuário a solicitar a inclusão no grupo ao administrador do campus, geralmente via Central de Serviços do SUAP ou contato direto com a DIRGE/PROEN
4. **Se o grupo estiver na lista** — o problema pode ser outro (projeto de outro campus, edital encerrado, situação do projeto incompatível com a ação)

### Módulos e Grupos conhecidos

| Módulo | Grupos |
|---|---|
| Administração :: Protocolo | Tramitador de processos |
| Atividades Estudantis :: Saúde | Psicólogo |
| Comum :: Central de Serviços | Atendente da Central de Serviços |
| Documentos e Processos Eletrônicos :: Processos Eletrônicos | Operador de Processo Eletrônico, Tramitador de Processos Eletrônicos |
| Ensino :: ETEP | Interessado ETEP, etep Administrador, Membro ETEP |
| Ensino :: Ensino | Pedagogo |
| Ensino :: Projetos de Ensino | projetos_ensino Administrador, Avaliador de Projetos de Ensino, Monitor de Projetos de Ensino, Visualizador de Projetos de Ensino, Coordenador de Projetos de Ensino, Integrante da Comissão de Acompanhamento |
| Gestão de Pessoas :: Gestão de Pessoas | Servidor |

> **Nota:** Esta lista reflete os grupos de um usuário específico. Outros módulos e grupos podem existir no SUAP. Atualize esta tabela conforme novos módulos forem documentados.
