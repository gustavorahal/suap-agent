# Projetos de Ensino

Submissão e gestão de projetos de ensino no SUAP. Programas disponíveis: PBIS, PROCORP, PIPE, PAPE, entre outros. Acesso via menu Ensino > Projetos > Projetos.

- **Módulo:** ensino
- **URL base:** `/admin/projetos_ensino/projeto/`
- **Perfis:** servidor, docente

---

## Listagem de Projetos

**URL:** `/admin/projetos_ensino/projeto/`
**Título da página:** "Projetos"
**Exportar:** sim

### Filtros

| Nome | Tipo |
|---|---|
| Texto | texto_livre |
| Ano | seleção |
| Edital | autocomplete |
| Campus | autocomplete |

### Abas de Status

| Aba |
|---|
| Todos |
| Em Edição |
| Enviados |
| Pré-Selecionados |
| Selecionados |
| Em Execução |
| Concluídos |
| Não Enviados |
| Não Pré-Selecionados |
| Não Selecionados |
| Inativos |
| Cancelados |

### Colunas da Tabela

| Coluna |
|---|
| Ações |
| Campus |
| Edital |
| Coordenador |
| Título de Projeto |
| Situação Atual |
| Pré-selecionado |
| Selecionado |

### Ações por Projeto

- **Visualizar:** seletor `a[class*='view']` — ícone de olho verde para abrir detalhe do projeto

---

## Detalhe do Projeto

**URL:** `/projetos_ensino/projeto/{id}/`
**Título da página:** "Projeto de Ensino: {titulo}"

### Cabeçalho

Campos exibidos no cabeçalho:

- Título do Projeto
- Período do Edital
- Campus do Projeto
- Setor
- Carga Horária do Projeto
- Monitor do Projeto
- Badge de situação (exibido)

### Abas

> **Via URL:** abas marcadas com `via_url: true` podem ser acessadas diretamente via parâmetro `?tab=`. Abas com `via_url: false` requerem clique via JavaScript na página.

| # | Nome | Parâmetro `?tab=` | Via URL | Descrição |
|---|---|---|---|---|
| 1 | Dados do Projeto | *(aba padrão)* | sim | Início/Término da Execução, Área Temática, Interdisciplinar, Parceiros externos, status Pré-seleção/Seleção, Pontuação, Data de Divulgação |
| 2 | Dados do Edital | `dados_do_edital` | não | Informações do edital vinculado ao projeto |
| 3 | Caracterização dos Beneficiários | `caracterizacao_dos_beneficiarios` | não | Público-alvo e quantidade de beneficiários |
| 4 | Equipe | `equipe` | sim | Membros do projeto (docentes e discentes) |
| 5 | Metas/Atividades | `metas_atividades` | não | Metas e atividades do projeto com cronograma |
| 6 | Plano de Aplicação | `plano_de_aplicacao` | não | Memória de cálculo (valor bolsa x quantidade) |
| 7 | Plano de Desembolso | `plano_de_desembolso` | não | Pagamentos mensais programados |
| 8 | Anexos | `anexos` | não | Arquivos anexados ao projeto |
| 9 | Fotos | `fotos` | não | Fotos relacionadas ao projeto |
| 10 | Registros de Frequência/Atividade Diária | `registros_de_frequencia_atividade_diaria` | não | Registros de presença e atividades |
| 11 | Pendências | `pendencias` | não | Pendências a resolver antes do envio/conclusão |
| 12 | Conclusão | `conclusao` | sim | Relatório final do projeto |

### Aba: Dados do Projeto

Seção **Discriminação do Projeto** — campos de texto longo:

- Justificativa
- Objetivo Geral
- Objetivos Específicos
- Metodologia
- Metodologia do Projeto (Estrutura, Recursos Humanos, Plano de Trabalho)
- Acompanhamento e avaliação das atividades
- Disseminação de Resultados
- Referências

### Aba: Equipe

| Coluna | Descrição |
|---|---|
| Ações | Botões de ação |
| Membro | Nome, matrícula, Termo de Compromisso |
| Situação | Ativo/Inativo |
| Categoria/Titulação | DOCENTE, DISCENTE |
| Bolsista | Sim/Não |
| Coordenador | Sim/Não |

### Aba: Conclusão

Campos:

- Resultados Alcançados (texto longo)
- Disseminação de resultados (texto longo)
- Observação
- Avaliação (avaliador, data, parecer)

---

## Editais Abertos

**URL:** `/projetos_ensino/editais_abertos/`
**Título da página:** "Editais de Ensino e de Fluxo Contínuo com Inscrições Abertas"
**Acesso via menu:** Ensino > Projetos > Adicionar projeto

Lista todos os editais de ensino com inscrições abertas. Cada edital mostra título, descrição, anexos, período de inscrições, campus e botões de ação.

### Campos por Edital

| Campo |
|---|
| titulo_edital |
| descricao |
| anexos (links para documentos do edital) |
| periodo_inscricoes (data início e fim) |
| campus |

### Ações por Edital

| Botão | Seletor | URL destino | Descrição |
|---|---|---|---|
| Adicionar projeto | `a.btn-success[href*='adicionar_projeto']` | `/projetos_ensino/adicionar_projeto/{edital_id}/` | Abre o formulário de submissão de projeto para o edital |
| Ver arquivo | `a.btn-default[href*='ver_arquivo'], a[href*='ver_arquivo']` | *(abre PDF)* | Abre o PDF/arquivo do edital |

---

## Formulário: Adicionar Projeto

**URL:** `/projetos_ensino/adicionar_projeto/{edital_id}/`
**Título da página:** "Adicionar projeto"

Formulário para submissão de novo projeto de ensino vinculado a um edital. Campos de texto longo usam editor rich text (CKEditor). Após salvar, o projeto é criado em situação "Em Edição" e o usuário deve preencher abas adicionais (equipe, metas, plano, etc.).

### Seção 1: Dados Gerais

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| edital | Edital | *(somente leitura)* | somente_leitura | — | Nome do edital (preenchido automaticamente) |
| campus | Campus | `#id_campus` | seleção | sim | Campus onde o projeto será executado |
| titulo | Título do projeto | `#id_titulo` | texto | sim | Título completo do projeto de ensino |
| acao | Ação | `#id_acao` | texto | sim | Ação administrativa vinculada ao projeto |
| carga_horaria_coordenador | Carga Horária Semanal do Coordenador | `#id_carga_horaria` | numero | sim | Horas semanais dedicadas pelo coordenador |

### Seção 2: Dados do Projeto

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| inicio_execucao | Início da Execução | `#id_inicio_execucao` | data (dd/mm/aaaa) | sim | Data de início da execução do projeto |
| termino_execucao | Término da Execução | `#id_fim_execucao` | data (dd/mm/aaaa) | sim | Data de término da execução |
| carga_horaria_total | Carga horária total para desenvolvimento do projeto | `#id_carga_horaria_total` | numero | sim | Total de horas para desenvolvimento do projeto |
| eixo_tematico | Eixo Temático | `#id_eixo` | multiseleção | sim | Eixos temáticos do projeto (múltipla escolha) |
| projeto_interdisciplinar | Projeto Interdisciplinar? | `#id_interdisciplinar` | checkbox | não | Indica se o projeto envolve mais de uma disciplina |
| disciplina | Disciplina | `#id_disciplina` | multiseleção | não | Disciplinas envolvidas no projeto |
| curso | Curso | `#id_curso` | multiseleção | não | Cursos associados ao projeto |
| relacao_pos_graduacao | Possui relação institucional com Pós-graduação? | `#id_pos_graduacao` | checkbox | não | Indica vínculo com programa de pós-graduação |
| parceiro_externo | Há parceiro externo? | `#id_parceiro_externo` | checkbox | não | Indica se há parceiros externos envolvidos |

### Seção 3: Descrição do Projeto

> Todos os campos usam editor rich text (CKEditor).

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| resumo | Resumo | `#id_resumo` | rich_text | sim | — |
| introducao | Introdução | `#id_introducao` | rich_text | sim | Pode conter texto pré-preenchido do edital |
| justificativa | Justificativa e Relevância | `#id_justificativa` | rich_text | sim | — |
| objetivo_geral | Objetivo Geral | `#id_objetivo_geral` | rich_text | sim | — |
| metodologia | Metodologia da execução do projeto | `#id_metodologia` | rich_text | sim | — |
| acompanhamento | Acompanhamento e avaliação das atividades durante a execução | `#id_acompanhamento_avaliacao` | rich_text | sim | — |
| resultados_esperados | Resultados Esperados e Disseminação dos Resultados | `#id_resultados_esperados` | rich_text | sim | — |
| referencias | Referências | `#id_referencias` | rich_text | sim | — |

### Seção 4: Termo de Compromisso

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| aceite_termo | Aceite do Termo de Compromisso do(a) Coordenador(a) do Projeto de Ensino | `#id_aceite_termo` | checkbox | sim | Termo com obrigações do coordenador conforme o edital: não estar afastado, registrar no Plano Individual de Trabalho, cumprir carga horária compatível, etc. |

### Botão Salvar

- **Seletor:** `input[type='submit'][value='Salvar'], button.btn-success`
- **Efeito:** Salva o projeto em situação "Em Edição"

---

## Ciclo de Vida do Projeto

| # | Situação |
|---|---|
| 1 | Em Edição |
| 2 | Enviado |
| 3 | Aguardando pré-seleção |
| 4 | Pré-selecionado |
| 5 | Não pré-selecionado |
| 6 | Habilitado |
| 7 | Selecionado |
| 8 | Não selecionado |
| 9 | Em execução |
| 10 | Conclusão (aguardando avaliação) |
| 11 | Concluído |
| 12 | Não aceito |
| 13 | Inativo |
| 14 | Cancelado |

---

## Fluxos

### 1. consultar_projetos

**Descrição:** Listar e filtrar projetos de ensino

**Pré-condições:**
- Usuário logado no SUAP

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/admin/projetos_ensino/projeto/` | Acessar listagem de projetos |
| 2 | verificar | `table` | Verificar que a tabela de projetos está visível |

---

### 2. consultar_projeto_detalhe

**Descrição:** Visualizar detalhes de um projeto específico

**Pré-condições:**
- Usuário logado no SUAP
- ID do projeto conhecido

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/` | Acessar página de detalhe do projeto |
| 2 | verificar | `h1, h2` | Verificar que o título do projeto aparece |

---

### 3. consultar_equipe_projeto

**Descrição:** Ver equipe de um projeto de ensino

**Pré-condições:**
- Usuário logado no SUAP
- ID do projeto conhecido

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=equipe` | Acessar aba Equipe do projeto |
| 2 | verificar | `table` | Verificar que a tabela de equipe está visível |

---

### 4. consultar_conclusao_projeto

**Descrição:** Ver conclusão/relatório final de um projeto

**Pré-condições:**
- Usuário logado no SUAP
- ID do projeto conhecido
- Projeto em situação Conclusão ou Concluído

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=conclusao` | Acessar aba Conclusão do projeto |
| 2 | verificar | `table, .box` | Verificar que os dados de conclusão estão visíveis |

---

### 5. listar_editais_abertos

**Descrição:** Listar editais de ensino com inscrições abertas para submissão de projetos

**Pré-condições:**
- Usuário logado no SUAP

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/editais_abertos/` | Acessar página de editais abertos (menu Ensino > Projetos > Adicionar projeto) |
| 2 | verificar | `h2, h3` | Verificar que os editais abertos estão listados |

---

### 6. adicionar_projeto

**Descrição:** Abrir formulário de novo projeto para um edital específico. Após salvar, o projeto fica "Em Edição" e o usuário deve preencher abas adicionais (equipe, metas, plano, etc.).

**Pré-condições:**
- Edital aberto para submissão
- Usuário logado como servidor/docente
- ID do edital conhecido

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/adicionar_projeto/{edital_id}/` | Acessar formulário de adicionar projeto para o edital |
| 2 | preencher_formulario | *(ver seção Formulário: Adicionar Projeto)* | Preencher todos os campos obrigatórios das seções: Dados Gerais, Dados do Projeto, Descrição do Projeto, e aceitar o Termo de Compromisso |
| 3 | clicar | `input[type='submit'][value='Salvar'], button.btn-success` | Salvar projeto (fica em situação "Em Edição") |

**Pós-passos:**

| Funcionalidade | Descrição |
|---|---|
| equipe | Adicionar membros da equipe (aba Equipe) |
| metas_atividades | Cadastrar metas e atividades com cronograma |
| caracterizacao_beneficiarios | Adicionar público-alvo e quantidade de beneficiários |
| plano_aplicacao | Preencher memória de cálculo |
| plano_desembolso | Cadastrar pagamentos mensais |
| enviar_pre_avaliacao | Enviar projeto para pré-avaliação |

---

### 7. submeter_projeto

**Descrição:** Fluxo completo para submeter um novo projeto de ensino: escolher edital, preencher formulário, e salvar.

**Pré-condições:**
- Edital aberto para submissão
- Usuário logado como servidor/docente

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/editais_abertos/` | Acessar página de editais abertos |
| 2 | clicar | `a.btn-success[href*='adicionar_projeto/{edital_id}']` | Clicar no botão "Adicionar projeto" do edital desejado |
| 3 | preencher_formulario | *(ver fluxo adicionar_projeto)* | Preencher formulário completo do projeto |
| 4 | clicar | `input[type='submit'][value='Salvar'], button.btn-success` | Salvar projeto |

**Pós-passos:**

| Funcionalidade | Descrição |
|---|---|
| equipe | Adicionar membros da equipe |
| metas_atividades | Cadastrar metas e atividades com cronograma |
| caracterizacao_beneficiarios | Adicionar público-alvo e quantidade de beneficiários |
| plano_aplicacao | Preencher memória de cálculo |
| plano_desembolso | Cadastrar pagamentos mensais |
| enviar_pre_avaliacao | Enviar projeto para pré-avaliação |

---

### 8. adicionar_equipe

**Descrição:** Adicionar membros à equipe do projeto

**Pré-condições:**
- Projeto já criado e salvo

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=equipe` | Acessar aba "Equipe" do projeto |
| 2 | clicar | `a[href*='adicionar'], .btn-success` | Clicar para adicionar novo membro |
| 3 | preencher_formulario | *(ver campos abaixo)* | Dados do membro da equipe |
| 4 | clicar | `input[type='submit']` | Salvar membro |

**Campos do formulário de membro:**

| Campo | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| tipo_membro | `#id_tipo` | seleção | sim | Tipo: aluno, servidor ou colaborador externo |
| membro | `#id_membro` | texto | sim | Nome ou matrícula do membro |
| carga_horaria | `#id_ch` | numero | sim | Carga horária semanal do membro |

---

### 9. enviar_pre_avaliacao

**Descrição:** Enviar projeto finalizado para pré-avaliação

**Pré-condições:**
- Todas as abas do projeto preenchidas
- Equipe, metas, plano de aplicação e desembolso cadastrados

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/` | Acessar a página do projeto |
| 2 | clicar | `a:has-text('Enviar para Pré-Avaliação'), button:has-text('Enviar')` | Clicar em "Enviar para Pré-Avaliação" |
| 3 | verificar | `.alert-success, .success` | Verificar mensagem de confirmação de envio |
