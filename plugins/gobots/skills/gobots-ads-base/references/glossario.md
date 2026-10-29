# Glossário do Product Ads (Mercado Livre) para as skills GoBots

Use estas definições ao explicar números ao lojista. Elas seguem a documentação de desenvolvedores do Mercado Livre e o gerenciador de publicidade; onde o MCP usa um nome diferente, o nome do MCP está entre parênteses.

## Estrutura

- **Campanha**: conjunto de adgroups com o mesmo orçamento diário, a mesma estratégia e o mesmo ROAS objetivo. Tem status active, paused ou ended (ended não volta).
- **Adgroup** (`ad_group_id`): a unidade que carrega os anúncios. Tipos: ITEM (um anúncio), CATALOG (todas as variantes de um produto de catálogo) e FAMILY (todas as variantes de uma família). **Pausar, ativar e mover agem no adgroup inteiro**, nunca num anúncio isolado. Um adgroup pode estar ativo e sem nenhum anúncio dentro; nesse caso o MCP responde not_found ao listar os anúncios.
- **Anúncio** (`item_id`, MLB…): a variante. Tem métricas próprias, mas só de leitura.
- **Anunciante** (`advertiser_id`): a conta de Ads de uma loja. Uma loja sem anunciante não tem Ads e derruba chamadas que somam a conta inteira.

## Estratégias

- **Rentabilidade** (profitability): produtos que já vendem e já aparecem bem; prioriza retorno.
- **Crescimento** (increase): produtos de margem média que precisam de tráfego; aceita retorno menor por volume.
- **Visibilidade** (visibility): lançamentos; o objetivo é gerar dados e avaliações.

## Alvo e retorno

- **ROAS objetivo** (`roas_target`): a meta de retorno que orienta o lance do algoritmo. É o alvo oficial da campanha desde dezembro de 2025, quando substituiu o `acos_target`. Objetivo maior = lance mais seletivo = menos volume. Faixa aceita pelo MCP: 1,0 a 35,0.
- **ACOS objetivo** (`acos_target`): o mesmo alvo visto como custo: ACOS = 1 ÷ ROAS. ROAS 20x é ACOS 5%.
- **ROAS real**: vendas atribuídas ÷ gasto, no período.
- **ACOS real**: gasto ÷ vendas atribuídas.
- **ROAS de equilíbrio**: 1 ÷ margem de contribuição. Abaixo dele cada venda por anúncio dá prejuízo.
- **TACOS** (derivado pela GoBots): gasto ÷ (vendas atribuídas + vendas orgânicas). Mede o peso do Ads sobre tudo o que a loja vendeu. ACOS subindo com TACOS caindo pode ser Ads puxando orgânico.

## Orçamento

- **Orçamento diário** (`budget_amount`): uma média. Num dia o gasto pode chegar ao dobro; o teto do mês é a soma dos diários. Ao esgotar, a campanha sai dos leilões até o dia seguinte.
- **Teto batido**: dia em que o gasto chegou ao orçamento. Três dias seguidos no teto é o sinal mínimo para falar em aumento.
- **Última alteração** (`updated_at` da campanha): quando orçamento, alvo ou status mudaram pela última vez. Orçamento alterado no meio da janela invalida a leitura dos 30 dias.

## Impressões e perdas (só no relatório semanal)

- **Impression share**: fração das impressões elegíveis que a campanha levou.
- **Top impression share**: fração em que apareceu nas primeiras posições.
- **Perda por orçamento** (`lost_impression_budget`): impressões que não aconteceram por falta de verba. Alavanca: orçamento.
- **Perda por rank** (`lost_impression_rank`): impressões perdidas porque o anúncio não ganhou o leilão. Alavanca: qualidade do anúncio ou ROAS objetivo menor.
- As duas perdas não somam 100% com a impression share; impressões inelegíveis ficam de fora.

## Vendas

- **Direta**: o comprador clicou e comprou o produto anunciado.
- **Indireta**: clicou e comprou outro produto da loja.
- **Atribuída**: direta + indireta, dentro da janela.
- **Orgânica**: do mesmo anúncio, sem clique pago.
- **ads_sales_share**: vendas via Ads ÷ vendas totais do anúncio. Não é share of voice.
- **Janela de atribuição**: 14 dias após o clique. A maior parte cai nos 7 primeiros.
- **Período de aprendizado**: até 30 dias para campanha nova. Julgar antes disso é julgar ruído.

## Métricas de funil

- **Impressões**, **cliques**, **CTR** (cliques ÷ impressões), **CPC** (gasto ÷ cliques), **CVR** (unidades ÷ cliques).
- **Gasto excedente** de um adgroup: gasto − receita × ACOS alvo. É o critério de ranqueamento para pausa, melhor que ACOS puro porque pondera pelo tamanho.

## Catálogo e promoções

- **Buy box**: a oferta principal de um produto de catálogo; leva a maior parte das vendas.
- **Preço para ganhar** (`price_to_win`): quanto precisaria custar para tomar o buy box.
- **Boosts**: fulfillment, parcelamento sem juros, frete grátis, retirada, envio no mesmo dia. Cada um com status boosted, not_boosted, opportunity ou not_apply.
- **Preço desalinhado**: item com preço acima da referência do Meli. Sai das ferramentas de impulsionamento, Product Ads incluído.
- **Promoção candidata**: promoção em que o item pode entrar, com preço sugerido e a divisão do desconto entre Meli (`meli_percentage`) e vendedor (`seller_percentage`).

## Atendimento (escopos do MCP)

- **PRE_SALE/PRODUCT**: perguntas em anúncios. **AFTER_SALE/ORDER**: mensagens pós-venda. **AFTER_SALE/TICKET**: reclamações.
- **engaged.gobots.bot** e **engaged.seller**: quem respondeu. **response_time**: segundos até a primeira resposta. pendentes + resolvidas = total, sempre.
