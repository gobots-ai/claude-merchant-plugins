---
name: ads-diagnostico
description: Diagnóstico de leitura da conta de Product Ads do lojista no Mercado Livre pelo MCP GoBots, sem alterar nada. Use sempre que o lojista perguntar como está o Ads, o resultado da loja, o que mudou, se uma campanha está travada por verba ou por rank, se vale a pena olhar algum adgroup, se um item ganha o catálogo ou em que promoção pode entrar, ou quantas perguntas e mensagens a IA respondeu e em quanto tempo. Acione mesmo que ele diga só "dá uma olhada na minha conta", "como estão minhas campanhas", "meu ROAS está bom?", "esse anúncio está bem?" ou "o atendimento está dando conta?". Não use para executar mudanças, porque pausar, ajustar orçamento ou aplicar recomendação é trabalho da ads-otimizar.
---

# ads-diagnostico

Esta skill responde "como está" e aponta "o que olhar". Ela só lê. Quando o diagnóstico pedir uma ação, ela nomeia a seção da `ads-otimizar` que resolve e para por aí. Essa separação é o que permite ao lojista confiar na pergunta: nada muda na conta porque ele perguntou.

Antes de começar, leia da base `gobots-ads-base`:
- `references/receitas-mcp.md` (como chamar o MCP sem cair nem estourar),
- `references/formato-saida.md` (o placar e o bloco de recomendação),
- `references/glossario.md` quando for explicar um termo.

## Três seções, acionadas pela pergunta

Identifique qual seção a pergunta pede. Uma pergunta ampla ("como está minha conta?") pede a seção 1; só entre nas outras se o lojista perguntar por item, promoção ou atendimento.

### 1. Ads: a loja em 30 dias

1. `list_stores`. Se o lojista não disse a loja e há mais de uma, pergunte qual, ou rode uma por uma. Nunca some a conta inteira (ver receitas).
2. `get_ads_performance` da loja, `last_30_days`, `granularity: "total"`: investimento, vendas atribuídas, ROAS, ACOS, unidades via Ads e orgânicas, TACOS.
3. `get_ads_performance` da loja, `last_7_days`, `granularity: "day"`: a tendência da semana e o ACOS dia a dia.
4. `list_ad_campaigns` da loja, status active: orçamento diário, ROAS objetivo e `updated_at`. Anote campanhas cujo orçamento mudou nos últimos 7 dias.
5. `list_ad_reports` da loja → `get_ad_report_campaigns` na data mais recente: impression share, perda por orçamento e por rank, ROAS do relatório. Se houver uma execução anterior, leia também e compare.
6. Para as 3 campanhas de maior gasto: `list_ad_groups` com `period: "last_30_days"`, `sort_by: "spend"`, `limit: 30`. Calcule gasto excedente (gasto − receita × ACOS alvo da campanha) e separe adgroups com gasto e zero vendas.
7. Para campanhas que gastam o teto: `get_ads_performance` com `campaign_id`, `last_7_days`, por dia, para ver se o ACOS nos dias de teto está subindo.

Monte o placar do `formato-saida.md`. Depois, a lista **O que olhar**, no máximo 5 itens, do maior para o menor impacto em reais, cada um com o encaminhamento:

- campanha no teto com ACOS marginal subindo → `ads-otimizar`, seção orçamento e alvo (resposta provável: esperar);
- campanha no teto com ACOS marginal abaixo do alvo e perda por orçamento → `ads-otimizar`, seção orçamento e alvo (candidata a +20 a 30%);
- adgroups com gasto e zero vendas, ou excedente alto → `ads-otimizar`, seção higiene;
- campanha com orçamento reservado e nenhum adgroup ativo → `ads-otimizar`, seção higiene;
- perda por rank dominante → explicar que a alavanca é anúncio ou alvo; não encaminhar aumento de verba;
- recomendações abertas no painel (`list_opportunities`) → `ads-otimizar`, seção recomendações.

Diga o que não foi possível ler (fonte instável, loja sem anunciante) em vez de estimar.

### 2. Item: catálogo e promoções

Quando o lojista perguntar por um item ou um grupo de itens:

1. Se vier título e não id, localize o `item_id` com `list_items` da loja (ordenado por vendas) e confirme com o lojista quando houver mais de um candidato.
2. `get_item_competition` com até 10 ids por chamada: status (winning, competing, sharing_first_place, listed, not_listed), preço atual e preço para ganhar, motivo da perda, quem está ganhando e a que preço, boosts em aberto.
3. `get_item_promotions` com os mesmos ids: promoções candidatas e ativas, preço sugerido, quem paga o desconto (Meli e vendedor), datas.
4. Responda por item: está pronto para Ads ou não, e o motivo. Alerte de forma explícita quando o preço estiver desalinhado, porque isso tira o anúncio do Product Ads.

Item fora de catálogo (`not_listed`, `item_not_opted_in`) não tem buy box para disputar; diga isso em vez de dizer que "perde".

### 3. Atendimento: quem respondeu e em quanto tempo

1. `describe_metrics` uma vez para saber os escopos e métricas disponíveis.
2. `get_metrics` com `stores` da loja, `scopes` pedidos (pré-venda por padrão), `period` (7 dias por padrão), `granularity: "total"`, `timezone: "America/Sao_Paulo"`.
3. Responda: total, respondidas, pendentes, parte da IA e parte do vendedor, e o tempo de resposta da IA contra o do vendedor. A comparação de tempos é o número que o lojista entende de primeira; mostre os dois lado a lado.

## Regras desta skill

- **Nunca chame ferramenta de escrita.** Se o lojista pedir "e pausa isso", explique que a `ads-otimizar` faz com confirmação e ofereça seguir para ela.
- **Sempre por loja.** Chamada conta inteira cai quando há loja sem anunciante.
- **Repita uma vez** em `source_unavailable` ou `partial`; se persistir, registre a lacuna na resposta.
- **`sold_quantity` é acumulado de vida.** Nunca apresente como venda recente, e diga isso quando listar best-sellers.
- **Métricas da lista de campanhas são do último dia.** Para 30 dias use `get_ads_performance` e o relatório semanal.
- **Não compare com outras contas** nem invente benchmark. Os números do lojista se comparam com a semana anterior dele e com os alvos dele.
- **Orçamento alterado nos últimos 7 dias** aparece sempre no placar, porque muda a leitura de tudo o mais.

## Exemplo de "O que olhar"

Entrada: uma campanha gasta o teto de R$ 3.000 todos os dias, perde 37% das impressões por orçamento, e o ACOS nos dias de teto foi de 3,2% para 5,1% com alvo de 5,6%; o orçamento subiu há 4 dias.

Saída:
1. **Campanha X no teto, ACOS marginal encostando no alvo.** Orçamento alterado há 4 dias; esperar 7 dias antes de nova mudança → ads-otimizar, orçamento e alvo.
2. **5 adgroups da campanha X com R$ 470 de gasto excedente e zero vendas**, 4 deles sem anúncio dentro → ads-otimizar, higiene.
