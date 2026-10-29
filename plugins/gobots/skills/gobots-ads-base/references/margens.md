# Margens por grupo de produto

O MCP não sabe a margem do lojista, e sem margem o ROAS objetivo é chute. Este arquivo é preenchido uma vez por lojista (na instalação ou na primeira conversa) e lido sempre que uma decisão depender da margem: ROAS objetivo, orçamento de campanha nova, julgar se um ROAS real é lucro ou prejuízo.

Quando uma skill precisar da margem de um grupo que não está aqui, ela pergunta ao lojista e pede para registrar abaixo. Nunca assume um valor.

## Como preencher

- **Grupo**: um conjunto de produtos com margem parecida. Pode ser por categoria, marca, aro, linha, ou pelo papel do produto na loja (defesa, expansão, teste). O critério é do lojista.
- **Margem de contribuição (%)**: preço de venda menos custo do produto, tarifa do marketplace, frete pago pelo vendedor e descontos, dividido pelo preço. Antes de qualquer gasto com Ads.
- **Margem a preservar (%)**: quanto o lojista quer que sobre depois do Ads. Padrão: 10 pontos, ou um terço da margem, o que for menor.
- **ROAS de equilíbrio** e **ROAS objetivo** são calculados: 1 ÷ margem e 1 ÷ (margem − preservar).

## Tabela (modelo)

| Grupo | Como identificar (categoria, marca, palavra no título) | Margem de contribuição | Margem a preservar | ROAS de equilíbrio | ROAS objetivo | Papel (defesa / expansão / teste) |
|---|---|---|---|---|---|---|
| exemplo: Linha A | categoria X, marca Y | 25% | 10% | 4,0x | 6,7x | defesa |
| exemplo: Linha B | título contém "kit" | 12% | 5% | 8,3x | 14,3x | expansão |

Linhas de exemplo devem ser apagadas ao preencher.

## Observações do lojista

Espaço livre para regras próprias: produtos proibidos em Ads, SKUs em saída de linha, tetos de ROAS que a IA não pode cruzar, sazonalidades.
