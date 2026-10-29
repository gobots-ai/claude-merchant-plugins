# Receitas de chamada do MCP GoBots

O MCP GoBots expõe 18 ferramentas de leitura e 7 de escrita, todas restritas ao lojista dono da credencial. Os ids de loja são opacos e vêm de `list_stores`; nenhum outro identificador é aceito. As receitas abaixo evitam os três problemas vistos em teste: chamadas que caem, saídas que estouram e dados mal interpretados.

## Sempre

1. **Chame `list_stores` primeiro** e guarde os ids. Toda chamada que aceita `stores` ou `store_id` deve recebê-los.
2. **Nunca faça chamada "conta inteira"** (`list_items`, `get_ads_performance`, `get_metrics` sem loja) enquanto a conta tiver uma loja sem anunciante de Ads: ela derruba a chamada com `source_unavailable`. Confira em `list_ad_advertisers` quais lojas têm anunciante e itere loja a loja.
3. **Repita uma vez** quando a resposta vier com `source_unavailable` ou `meta.status: "partial"` (aviso `ads_source_partial`). Em teste, todas as quedas resolveram na segunda tentativa. Se persistir, diga ao lojista que a fonte está instável e qual leitura ficou faltando.
4. **Página vazia com `partial` não é prova de ausência.** Com `in_campaign` definido, uma falha na consulta de Ads esvazia a página inteira.
5. **Limite a saída.** `list_ad_groups` em campanha com mais de 100 adgroups e `get_ad_report_products` estouram o limite de resposta. Use `limit` 30 a 50 com `sort_by: "spend"` e pagine com `cursor` só quando precisar do resto.
6. **Confira a data da última alteração** (`updated_at` em `list_ad_campaigns` ou `get_ad_campaign`) antes de qualquer conclusão sobre orçamento. Orçamentos mudam por fora, inclusive mais de uma vez na mesma semana.

## Leituras por objetivo

| Quero | Chame | Observações |
|---|---|---|
| Lojas e anunciantes | `list_stores`; `list_ad_advertisers` | anunciante por loja; loja sem anunciante não tem Ads |
| Visão de 30 dias de uma loja | `get_ads_performance` com `store_id`, `period: "last_30_days"`, `granularity: "total"` | traz atribuídas, orgânicas, TACOS |
| Gasto e ACOS por dia | `get_ads_performance` com `campaign_id` (ou `store_id`), `period: "last_7_days"`, `granularity: "day"` | o dia de hoje vem parcial |
| Campanhas com orçamento e alvo | `list_ad_campaigns` com `stores` e `status` | a métrica embutida é só do último dia; `updated_at` mostra a última alteração |
| Uma campanha completa | `get_ad_campaign` | mesmo conteúdo, para conferir antes de recomendar |
| Perdas por orçamento e por rank | `list_ad_reports` (data da última execução) → `get_ad_report_campaigns` com `date` e `store_id` | relatório semanal; a janela cobre cerca de 30 dias |
| Produto a produto no relatório | `get_ad_report_products` | trunca em algumas centenas de linhas; pagine por cursor |
| Adgroups com métricas | `list_ad_groups` com `campaign_id`, `period: "last_30_days"`, `sort_by: "spend"`, `limit: 30` | status active, unavailable (hold), removed |
| Anúncios de um adgroup | `get_ad_group_ads` com `campaign_id`, `ad_group_id`, `period` | adgroup sem anúncio responde `not_found`; as métricas do adgroup podem incluir anúncios que já saíram |
| Itens fora de campanha | `list_items` com `stores`, `in_campaign: false`, `sort: "sales_desc"` | `sold_quantity` é acumulado de vida, não de período; não existe venda recente por item |
| Buy box e boosts | `get_item_competition` com até 10 `item_ids` por vez | um pedido por item ao Meli; lento |
| Promoções de um item | `get_item_promotions` com até 10 `item_ids` | a mais lenta do MCP; a lista da loja (`list_promotions`) é incompleta por natureza |
| Recomendações GoBots | `list_opportunities` com `stores`, `detail: "full"`; `get_opportunity` | `action: null` em lançamento = não aplicável pelo MCP |
| Atendimento | `describe_metrics` → `get_metrics` com `stores`, `scopes`, `period`, `timezone: "America/Sao_Paulo"` | sempre por loja e escopo |

## Escritas (ver `guardrails.md` antes)

| Ferramenta | O que faz | Exige |
|---|---|---|
| `create_ad_campaign` | cria campanha pausada e vazia | `name`, `budget_amount`, `strategy`, `roas_target`, `channel`, `advertiser_id` em conta com várias lojas, `idempotency_key` |
| `update_ad_campaign` | nome, status, orçamento, ROAS objetivo, estratégia | `campaign_id`, pelo menos um campo, `idempotency_key` |
| `set_ad_group_status` | pausa ou ativa adgroups (até 50) | `apply_to_all_variants: true` em CATALOG/FAMILY; `item_ids` só para pausar |
| `move_ad_groups` | move adgroups entre campanhas do mesmo anunciante | destino diferente da origem; `apply_to_all_variants` |
| `apply_opportunity` / `apply_opportunities` | aplica recomendação como proposta (até 20 no lote) | `idempotency_key` |
| `dismiss_opportunity` | descarta (irreversível), favorita, oculta, comenta | **grava na hora, sem confirmação** |

## Lacunas conhecidas (não tente contornar com gambiarra; explique ao lojista)

1. Não existe ferramenta para anexar item a campanha. `create_ad_campaign` nasce vazia; só `move_ad_groups` leva adgroups de uma campanha a outra.
2. Loja sem anunciante derruba chamadas conta inteira.
3. `list_items` em loja sem Ads devolve página vazia em vez de itens com `advertised: null`.
4. `get_ad_report_products` trunca e exige paginação.
5. Métricas de adgroup e de anúncio divergem quando anúncios saíram do adgroup.
6. `get_ad_group_ads` responde `not_found` para adgroup ativo sem anúncio.
7. Margem não existe no MCP (por isso `margens.md`).
8. `list_items` não aceita período; não há venda recente por item fora do Ads.
