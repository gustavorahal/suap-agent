# Editais de Ensino

Criação e gestão de editais de projetos de ensino no SUAP. Editais definem as regras, prazos e vagas para submissão de projetos pelos servidores/docentes.

- **Módulo:** ensino
- **URL base (admin):** `/admin/projetos_ensino/edital/`
- **URL base (visualização):** `/projetos_ensino/edital/{id}/`
- **Perfis:** administrador de projetos de ensino
- **Menu:** Ensino > Projetos > Editais > Gerenciar editais

---

## Listagem de Editais

**URL:** `/admin/projetos_ensino/edital/`
**Título da página:** "Editais"

### Filtros

| Nome | Tipo |
|---|---|
| Texto | texto_livre |
| Ano | seleção |
| Edital de Campus | autocomplete |

### Abas de Status

| Aba |
|---|
| Todos |
| Abertos |
| Em Execução |
| Encerrados |

### Colunas da Tabela

| Coluna |
|---|
| Ações (visualizar, editar, remover) |
| Título |
| Descrição |
| Tipo do Edital |
| Forma de Seleção |
| Início das Inscrições |
| Fim das Inscrições |
| Proporção de Projetos Encerrados |

---

## Formulário: Adicionar Edital

**URL:** `/admin/projetos_ensino/edital/add/`
**Título da página:** "Adicionar Edital"

Após salvar, o sistema redireciona para a listagem. Para acessar as abas de gestão (anexos, ofertas por campus, etc.), use **"Salvar e continuar editando"** — isso recarrega a página de edição. A partir daí, acesse a visualização do edital em `/projetos_ensino/edital/{id}/`.

### Seção 1: Dados Gerais

| Campo | Label | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|---|
| titulo | Título | texto | sim | — | Nome do edital |
| descricao | Descrição | textarea | sim | — | Descrição completa do edital. Contador de caracteres visível |
| tipo_edital | Tipo do Edital | seleção | sim | — | Ver opções abaixo |
| forma_selecao | Forma de Seleção | seleção | sim | Campus | Ver "Implicações da Forma de Seleção" |
| edital_campus | Edital de Campus | checkbox | não | desmarcado | Se marcado, projetos podem ser avaliados por servidores do mesmo campus do projeto |
| arquivo | Arquivo | arquivo | não | — | PDF do edital. Máximo 10 MB |

**Tipo do Edital — opções:**

| Valor | Descrição |
|---|---|
| Ensino | Edital convencional com período definido de inscrições |
| Ensino Contínuo | Edital de fluxo contínuo, inscrições abertas por período prolongado |

> **Atenção:** O tipo do edital fica somente leitura após a criação. Não é possível alterá-lo depois.

**Forma de Seleção — opções e implicações:**

| Valor | Descrição |
|---|---|
| Campus | Seleção descentralizada — cada campus tem sua própria cota de vagas |
| Geral | Seleção centralizada — vagas definidas globalmente, sem separação por campus |

> **Se Forma de Seleção = "Campus":**
> Após salvar o edital, é **obrigatório** acessar a aba "Plano de Oferta por Campus" (na visualização do edital) e adicionar uma oferta para **cada campus participante**. Sem isso, os campi não terão vagas disponíveis para pré-seleção e seleção de projetos.

### Seção 2: Calendário

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| inicio_inscricoes | Início das Inscrições | datetime | sim | Quando abre o período de submissão de projetos |
| fim_inscricoes | Fim das Inscrições | datetime | sim | Quando fecha o período de submissão |
| inicio_pre_selecao | Início da Pré-Seleção | datetime | condicional | Início da fase de pré-seleção |
| inicio_selecao | Início da Seleção | datetime | condicional | Início da fase de seleção |
| fim_selecao | Fim da Seleção | datetime | condicional | Fim da fase de seleção |
| inicio_interposicao_recursos | Início da Interposição de Recursos | datetime | não | Abertura do período de recursos |
| fim_interposicao_recursos | Fim da Interposição de Recursos | datetime | não | Encerramento do período de recursos |
| divulgacao_selecao | Divulgação da Seleção | datetime | condicional | Data de publicação do resultado |

> **Campos condicionalmente obrigatórios:** Quando Tipo do Edital = "Ensino", os campos Início da Pré-Seleção, Início da Seleção, Fim da Seleção e Divulgação da Seleção tornam-se **obrigatórios**. Para Tipo "Ensino Contínuo", estes campos são opcionais.

### Seção 3: Configurações do Edital

| Campo | Label | Tipo | Padrão | Descrição |
|---|---|---|---|---|
| participacao_aluno_obrigatoria | Participação de Aluno Obrigatória | checkbox | marcado | Todos os projetos devem ter aluno na equipe |
| participacao_servidor_obrigatoria | Participação de Servidor Obrigatória | checkbox | marcado | Todos os projetos devem ter servidor na equipe |
| valor_financiado | Valor Financiado por Projeto | número | 0,0 | Valor em reais disponível por projeto |
| exige_licoes_aprendidas | Exige Lições Aprendidas | checkbox | desmarcado | Coordenadores devem cadastrar lições aprendidas |
| exige_avaliacao_alunos | Exige Avaliação dos Alunos | checkbox | desmarcado | Coordenadores devem avaliar os alunos |
| permite_aluno_sem_identificar | Permite Cadastrar Aluno sem Identificá-lo | checkbox | desmarcado | **Recomendado marcar.** Permite registrar participação de alunos sem indicar quais especificamente. **Efeito:** no projeto, o modal "Adicionar Aluno" exibe checkbox "Indicar o Aluno Posteriormente" — ao marcar, oculta os campos Participante e Data de Entrada (ver [projetos.md](projetos.md) — Aba: Equipe) |
| aluno_graduacao_submete | Aluno de graduação pode submeter | checkbox | desmarcado | Alunos de graduação podem submeter projetos |
| pode_escolher_campus | Pode escolher campus de submissão | checkbox | desmarcado | Coordenador pode vincular projeto a qualquer campus |

### Seção 4: Termos de Compromisso

Todos os campos usam editor rich text (CKEditor).

| Campo | Label | Descrição |
|---|---|---|
| termo_coordenador | Termo de Compromisso do Coordenador | Obrigações do coordenador do projeto |
| termo_servidor | Termo de Compromisso do Servidor | Obrigações do servidor participante do projeto |
| termo_aluno | Termo de Compromisso do Aluno | Obrigações do aluno participante do projeto |
| termo_colaborador_externo | Termo de Compromisso do Colaborador Externo | Obrigações do colaborador externo participante do projeto |

### Botões

| Botão | Descrição |
|---|---|
| Salvar | Salva e redireciona para a listagem |
| Salvar e adicionar outro(a) | Salva e abre formulário em branco para novo edital |
| Salvar e continuar editando | Salva e permanece na página de edição (necessário para depois acessar a visualização com abas) |
| Remover | *(somente na edição)* Remove o edital |

---

## Visualização do Edital (Gestão)

**URL:** `/projetos_ensino/edital/{id}/`
**Título da página:** "{titulo} - Edital de Ensino - {tipo}"

Página de gestão do edital após criação. Exibe dados resumidos no cabeçalho e abas para configuração complementar.

### Cabeçalho — Dados do Edital

| Campo |
|---|
| Título |
| Forma de Seleção |
| Descrição |
| Início das inscrições |
| Fim das inscrições |
| Arquivo digitalizado |

### Botões do Cabeçalho

| Botão | Descrição |
|---|---|
| Carregar arquivo | Upload do PDF do edital |
| Editar Edital | Abre a página admin de edição (`/admin/projetos_ensino/edital/{id}/change/`) |

### Abas

| # | Nome | Parâmetro `?tab=` | Conteúdo | Ação |
|---|---|---|---|---|
| 0 | Anexos do Edital | *(padrão)* | Arquivos anexados ao edital | Adicionar Anexo |
| 1 | Anexos dos Projetos | `tab1` | Tipos de anexo que projetos devem enviar | Adicionar Anexo |
| 2 | Fonte de Recursos | `tab2` | Fontes de financiamento do edital | Adicionar Recurso |
| 3 | Plano de Oferta por Campus | `tab3` | Vagas por campus (pré-seleção e seleção) | Adicionar Oferta |
| 4 | Critérios de Avaliação da Qualificação do Projeto | `tab4` | Critérios usados na avaliação dos projetos | Adicionar Critério de Avaliação |

> **Aba "Plano de Oferta por Campus" só é relevante quando Forma de Seleção = "Campus".**
> Sem ofertas cadastradas, nenhum campus terá vagas para projetos.

---

## Formulário: Adicionar Oferta de Projeto

**Acesso:** Aba "Plano de Oferta por Campus" → botão "Adicionar Oferta"
**Exibição:** modal sobreposto à página

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| campus | Campus | autocomplete | sim | Campus que receberá as vagas |
| pre_selecionados | Pré-Selecionados | número | sim | Quantos projetos poderão ser pré-selecionados pelo coordenador do respectivo campus |
| selecionados | Selecionados | número | sim | Quantos projetos serão selecionados para execução |

> **Dica:** Cadastre uma oferta para cada campus participante. Se um campus não tiver oferta cadastrada, servidores daquele campus não terão vagas disponíveis.

---

## Formulário: Adicionar Anexo do Edital

**Acesso:** Aba "Anexos do Edital" → botão "Adicionar Anexo"
**Exibição:** modal sobreposto à página

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| nome | Nome | texto | sim | Nome do anexo |
| descricao | Descrição | textarea | não | Descrição do anexo. Contador de caracteres visível |
| arquivo | Arquivo | arquivo | não | Arquivo do anexo. Máximo 10 MB |
| ordem | Ordem | número | sim | Número inteiro ≥ 1. Define a ordem de exibição |

---

## Formulário: Adicionar Anexo dos Projetos

**Acesso:** Aba "Anexos dos Projetos" → botão "Adicionar Anexo"
**URL:** `/projetos_ensino/adicionar_anexo/{edital_id}/`
**Exibição:** página separada (não modal)

Define os tipos de anexo que os membros dos projetos deverão enviar durante a submissão.

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| anexo_edital | Anexo do Edital | autocomplete | não | Vincula a um anexo já cadastrado na aba "Anexos do Edital" |
| nome | Nome | texto | sim | Nome do tipo de anexo exigido |
| descricao | Descrição | textarea | não | Descrição do anexo esperado. Contador de caracteres visível |
| tipo_membro | Tipo de Membro | seleção | sim | Ver opções abaixo |
| vinculo | Tipo de Vínculo | seleção | sim | Ver opções abaixo |
| ordem | Ordem | número | sim | Número inteiro ≥ 1 |

**Tipo de Membro — opções:**

| Valor |
|---|
| Docente |
| Técnico Administrativo |
| Aluno |
| Coordenador Docente |

**Tipo de Vínculo — opções:**

| Valor |
|---|
| Bolsista |
| Voluntário |

> **Uso prático:** Configure aqui quais documentos cada tipo de participante deve anexar ao projeto. Exemplo: "Plano de trabalho" para Aluno Bolsista, "Declaração de carga horária" para Docente.

---

## Formulário: Adicionar Recurso

**Acesso:** Aba "Fonte de Recursos" → botão "Adicionar Recurso"
**Exibição:** modal sobreposto à página

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| origem_recurso | Origem | seleção | sim | Ver opções abaixo |
| valor_disponivel | Valor disponível por projeto (R$) | número | sim | Valor em reais disponível por projeto para essa fonte |
| despesa | Despesa | autocomplete | sim | Natureza da despesa (busca por código ou descrição) |

**Origem — opções:**

| Valor |
|---|
| Projetos de ensino |
| PRUNI |
| CAMPUS |

> **Efeito nos projetos:** Ao cadastrar pelo menos uma Fonte de Recursos no edital, todos os projetos vinculados passam a exibir duas abas adicionais: **"Plano de Aplicação"** (memória de cálculo dos gastos) e **"Plano de Desembolso"** (cronograma de pagamentos mensais). Sem recurso cadastrado, essas abas não aparecem nos projetos.

---

## Formulário: Adicionar Critério de Avaliação

**Acesso:** Aba "Critérios de Avaliação da Qualificação do Projeto" → botão "Adicionar Critério de Avaliação"
**Exibição:** modal sobreposto à página

| Campo | Label | Tipo | Obrigatório | Descrição |
|---|---|---|---|---|
| descricao | Descrição | textarea | sim | Texto descritivo do critério de avaliação. Contador de caracteres visível |
| pontuacao_maxima | Pontuação Máxima | número | sim | Nota máxima que o avaliador pode atribuir neste critério |
| ordem_desempate | Ordem para Desempate | número | sim | Ordem 1 indica que o critério será o primeiro a ser considerado para desempate |

> **Uso prático:** Defina os critérios que os avaliadores usarão para pontuar os projetos submetidos. A pontuação total do projeto será a soma das notas em cada critério. A ordem de desempate é usada quando dois projetos empatam na pontuação total.

---

## Fluxos

### 1. consultar_editais

**Descrição:** Listar e filtrar editais de ensino

**Pré-condições:**
- Usuário logado no SUAP
- **Permissão:** projetos_ensino Administrador

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/admin/projetos_ensino/edital/` | Acessar listagem de editais |
| 2 | verificar | `table` | Verificar que a tabela de editais está visível |

---

### 2. criar_edital

**Descrição:** Criar um novo edital de ensino. Após salvar, configurar abas complementares (ofertas por campus, anexos, fontes de recurso).

**Pré-condições:**
- Usuário logado no SUAP
- **Permissão:** projetos_ensino Administrador

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/admin/projetos_ensino/edital/add/` | Acessar formulário de criação |
| 2 | preencher_formulario | *(ver seção Formulário: Adicionar Edital)* | Preencher todas as seções obrigatórias |
| 3 | clicar | `Salvar e continuar editando` | Salvar edital e permanecer na edição |
| 4 | navegar | `/projetos_ensino/edital/{id}/` | Acessar visualização de gestão do edital |

**Pós-passos (condicionais):**

| Condição | Ação | Descrição |
|---|---|---|
| Forma de Seleção = "Campus" | Ir à aba "Plano de Oferta por Campus" (`?tab=tab3`) | **Obrigatório.** Adicionar uma oferta para cada campus participante |
| Sempre | Ir à aba "Anexos do Edital" | Opcional. Anexar PDF do edital e outros documentos |
| Sempre | Ir à aba "Anexos dos Projetos" | Opcional. Definir tipos de anexo exigidos dos projetos |
| Sempre | Ir à aba "Fonte de Recursos" | Opcional. Cadastrar fontes de financiamento |

---

### 3. adicionar_oferta_campus

**Descrição:** Cadastrar vagas de pré-seleção e seleção para um campus específico

**Pré-condições:**
- Edital já criado com Forma de Seleção = "Campus"
- **Permissão:** projetos_ensino Administrador

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/projetos_ensino/edital/{id}/?tab=tab3` | Acessar aba "Plano de Oferta por Campus" |
| 2 | clicar | `Adicionar Oferta` | Abrir modal de cadastro |
| 3 | preencher_formulario | *(ver seção Formulário: Adicionar Oferta de Projeto)* | Selecionar campus e definir quantidades |
| 4 | clicar | `Salvar` | Salvar oferta |
| 5 | repetir | passos 2-4 | Repetir para cada campus participante |

---

## Conhecimento Organizacional

- **Tipo do Edital** fica somente leitura após criação — escolha com cuidado. "Ensino Contínuo" para editais de fluxo contínuo com períodos longos; "Ensino" para editais convencionais com prazo definido.
- **Forma de Seleção "Campus"** é a mais comum no IFPR. Exige configuração extra (plano de oferta), mas permite controle descentralizado por campus.
- **Forma de Seleção "Geral"** simplifica a gestão (sem ofertas por campus), mas centraliza toda a seleção.
- **"Edital de Campus" (checkbox)** é diferente de "Forma de Seleção: Campus". O checkbox controla se avaliadores do mesmo campus podem avaliar projetos daquele campus.
- **Participação de Aluno e Servidor Obrigatória** vêm marcados por padrão — desmarcar se o edital permitir projetos sem aluno ou sem servidor.
- **"Permite Cadastrar Aluno sem Identificá-lo"** — **sempre marcar esta opção.** Na prática, coordenadores frequentemente precisam submeter o projeto antes de ter a confirmação dos alunos participantes. Sem esta opção marcada, o coordenador é obrigado a indicar cada aluno pelo nome no momento da inscrição, o que causa retrabalho e atrasos. Com a opção habilitada, o coordenador pode reservar vagas de alunos e indicá-los depois. Ao criar um edital a pedido do usuário, marcar por padrão. Ao orientar o usuário na criação, destacar que é importante marcar este checkbox.
- Os **Termos de Compromisso** são exibidos aos coordenadores/participantes durante a submissão do projeto. Devem refletir as regras do edital. Se nenhum termo for preenchido no edital, a seção de aceite **não aparece** no formulário de submissão de projeto.
- **Fonte de Recursos** controla a visibilidade de abas nos projetos: ao cadastrar pelo menos uma fonte de recurso, os projetos passam a exibir as abas "Plano de Aplicação" e "Plano de Desembolso". Sem recurso cadastrado, essas abas não existem nos projetos.

### Erros comuns e validações

- **"O edital selecionado não possui plano de oferta por campus cadastrado."** — Aparece ao tentar adicionar projeto a um edital com Forma de Seleção = "Campus" sem nenhuma oferta cadastrada. Solução: acessar a aba "Plano de Oferta por Campus" do edital e adicionar pelo menos uma oferta.
- **Campus não aparece no formulário de projeto** — O dropdown de Campus no formulário "Adicionar projeto" exibe **apenas** os campi que têm oferta cadastrada no plano de oferta. Se um campus não aparece, é porque não foi adicionado ao plano.

### Relação Edital → Projeto

A página de editais abertos (`/projetos_ensino/editais_abertos/`) é o ponto de entrada para submissão de projetos. Acesso via menu: **Ensino > Projetos > Adicionar projeto**.

Cada edital exibe: título, descrição, anexos, período de inscrições e lista de campi com oferta. O botão "Adicionar projeto" redireciona para `/projetos_ensino/adicionar_projeto/{edital_id}/` (formulário documentado em [projetos.md](projetos.md)).
