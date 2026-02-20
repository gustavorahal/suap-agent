# SUAP Knowledge Base

Base de conhecimento para automação e navegação do SUAP — sistema acadêmico do IFPR (suap.ifpr.edu.br).

## O que é este repositório?

Uma base de conhecimento estruturada que permite a qualquer assistente de IA com acesso a um navegador web guiar servidores e professores do IFPR no uso do SUAP. Contém:

- **Orientação de navegação** — URLs, menus, padrões de interface do SUAP
- **Passos de tarefas** — Como consultar dados, submeter projetos, preencher formulários
- **Conhecimento organizacional** — O que a instituição espera, boas práticas, erros comuns

## Para assistentes de IA

Leia [`guia-uso.md`](guia-uso.md) para entender seu papel e como usar esta base.

## Módulos documentados

| Módulo | Descrição | Link |
|--------|-----------|------|
| Ensino | Editais e projetos de ensino (PBIS, PROCORP, PIPE, etc.) | [ensino/](ensino/) |
| Gestão de Pessoas | Dados do servidor, contracheques, férias, afastamentos | [gestao-pessoas/](gestao-pessoas/) |

## Referência de navegação

Padrões de URL, seletores, menus e dicas gerais: [`navegacao.md`](navegacao.md)

## Como usar

1. Configure um assistente de IA com acesso a navegador (ex: Claude Code + Chrome, Gemini CLI + Playwright MCP, ChatGPT)
2. Cole o prompt inicial abaixo na primeira mensagem ou nas instruções personalizadas
3. Peça para realizar tarefas no SUAP em linguagem natural

### Prompt inicial

Cole este texto para carregar a base de conhecimento em qualquer LLM:

```
Você é um assistente que ajuda servidores do IFPR a navegar o sistema SUAP.

Para começar, leias suas instruções completas em https://raw.githubusercontent.com/gustavorahal/suap-agent/master/guia-uso.md

Sempre fale em português BR. Confirme com o usuário antes de submeter qualquer formulário.
```

## Contribuindo

Para adicionar um novo módulo:

1. Crie uma pasta com o nome do módulo (ex: `pesquisa/`)
2. Adicione `README.md` com visão geral e links
3. Adicione um arquivo `.md` por funcionalidade seguindo o template dos módulos existentes
4. Atualize a tabela de módulos neste README
