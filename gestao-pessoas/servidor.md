# Servidor

Página de perfil do servidor no SUAP. Exibe dados pessoais, funcionais, bancários, ocorrências/afastamentos, histórico funcional, funções, contracheques e férias. Acessível pela matrícula do servidor.

**URL base:** `/rh/servidor/{matricula}/`

**Perfis:** servidor, gestor_rh

---

## Abas

A página do servidor é organizada em 7 abas. Algumas podem ser acessadas diretamente via parâmetro `?tab=` na URL.

| Aba | Parâmetro `?tab=` | Acesso direto via URL |
|---|---|---|
| Geral | *(nenhum — aba padrão)* | Sim (URL base) |
| Ocorrências/Afastamentos | `ocorrencias_afastamentos` | Sim |
| Setores | `setores` | Sim |
| Histórico funcional | `historico_funcional` | Sim |
| Funções | `funcoes` | Sim |
| Contracheques | `contracheques` | Sim |
| Férias | `ferias` | Sim |

---

### 1. Geral

Aba padrão. Exibe dados pessoais (CPF, nome, nascimento, estado civil, sexo, dependentes, RG, título de eleitor, CNH), dados funcionais (matrícula, setor, exercício, situação, regime, jornada, cargo, classe/padrão, PGD) e dados bancários (banco, agência, conta).

#### Dados pessoais

| Campo |
|---|
| CPF |
| Nome do Registro |
| Nascimento |
| Estado Civil |
| Naturalidade |
| Sexo |
| Grupo Sanguíneo/Rh |
| Dependentes IR |
| Raça/Etnia |
| Nome do Pai |
| Nome da Mãe |
| PIS/PASEP |
| Titulação |
| Escolaridade |
| Endereço |
| Registro Geral (Identidade, Órgão Expedidor, UF, Data Expedição) |
| Título de Eleitor (Número, Zona, Seção, UF) |
| CNH (Número, Registro, Categoria, Emissão, Validade) |

#### Dados funcionais

| Campo |
|---|
| Matrícula |
| Setor SUAP |
| Lotação SIAPE |
| Exercício SIAPE |
| Situação |
| Regime |
| Jornada Trabalho |
| Opera Raio X |
| Início no Serviço Público |
| Tempo no serviço público |
| Data de Posse na Instituição |
| Início de Exercício na Instituição |
| Tempo de serviço na Instituição |
| Data de Posse no Cargo |
| Início Exercício no Cargo |
| Tempo de Serviço no Cargo |
| Cargo |
| Classe do Cargo |
| Padrão |
| Grupo do Cargo |
| Código da Vaga |
| Participa do PGD |
| Modalidade do PGD |

#### Dados bancários

| Campo |
|---|
| Banco |
| Agência |
| Conta corrente |

---

### 2. Ocorrências/Afastamentos

**URL:** `/rh/servidor/{matricula}/?tab=ocorrencias_afastamentos`

Resumo de afastamentos por ano (com total de dias) e tabelas de ocorrências e afastamentos vindos do SIGEPE.

#### Resumo por ano

Cards com total de afastamentos por ano e total geral.

#### Ocorrências

| Tipo Ocorrência | Descrição | Início | Término | Total Dias |
|---|---|---|---|---|

#### Afastamentos (fonte SIGEPE)

| Tipo de Afastamento | Descrição | Período | Total de Dias |
|---|---|---|---|

---

### 3. Setores

**URL:** `/rh/servidor/{matricula}/?tab=setores`

Histórico de setores onde o servidor esteve lotado. Pode estar vazio se não houver movimentações registradas.

---

### 4. Histórico funcional

**URL:** `/rh/servidor/{matricula}/?tab=historico_funcional`

Linha do tempo do servidor com eventos como entrada no PCA, início de exercício, progressão funcional, jornada de trabalho, regime jurídico, e tempo de serviço acumulado (real e ficto).

#### Linha do Tempo

Eventos possíveis:

- Entrada no PCA
- Início de Exercício ou Progressão Funcional
- Início nova Jornada de Trabalho
- Início novo regime jurídico
- Fim de um posicionamento ou PCA

#### Tempo de Serviço

| Campo |
|---|
| Tempo Real |
| Tempo Ficto |

---

### 5. Funções

**URL:** `/rh/servidor/{matricula}/?tab=funcoes`

Lista de funções gratificadas (FG) ou cargos de direção (CD) exercidos pelo servidor. Badge com contagem de funções ativas.

---

### 6. Contracheques

**URL:** `/rh/servidor/{matricula}/?tab=contracheques`

Exibe o último contracheque com tabela de rendimentos e descontos. Mostra totais de bruto, desconto e líquido. Botão "Todos os Contracheques" para histórico.

#### Último Contracheque

| Descrição | Sequência | Prazo | Valor |
|---|---|---|---|

**Totais:** Bruto, Desconto, Líquido

---

### 7. Férias

**URL:** `/rh/servidor/{matricula}/?tab=ferias`

Férias do servidor organizadas por exercício (ano). Sub-abas de ano (ex: 2026, 2025, ..., 2015). Cada exercício mostra parcelas com detalhes.

#### Exercício por ano

| Parcela | Data Início | Data Fim | Dias | Adiantamento 13o | Situação |
|---|---|---|---|---|---|

**Situações possíveis:** ENCERRADA, PROGRAMADA, EM ANDAMENTO

---

## Fluxos

### consultar_dados_servidor

**Descrição:** Consultar dados gerais de um servidor pela matrícula

**Pré-condições:**

- Usuário logado no SUAP
- Matrícula do servidor conhecida

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/rh/servidor/{matricula}/` | Acessar página do servidor pela matrícula |
| 2 | verificar | `h1, h2` | Verificar que o nome do servidor aparece no título da página |

---

### consultar_contracheque

**Descrição:** Consultar o último contracheque do servidor

**Pré-condições:**

- Usuário logado no SUAP
- Matrícula do servidor conhecida

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/rh/servidor/{matricula}/?tab=contracheques` | Acessar aba Contracheques do servidor |
| 2 | verificar | `table` | Verificar que a tabela de contracheque está visível |

---

### consultar_ferias

**Descrição:** Consultar férias do servidor por exercício

**Pré-condições:**

- Usuário logado no SUAP
- Matrícula do servidor conhecida

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/rh/servidor/{matricula}/?tab=ferias` | Acessar aba Férias do servidor |
| 2 | verificar | `table` | Verificar que a tabela de férias está visível |

---

### consultar_afastamentos

**Descrição:** Consultar ocorrências e afastamentos do servidor

**Pré-condições:**

- Usuário logado no SUAP
- Matrícula do servidor conhecida

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/rh/servidor/{matricula}/?tab=ocorrencias_afastamentos` | Acessar aba Ocorrências/Afastamentos do servidor |
| 2 | verificar | `table` | Verificar que as tabelas de ocorrências e afastamentos estão visíveis |

---

### consultar_historico_funcional

**Descrição:** Consultar a linha do tempo funcional do servidor

**Pré-condições:**

- Usuário logado no SUAP
- Matrícula do servidor conhecida

**Passos:**

| # | Ação | Destino / Seletor | Descrição |
|---|---|---|---|
| 1 | navegar | `/rh/servidor/{matricula}/?tab=historico_funcional` | Acessar aba Histórico funcional do servidor |
| 2 | verificar | `.timeline, .line-do-tempo, table` | Verificar que a linha do tempo está visível |
