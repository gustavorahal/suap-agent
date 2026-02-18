# CLAUDE.md

## Project Overview

SUAP Knowledge Base — a structured knowledge repository for navigating and automating the SUAP academic system (IFPR). No code, no runtime. Just markdown files that any LLM with browser access can use to guide IFPR staff through SUAP.

## Language

All content in **Portuguese BR** with proper diacritics (acentuação). Never write Portuguese without accents.

## Repository Structure

```
├── README.md              # Entry point — what is SUAP, module index
├── guia-uso.md            # Instructions for the AI assistant
├── navegacao.md           # Cross-cutting navigation patterns & gotchas
├── ensino/
│   ├── README.md          # Module overview
│   └── projetos.md        # Teaching projects: flows, fields, org knowledge
├── gestao-pessoas/
│   ├── README.md          # Module overview
│   └── servidor.md        # Employee data: flows, fields, org knowledge
└── docs/plans/            # Design documents
```

## Content Conventions

Each functionality file follows a consistent template:

1. Title and description
2. URL and access path
3. Page structure (tabs, fields, tables)
4. Step-by-step tasks (with URLs, selectors, expected results)
5. Organizational knowledge and tips

## Adding New Modules

1. Create a directory: `<module-name>/`
2. Add `README.md` with module overview and links to functionalities
3. Add one `.md` file per functionality following the template in existing modules
4. Update root `README.md` module table

## Navigation Knowledge

`navegacao.md` is the central source for SUAP navigation patterns. Update it when discovering new URL patterns, selector behaviors, or tab accessibility.
