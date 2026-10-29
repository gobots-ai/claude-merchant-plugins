# Régua de decisão

Os limiares abaixo são o ponto de partida, tirados do consenso de guias de Product Ads e da própria documentação do Mercado Livre. Se o motor de recomendações da GoBots usar outros valores, os da GoBots valem e estes devem ser atualizados aqui.

A régua existe porque o lojista costuma errar em três direções previsíveis: subir verba em campanha que já não converte, pausar cedo demais, e mexer em várias coisas ao mesmo tempo. Cada regra abaixo fecha uma dessas portas.

## 1. ROAS objetivo pela margem

- Margem de contribuição antes de Ads = preço − custo − tarifa − frete − descontos.
- ROAS de equilíbrio = 1 ÷ margem.
- ROAS objetivo = 1 ÷ (margem − margem que se quer preservar). Exemplo: margem 30% preservando 10% → equilíbrio 3,3x, objetivo 5x. Equivale a "equilíbrio com cerca de 20% de folga".
- Calcule por grupo de produto, nunca pela conta inteira. Margens misturadas escondem o produto que dá prejuízo.
- A margem vem de `margens.md`. Se não estiver lá, pergunte ao lojista antes de propor um número; nunca chute.

## 2. Orçamento: subir, segurar ou esperar

Responda estas perguntas em ordem. A primeira que der "sim" decide.

1. **O orçamento mudou há menos de 7 dias?** Sim → esperar. A leitura dos 30 dias está contaminada; use só os dias após a mudança.
2. **A campanha gasta o teto todos os dias (3 dias seguidos no mínimo)?** Não → subir não resolve. Olhe estoque, preço, itens ativos e ROAS objetivo.
3. **A perda maior é por rank, não por orçamento?** Sim → a alavanca é qualidade do anúncio ou ROAS objetivo menor. Só a pedido explícito do lojista, nunca por iniciativa.
4. **O ACOS dos dias em que bateu o teto está abaixo do alvo?** Sim → propor +20% a +30%, reavaliar em 3 a 4 dias. Não → esperar: mais verba estaria comprando clique, não venda.

"Esperar" é uma resposta válida e frequente. Uma skill que só sabe aumentar orçamento é uma máquina de queimar verba.

Use o ACOS marginal (dos dias no teto), não a média de 30 dias. A média esconde o retorno decrescente.

## 3. Pausar adgroups

Candidato a pausa é o adgroup, inteiro, que:
- tem 80 a 100 cliques ou mais em 30 dias e zero vendas atribuídas; ou
- tem ACOS consistentemente acima do ACOS de equilíbrio do grupo; ou
- tem ROAS muito abaixo do objetivo com gasto relevante (ROAS abaixo de 5x quando o objetivo é 15x ou mais).

Ranqueie por gasto excedente (gasto − receita × ACOS alvo), não por ACOS. Um adgroup com ACOS 25% e R$ 50 pesa menos que um com ACOS 15% e R$ 2.000.

Não pause:
- adgroup com ROAS ainda alto em absoluto (entre 7x e 12x acima do alvo, mas rentável): vai para "conversar com o lojista";
- adgroup misto, com um anúncio dentro do alvo e outro fora: a ação é separar, não pausar;
- adgroup cujo item vende bem no orgânico e nunca converteu via Ads sem antes olhar preço, foto e frete (o problema pode ser a oferta, não o anúncio).

Adgroup ativo sem anúncio dentro: pausar é higiene, não economia. Diga isso ao lojista.

## 4. Escalar

- ACOS abaixo do alvo com pelo menos 50 cliques, ou conversão alta com volume baixo (a verba limita).
- Aumente 20% a 30% por vez. Reverta se o ACOS subir 30% a 40% em relação ao período anterior.
- Adgroups de ROAS muito alto presos no teto de uma campanha grande escalam melhor em campanha própria (ads-estruturar), não por aumento geral da campanha.

## 5. Recomendações do motor GoBots

Antes de aplicar qualquer uma, confira com dado vivo:
- **Aumento de orçamento**: o orçamento atual já é maior ou igual ao proposto? → obsoleta. Mudou há menos de 7 dias? → esperar. Caso contrário, passe pela régua 2.
- **Pausa de anúncio**: o MCP aplica como pausa do adgroup. Passe pela régua 3.
- **Redução de ROAS objetivo**: nunca aplique por iniciativa própria. Explique a alavanca e deixe o lojista decidir.
- **Lançamento de campanha**: o MCP não anexa itens; explique a recomendação, não a aplique.

Classifique cada uma em aplicar, esperar (favoritar) ou obsoleta. Descarte é irreversível e só a pedido explícito.

## 6. Ritmo

- Uma mudança por vez: ou orçamento, ou objetivo, ou produtos.
- 7 a 14 dias antes de julgar qualquer mudança; 30 dias para campanha nova.
- Registre data, hipótese e resultado esperado em cada mudança, para a próxima leitura ter contra o que comparar.
- Antes de datas de pico, verba extra só em campanha que já bate a meta e perde por orçamento. Nada de mudança estrutural na semana do evento.
