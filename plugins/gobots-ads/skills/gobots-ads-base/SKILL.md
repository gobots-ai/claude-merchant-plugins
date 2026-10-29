---
name: gobots-ads-base
description: Base de conhecimento compartilhada das skills de Product Ads da GoBots (ads-diagnostico, ads-otimizar, ads-estruturar). Não tem fluxo próprio. Leia as referências daqui quando uma dessas skills mandar, ou quando o usuário perguntar o que é ROAS objetivo, ACOS, impression share, perda por orçamento ou por rank, adgroup, janela de atribuição, ou como escolher o ROAS pela margem, sem pedir nenhuma ação na conta.
---

# gobots-ads-base

Esta pasta guarda o que as três skills de uso do MCP GoBots precisam saber e não querem repetir: o vocabulário do Product Ads do Mercado Livre, a régua de decisão, como chamar o MCP sem estourar ou cair, os guardrails de escrita, o formato de resposta e a margem por grupo de produto de cada lojista.

Ela existe para que a mesma régua valha no diagnóstico, na otimização e na reestruturação. Quando uma delas mudar um limiar, muda aqui, uma vez.

## Referências

| Arquivo | Leia quando |
|---|---|
| `references/glossario.md` | precisar explicar um termo ao lojista, ou antes de interpretar um relatório |
| `references/regua-de-decisao.md` | for decidir pausar, escalar, subir orçamento, mexer no ROAS objetivo ou julgar uma recomendação |
| `references/receitas-mcp.md` | antes de qualquer chamada ao MCP: filtros obrigatórios, limites, paginação e o que fazer quando a fonte falha |
| `references/guardrails.md` | antes de qualquer ferramenta de escrita, e para saber o que nunca fazer por conta própria |
| `references/formato-saida.md` | ao montar a resposta final de um diagnóstico ou de uma recomendação |
| `references/margens.md` | quando a decisão depender da margem do lojista (ROAS objetivo, orçamento de campanha nova) |

## Como as skills de uso usam esta base

- `ads-diagnostico` lê glossário, receitas e formato. Nunca escreve.
- `ads-otimizar` lê tudo, em especial régua, guardrails e margens. Escreve só depois do portão de confirmação descrito em `guardrails.md`.
- `ads-estruturar` lê tudo e ainda depende de lacunas do MCP listadas em `receitas-mcp.md`.

Se o usuário só quer entender um conceito, responda com o glossário e pare. Não puxe dados da conta sem ele pedir.
