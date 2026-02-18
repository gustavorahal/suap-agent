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
