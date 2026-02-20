# Projetos de Ensino

Submissão e gestão de projetos de ensino no SUAP. Programas disponíveis: PBIS, PROCORP, PIPE, PAPE, entre outros. Acesso via menu Ensino > Projetos > Projetos.

- **Módulo:** ensino
- **URL base:** `/admin/projetos_ensino/projeto/`
- **Perfis:** servidor, docente

---

## Permissões Necessárias

**Módulo SUAP:** Ensino :: Projetos de Ensino

O acesso às funcionalidades de Projetos de Ensino depende dos grupos atribuídos ao usuário. Sem o grupo adequado, o SUAP pode exibir erro 403 (acesso negado) ou simplesmente não mostrar o menu/botão correspondente.

| Grupo | Permite |
|---|---|
| Visualizador de Projetos de Ensino | Consultar projetos e seus detalhes |
| Coordenador de Projetos de Ensino | Criar, editar e submeter projetos |
| Avaliador de Projetos de Ensino | Avaliar projetos submetidos |
| Monitor de Projetos de Ensino | Acompanhar projetos em execução |
| projetos_ensino Administrador | Acesso administrativo total ao módulo |
| Integrante da Comissão de Acompanhamento | Acompanhamento institucional dos projetos |

> **Como verificar suas permissões:** Acesse `/comum/grupos_usuario/{seu_id}/` e procure pela seção "Ensino :: Projetos de Ensino".
>
> **Sem acesso?** Solicite a inclusão no grupo necessário ao administrador do campus. Geralmente via Central de Serviços do SUAP ou contato direto com a DIRGE/PROEN.

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

## Detalhe do Projeto (Visualização / Edição)

**URL:** `/projetos_ensino/projeto/{id}/`
**Título da página:** "Projeto de Ensino Contínuo: {titulo}" ou "Projeto de Ensino: {titulo}" (conforme tipo do edital)

### Alerta de Modo de Edição

Quando o projeto está "Em edição", exibe banner amarelo:
> "Este projeto está em modo de edição. Quando o preenchimento for concluído, clique no botão 'Enviar Projeto'. Lembre-se de que o prazo final para submissão (envio) é {data_fim_inscricoes}."

### Cabeçalho

| Campo | Descrição |
|---|---|
| Título do Projeto | Nome completo do projeto |
| Período do Edital | Fase atual (ex: "Inscrição") |
| Campus do Projeto | Campus vinculado |
| Setor | Setor do campus |
| Carga Horária do Projeto | Total em horas |
| Monitor do Projeto | Servidor monitor (se atribuído) |
| Badge de situação | "Em edição", "Enviado", "Em Execução", etc. |

### Botões de Ação

| Botão | Cor | Descrição |
|---|---|---|
| Enviar Projeto | verde | Submete o projeto para pré-avaliação. Só aparece quando projeto está "Em edição" |
| Remover Projeto | vermelho | Remove o projeto permanentemente |
| Inativar Projeto | vermelho | Inativa o projeto |
| Editar Projeto | verde (dentro da aba Dados do Projeto) | Redireciona para formulário de edição |
| Visualizar | dropdown cinza | Opções de visualização |

### Abas

As abas visíveis dependem da configuração do edital e da situação do projeto. As 6 abas abaixo aparecem sempre. Abas adicionais (Plano de Aplicação, Plano de Desembolso, Fotos, Registros de Frequência, Pendências, Conclusão) podem aparecer em projetos com financiamento ou em estágio avançado do ciclo de vida.

| # | Nome | Parâmetro `?tab=` | Descrição |
|---|---|---|---|
| 1 | Dados do Projeto | *(padrão)* | Dados do projeto, datas, status de seleção e textos descritivos. Badge ✓ quando completo |
| 2 | Dados do Edital | `dados_edital` | Informações somente leitura do edital vinculado (datas, anexos) |
| 3 | Caracterização dos Beneficiários | `caracterizacao_beneficiario` | Público-alvo e quantidade de beneficiários |
| 4 | Equipe | `equipe` | Membros do projeto. Badge numérico com contagem de membros |
| 5 | Metas/Atividades | `metas` | Metas e atividades do projeto |
| 6 | Anexos | `anexos` | Arquivos anexados ao projeto |

**Abas condicionais** (podem não aparecer):

| Nome | Parâmetro `?tab=` | Condição |
|---|---|---|
| Plano de Aplicação | `plano_de_aplicacao` | Edital com valor financiado > 0 |
| Plano de Desembolso | `plano_de_desembolso` | Edital com valor financiado > 0 |
| Fotos | `fotos` | Projeto em execução ou concluído |
| Registros de Frequência/Atividade Diária | `registros_de_frequencia_atividade_diaria` | Projeto em execução |
| Pendências | `pendencias` | Projeto com pendências |
| Conclusão | `conclusao` | Projeto em fase de conclusão |

### Aba: Dados do Projeto

Duas seções colapsáveis:

**Seção "Dados do Projeto":**

| Campo | Descrição |
|---|---|
| Início da Execução | Data de início |
| Término da Execução | Data de término |
| Eixo Temático | Eixo(s) selecionado(s) |
| Interdisciplinar? | Badge Sim/Não |
| Possui relação institucional com Pesquisa/Extensão? | Badge Sim/Não |
| Há parceiros externos? | Badge Sim/Não |
| Pré-seleção | Status (ex: "Aguardando finalização da inscrição.") + Data da Pré-seleção |
| Seleção | Status (ex: "Em Espera") + Data da Seleção |
| Pontuação | Status (ex: "Não se aplica") |
| Data da Divulgação | Data de divulgação do resultado |

Botão: **Editar Projeto** — abre formulário de edição dos dados.

**Seção "Discriminação do Projeto"** — campos de texto longo (somente leitura na visualização):

- Resumo
- Introdução
- Justificativa
- Objetivo Geral
- Metodologia da Execução do Projeto
- Acompanhamento e Avaliação do Projeto Durante a Execução
- Resultados Esperados e Disseminação dos Resultados
- Referências

### Aba: Dados do Edital

Informações somente leitura do edital vinculado:

| Campo | Descrição |
|---|---|
| Título do edital | Nome do edital |
| Período de Inscrição | Datas de início e fim (destaque amarelo se período atual) |
| Período de Pré-seleção | Datas de início e fim |
| Período de Seleção | Datas de início e fim |
| Divulgação do Resultado | Data |
| Anexos | Arquivos do edital ou "Aguardando submissão de arquivos." |

### Aba: Caracterização dos Beneficiários

Botão: **Adicionar Caracterização dos Beneficiários**

Modal "Adicionar Caracterização do Beneficiário":

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| tipo_beneficiario | Tipo de beneficiário | autocomplete | sim | Ver opções abaixo |
| quantidade | Quantidade Prevista de Pessoas a Atender | número | sim | — |

**Tipo de beneficiário — opções:**

| Valor |
|---|
| Público Interno do Instituto |
| Instituições Governamentais Federais |
| Instituições Governamentais Estaduais |
| Instituições Governamentais Municipais |
| Organizações de Iniciativa Privada |
| Movimentos Sociais |
| Organizações Não-governamentais |
| Organizações Sindicais |
| Grupos Comunitários |
| Público externo |

> Pode-se adicionar múltiplas caracterizações (ex: "Público Interno do Instituto" + "Público externo").

### Aba: Equipe

Badge numérico no título da aba mostra a quantidade de membros.

**Botões:** Adicionar Aluno, Adicionar Servidor, Adicionar Colaborador Externo

**Tabela de membros:**

| Coluna | Descrição |
|---|---|
| Ações | Visualizar (ícone olho), Editar (ícone lápis) |
| Membro | Nome e matrícula (ex: "Gustavo Matheus Rahal (2157473)") |
| Situação | Ativo (verde) / Inativo |
| Categoria/Titulação | Ex: "TÉCNICO-ADMINISTRATIVO (MESTRADO)", "DOCENTE (DOUTORADO)", "DISCENTE" |
| Bolsista | Sim/Não (badges coloridos) |
| Coordenador | Sim/Não (badges coloridos) |
| Carga Horária | Ex: "4 h" |
| Opções | Substituir Coordenador, Gerenciar Anexos, Plano de Trabalho, Dados bancários |

**Modal "Adicionar Aluno":**

| Campo | Label | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|---|
| bolsista | Bolsista | seleção (Sim/Não) | sim | Sim | Se o aluno recebe bolsa |
| carga_horaria | Carga Horária | número | sim | — | Carga horária semanal |
| indicar_posteriormente | Indicar o Aluno Posteriormente | checkbox | não | desmarcado | **Condicional:** só aparece se o edital tem "Permite Cadastrar Aluno sem Identificá-lo" marcado. Ao marcar, oculta os campos Participante e Data de Entrada |
| participante | Participante | autocomplete | condicional | — | Busca por nome ou matrícula do aluno. Oculto se "Indicar o Aluno Posteriormente" marcado |
| data_entrada | Data de Entrada | data | condicional | — | "A data não pode ser maior do que hoje." Oculto se "Indicar o Aluno Posteriormente" marcado |

> **Comportamento condicional:** Quando o edital tem "Permite Cadastrar Aluno sem Identificá-lo" habilitado, Participante e Data de Entrada deixam de ser obrigatórios. Se o checkbox "Indicar o Aluno Posteriormente" for marcado, esses campos são completamente ocultados — útil para reservar vagas de alunos antes de definir quem serão.

**Modal "Adicionar Participante" (Servidor):**

Mesmos campos do Aluno, com diferença no help text:
- Carga Horária: "Caso o participante seja docente, informe a carga horária semanal em horas/aula"

**Modal "Adicionar Participante" (Colaborador Externo):**

Mesmos campos do Aluno, com diferença no help text:
- Participante: "O Colaborador precisa ser cadastrado previamente pelo Diretor Acadêmico ou pela Comissão de Acompanhamento."

### Aba: Metas/Atividades

Botão: **Adicionar Meta**

Modal "Adicionar Meta":

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| ordem | Ordem | número | sim | Número inteiro ≥ 1 |
| descricao | Descrição | textarea | sim | Descrição da meta. Contador de caracteres visível |

> Após adicionar uma meta, é possível adicionar **atividades** vinculadas a ela (com responsável, data início/fim e indicadores).

### Aba: Anexos

Duas seções:

- **Anexos da Equipe:** Arquivos exigidos pelo edital (via aba "Anexos dos Projetos" do edital). Se o edital não exige anexos, exibe "Nenhum anexo vinculado à equipe foi exigido pelo edital."
- **Outros Anexos:** Arquivos livres do projeto. Botão "Adicionar Anexo". Se vazio: "O projeto não possui anexos adicionais."

### Aba: Conclusão (condicional)

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

> **Nota:** Os campos deste formulário podem variar conforme a configuração do edital. Exemplo: o campo "Ação" pode não aparecer em certos editais, e "Setor" pode ser exibido em outros. O dropdown de Campus exibe apenas campi com oferta cadastrada no edital (ver [editais.md](editais.md) — Plano de Oferta por Campus).

### Seção 1: Dados Gerais

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| edital | Edital | *(somente leitura)* | somente_leitura | — | Nome do edital (preenchido automaticamente) |
| campus | Campus | `#id_campus` | seleção | sim | Campus onde o projeto será executado. Exibe apenas campi com oferta no edital |
| setor | Setor | `#id_setor` | seleção | sim* | Setor do campus. Auto-preenche ao selecionar Campus. *Pode não aparecer dependendo do edital |
| titulo | Título do projeto | `#id_titulo` | texto | sim | Título completo do projeto de ensino |
| acao | Ação | `#id_acao` | texto | sim* | Ação administrativa vinculada ao projeto. *Pode não aparecer dependendo do edital |
| carga_horaria_coordenador | Carga Horária Semanal do Coordenador | `#id_carga_horaria` | numero | sim | Horas semanais dedicadas pelo coordenador |

### Seção 2: Dados do Projeto

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| inicio_execucao | Início da Execução | `#id_inicio_execucao` | data (dd/mm/aaaa) | sim | Data de início da execução do projeto |
| termino_execucao | Término da Execução | `#id_fim_execucao` | data (dd/mm/aaaa) | sim | Data de término da execução |
| carga_horaria_total | Carga horária total para desenvolvimento do projeto | `#id_carga_horaria_total` | numero | sim | Cálculo: Carga Horária Semanal do Coordenador × número de semanas entre Início e Término da Execução |
| eixo_tematico | Eixo Temático | `#id_eixo` | multiseleção | sim | Eixos temáticos do projeto (múltipla escolha) |
| projeto_interdisciplinar | Projeto Interdisciplinar? | `#id_interdisciplinar` | checkbox | não | Indica se o projeto envolve mais de uma disciplina |
| disciplina | Disciplina | `#id_disciplina` | multiseleção | não | Disciplinas envolvidas no projeto |
| curso | Curso | `#id_curso` | multiseleção | não | Cursos associados ao projeto |
| relacao_institucional | Possui relação institucional com Pós-graduação / Pesquisa/Extensão? | `#id_pos_graduacao` | checkbox | não | Label varia conforme edital: "Pós-graduação" ou "Pesquisa/Extensão" |
| parceiro_externo | Há parceiro externo? | `#id_parceiro_externo` | checkbox | não | Indica se há parceiros externos envolvidos |

### Seção 3: Descrição do Projeto

> Todos os campos usam editor rich text (CKEditor).
> Para preencher via automação: `CKEDITOR.instances['id_campo'].setData('<p>texto</p>')`

| Campo | Label | Seletor | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|---|
| resumo | Resumo | `#id_resumo` | rich_text | sim | — |
| introducao | Introdução | `#id_introducao` | rich_text | sim | Pode conter texto pré-preenchido do edital |
| justificativa | Justificativa e Relevância | `#id_justificativa` | rich_text | sim | — |
| objetivo_geral | Objetivo Geral | `#id_objetivo_geral` | rich_text | sim | — |
| metodologia | Metodologia da execução do projeto | `#id_metodologia` | rich_text | sim | — |
| acompanhamento | Acompanhamento e avaliação das atividades durante a execução | `#id_acompanhamento_e_avaliacao` | rich_text | sim | — |
| resultados_esperados | Resultados Esperados e Disseminação dos Resultados | `#id_resultados_esperados` | rich_text | sim | — |
| referencias | Referências | `#id_referencias` | rich_text | sim | — |

### Seção 4: Termo de Compromisso

> **Nota:** Esta seção só aparece se o edital tiver Termos de Compromisso configurados. Caso contrário, o formulário vai direto do campo Referências ao botão Salvar.

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
- **Permissão:** qualquer grupo do módulo Ensino :: Projetos de Ensino (mínimo: Visualizador de Projetos de Ensino)

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
- **Permissão:** Visualizador de Projetos de Ensino (ou superior)

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
- **Permissão:** Visualizador de Projetos de Ensino (ou superior)

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
- **Permissão:** Visualizador de Projetos de Ensino (ou superior)

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
- **Permissão:** Coordenador de Projetos de Ensino (para submeter projetos)

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
- **Permissão:** Coordenador de Projetos de Ensino

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
- **Permissão:** Coordenador de Projetos de Ensino

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
- **Permissão:** Coordenador de Projetos de Ensino (ser coordenador do projeto)

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=equipe` | Acessar aba "Equipe" do projeto |
| 2 | clicar | `Adicionar Aluno` / `Adicionar Servidor` / `Adicionar Colaborador Externo` | Escolher o tipo de membro a adicionar. Cada botão abre um modal com os mesmos campos |
| 3 | preencher_formulario | *(ver seção Aba: Equipe — modais)* | Preencher Bolsista, Carga Horária, Participante e Data de Entrada |
| 4 | clicar | `Salvar` | Salvar membro na equipe |
| 5 | repetir | passos 2-4 | Repetir para cada membro adicional |

---

### 9. enviar_pre_avaliacao

**Descrição:** Enviar projeto finalizado para pré-avaliação

**Pré-condições:**
- Todas as abas do projeto preenchidas
- Equipe, metas, plano de aplicação e desembolso cadastrados
- **Permissão:** Coordenador de Projetos de Ensino (ser coordenador do projeto)

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/` | Acessar a página do projeto |
| 2 | clicar | `Enviar Projeto` | Clicar no botão verde "Enviar Projeto" no topo da página |
| 3 | verificar | `.alert-success, .success` | Verificar mensagem de confirmação de envio |

---

### 10. adicionar_caracterizacao_beneficiarios

**Descrição:** Cadastrar público-alvo e quantidade de beneficiários do projeto

**Pré-condições:**
- Projeto já criado e salvo
- **Permissão:** Coordenador de Projetos de Ensino (ser coordenador do projeto)

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=caracterizacao_beneficiario` | Acessar aba "Caracterização dos Beneficiários" |
| 2 | clicar | `Adicionar Caracterização dos Beneficiários` | Abrir modal de cadastro |
| 3 | preencher_formulario | *(ver seção Aba: Caracterização dos Beneficiários)* | Selecionar tipo de beneficiário e quantidade |
| 4 | clicar | `Salvar` | Salvar caracterização |
| 5 | repetir | passos 2-4 | Repetir para cada tipo de beneficiário |

---

### 11. adicionar_meta

**Descrição:** Cadastrar metas do projeto

**Pré-condições:**
- Projeto já criado e salvo
- **Permissão:** Coordenador de Projetos de Ensino (ser coordenador do projeto)

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/projeto/{id}/?tab=metas` | Acessar aba "Metas/Atividades" |
| 2 | clicar | `Adicionar Meta` | Abrir modal de cadastro |
| 3 | preencher_formulario | *(ver seção Aba: Metas/Atividades)* | Preencher ordem e descrição da meta |
| 4 | clicar | `Salvar` | Salvar meta |
| 5 | repetir | passos 2-4 | Repetir para cada meta adicional |
