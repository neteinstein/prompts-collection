# “O que é que falta lá em casa?” (PT)

Fazemos as compras online no Continente quase todas as semanas, e quase todas as semanas a Maria Cortês Ferreira que acaba por fazer isto muito mais vezes que eu 🙈 pergunta a cada um de nós o que falta. 
Nem sempre tenho resposta.

Por isso criei uma rotina com o Claude que corre sozinha todas as sextas às 18h:

1️⃣ Lê as faturas Continente dos últimos 6 meses, diretamente do Gmail

2️⃣ Descobre o ritmo da família: o que compramos em todas as encomendas, o que compramos de 2 em 2 semanas, o que já devia ter voltado ao carrinho

3️⃣ Repara no que não foi entregue da última vez e nos produtos que já não estão na época

4️⃣ Envia um email com a lista organizada por categorias, quantidades e custo estimado

No fim vem uma linha pronta a colar na app Continente Siga (“banana mais sumo de laranja mais azeitonas…”). Toco em “Encomendar online” e está feito.
Na primeira execução analisou 17 encomendas e 876 produtos. O vencedor foi o sumo de laranja, em 16 das 17 encomendas 🍊

Junta-se à [rotina de domingo](weekly_meals.md) que já me sugere as refeições da semana. Uma diz o que cozinhar, a outra diz o que está a acabar.
O prompt completo está nos comentários. 

Copiem, agendem e adaptem ao vosso supermercado.

# “What are we running out of?” (EN)

We do our grocery shopping online almost every week, and almost every week I forgot something.

So I set up a Claude routine that runs on its own every Friday at 6pm:

1️⃣ Reads 6 months of supermarket invoices straight from Gmail

2️⃣ Learns the family’s rhythm: what we buy every order, what we buy every two weeks, what’s overdue

3️⃣ Notices what wasn’t delivered last time and what’s out of season

4️⃣ Emails a list grouped by category, with quantities and an estimated total

At the end there’s one line ready to paste into the supermarket app. One tap on “Order online” and the cart is ready.

It sits next to my Sunday routine that suggests the [week’s meals](weekly_meals.md). One tells me what to cook, the other tells me what’s running low.

Copy it, schedule it, adapt it to your own supermarket. 

Note: This is aimed at Portuguese Supermarket "Continente" but could be easily adapted.

## Prompt

Weekly Continente shopping suggestions — analyse past online orders and email a suggested shopping list.
1. FIND THE ORDERS (Gmail)
- Search Gmail for: from:ajuda@continente.pt subject:"Informação sobre a sua encomenda - Envio de Fatura"
- There are ~120 of these. Use the last 6 months of orders (roughly 25–30 emails) for the pattern; fetch each with get_thread using messageFormat PLAIN_TEXT. Note each order's date (the email date).
- Each email body contains a markdown-like table: "| ## <Product name> <Brand> emb. <size> | <Qtd> | <Preço> | <Desconto> | ... |". Quantity is either "N Un" or a weight like "0.98 kg". The PDF invoice attachment is not needed.
- The table has two sections: "Produtos com Alterações" (items that were unavailable / not delivered or substituted) and "Restantes Produtos" (delivered). Count both as "wanted" for pattern purposes, but note items that repeatedly appear under "Produtos com Alterações" (often unavailable).
- Save the parsed line items (order date, product, brand, size, qty, unit, price, discount) to a CSV in the working directory and do the analysis in Python, not by eyeballing.
2. FIND THE PATTERN
- Normalise product names (same product across orders = same item; ignore minor text variations).
- For each product compute: number of orders it appeared in, frequency (e.g. every order / every ~2 weeks / monthly), typical quantity, average price paid, days since last bought.
- Note seasonal items (e.g. castanhas, dióspiros, specific fruit) and only suggest them if they're in season now.
- Detect the household's order rhythm (how often they order) to judge what is "due".
3. BUILD THE SUGGESTION
- Suggest items that are DUE: staples bought in most orders, plus recurring items whose usual interval since the last purchase has passed. Skip items bought in the most recent order unless they are bought every single order (e.g. fruit, milk, yogurts).
- Suggest a quantity for each (typical quantity).
- Optionally add a small "Talvez também" section with 3–6 occasional items worth considering (bought before, not recently).
- Estimate the total cost from average prices.
4. GROUP BY TYPE — use these categories (only those with items), each with an emoji:
🍎 Fruta | 🥦 Legumes e Verduras | 🥩 Carne | 🐟 Peixe e Marisco | 🧀 Laticínios e Ovos | 🥓 Charcutaria | 🍝 Mercearia (massas, arroz, molhos, óleos, conservas) | 🍪 Snacks, Bolachas e Pequeno-almoço | 👶 Bebé e Criança (saquetas de fruta, etc.) | 🍱 Refeições Prontas | 🧃 Bebidas | 🧊 Congelados | 🧻 Casa e Limpeza | 🧴 Higiene
5. THE EMAIL — in European Portuguese (pt-PT), HTML, beautiful
- Send with Gmail send_message to ____
- Subject: "🛒 Lista de compras sugerida — semana de <data>"
- Design: email-safe HTML (tables + inline CSS, max-width ~640px, centred). Header banner in Continente red (#E30613) with white title and a subtitle with the date and how many orders were analysed. Each category as a rounded card with a coloured header (emoji + category name + item count). Each item row: product name (bold), brand/size in small grey text, suggested quantity as a pill/badge, average price on the right, and a small tag like "Todas as encomendas", "A cada ~2 semanas", "Há 3 semanas sem comprar", or "⚠️ Muitas vezes indisponível". Alternating subtle row backgrounds, generous padding, system font stack.
- A summary box near the top: number of items suggested, estimated total (€), top 3 most-bought products, and the family's usual order frequency.
- "Talvez também" section in a softer style.
- At the end, a box with the whole list as a single line joined by the Portuguese word " mais " (e.g. "banana mais iogurte grego mais ovos de ar livre mais ..."), using short generic product names, with instructions: open the Continente Siga app → Listas de compras → add multiple items via text → paste the line (the app splits on "mais") → tap "Encomendar online" to turn the list into a cart.
- Footer: small grey text "Gerado automaticamente a partir das faturas Continente."
- Do not use images that need external hosting other than emoji.
6. If no Continente order emails are found, send a short email saying so instead of a list. Don't ask questions — this runs unattended.
