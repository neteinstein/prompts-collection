# 🧠 Prompts Collection

> A personal collection of real-world AI prompts and routines that automate everyday life.
> Uma coleção pessoal de prompts e rotinas de IA que automatizam o dia a dia.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
![Language](https://img.shields.io/badge/lang-PT%20%7C%20EN-green)
![Made with Claude](https://img.shields.io/badge/made%20with-Claude-d97757)

🇬🇧 [English](#-english) · 🇵🇹 [Português](#-português)

---

## 📚 Prompts

| # | Prompt | 🇬🇧 Description | 🇵🇹 Descrição | Schedule / Agendamento | Tools / Ferramentas |
|---|--------|-----------------|---------------|------------------------|---------------------|
| 1 | [🍽️ Weekly Meals](scheduled/weekly_meals.md) | Weekly email with 14 seasonal meals (6 meat, 6 fish, 2 veggie) + 1 exotic dish, full recipes, and a ready-to-paste shopping line. | Email semanal com 14 refeições da época (6 carne, 6 peixe, 2 vegetarianas) + 1 prato exótico, receitas completas e uma linha de compras pronta a colar. | Sunday morning / Domingo de manhã | Gmail, Web |
| 2 | [🛒 Weekly Groceries](scheduled/weekly_groceries.md) | Analyses 6 months of supermarket invoices in Gmail, learns the family's buying rhythm, and emails a list of what's running out. | Analisa 6 meses de faturas do supermercado no Gmail, aprende o ritmo da família e envia por email a lista do que está a acabar. | Friday 6pm / Sexta às 18h | Gmail, Python |

> 💡 Both routines end with a single line joined by **"mais"** that can be pasted into the [Continente Siga](https://www.continente.pt/siga/) app to build the cart in one tap.
> Ambas as rotinas terminam com uma linha unida por **"mais"** que se cola na app [Continente Siga](https://www.continente.pt/siga/) para criar o carrinho num toque.

---

## 🇬🇧 English

### What is this?

A collection of prompts I actually use. Most of them are **scheduled routines**: prompts that run on their own (e.g. as a scheduled task in Claude) and deliver something useful to my inbox: a meal plan, a shopping list, and so on.

Each prompt file contains:

- **The story**: the problem it solves and what the output looks like (PT + EN)
- **The prompt**: the full text, ready to copy

### How to use

1. Open a prompt from the table above.
2. Copy the text under the `## Prompt` section.
3. Replace placeholders such as your email address (`____`).
4. Adapt it to your life: supermarket, family size, language, dietary preferences.
5. Schedule it with your AI assistant (for example, a Claude scheduled task) with access to the tools it needs (Gmail, web search…).

### Structure

```
prompts-collection/
├── scheduled/          # Prompts meant to run on a schedule
│   ├── weekly_meals.md
│   └── weekly_groceries.md
├── LICENSE
└── README.md
```

### Contributing

Have a prompt that makes your life easier? Open a pull request.

- Put it in a folder that fits its kind (e.g. `scheduled/`), or create a new one.
- Use `snake_case.md` file names.
- Include a short description (ideally in PT and EN) and a `## Prompt` section with the full text.
- Remove personal data (emails, names, addresses) and use placeholders instead.
- Add a row to the table in this README.

---

## 🇵🇹 Português

### O que é isto?

Uma coleção de prompts que uso mesmo. A maioria são **rotinas agendadas**: prompts que correm sozinhos (por exemplo, como tarefa agendada no Claude) e entregam algo útil no meu email: um plano de refeições, uma lista de compras, etc.

Cada ficheiro contém:

- **A história**: o problema que resolve e o aspeto do resultado (PT + EN)
- **O prompt**: o texto completo, pronto a copiar

### Como usar

1. Abre um prompt da tabela acima.
2. Copia o texto na secção `## Prompt`.
3. Substitui os campos a preencher, como o teu email (`____`).
4. Adapta à tua vida: supermercado, tamanho da família, idioma, preferências alimentares.
5. Agenda-o no teu assistente de IA (por exemplo, uma tarefa agendada no Claude) com acesso às ferramentas necessárias (Gmail, pesquisa web…).

### Contribuir

Tens um prompt que te facilita a vida? Abre um pull request.

- Coloca-o numa pasta adequada (ex.: `scheduled/`) ou cria uma nova.
- Usa nomes de ficheiro em `snake_case.md`.
- Inclui uma breve descrição (idealmente em PT e EN) e uma secção `## Prompt` com o texto completo.
- Remove dados pessoais (emails, nomes, moradas) e usa campos a preencher.
- Acrescenta uma linha à tabela deste README.

---

## 📄 License / Licença

[GPL-3.0](LICENSE)
