# GoBots Ads

Plugin do Claude para lojistas do Mercado Livre que usam a GoBots. Ele conecta o Claude ao MCP GoBots e traz duas skills de Product Ads.

## O que vem no plugin

| Componente | O que faz |
|---|---|
| MCP `gobots` | Servidor `https://open-api.live.gobots.com.br/mcp`: lojas, campanhas, adgroups, relatórios, catálogo, promoções, recomendações e métricas de atendimento da conta do lojista. |
| Skill `ads-diagnostico` | Lê a conta e responde "como está": placar de 30 dias da loja, campanhas travadas por orçamento ou por rank, catálogo e promoções de um item, e atendimento da IA contra o do vendedor. Nunca altera nada. |
| Skill `gobots-ads-base` | Base de conhecimento compartilhada: glossário, régua de decisão, receitas de chamada do MCP, guardrails de escrita, formato de resposta e margens por grupo de produto. |

## Configuração

1. Crie uma chave de API no painel GoBots ([Primeiros passos](https://developers.gobots.com.br/guias/primeiros-passos/)).
2. Instale o plugin: `/plugin marketplace add gobots-ai/claude-merchant-plugins` e depois `/plugin install gobots-ads@gobots`. No Claude Code, rode `/mcp`, escolha `gobots` e faça o login: a tela de autorização da GoBots pede a chave de API.
3. Pergunte, por exemplo: "como estão minhas campanhas?" ou "meu ROAS está bom?".

O acesso dura 1 hora e renova sozinho por até 30 dias. Revogar a chave no painel desconecta o Claude na hora.

## Segurança

As ferramentas de escrita do MCP pedem confirmação antes de mudar algo no Mercado Livre. A skill `ads-diagnostico` só chama ferramentas de leitura.

## Links

- Documentação: https://developers.gobots.com.br/guias/assistente-de-ia/
- Política de privacidade: https://gobots.com.br/politica-de-privacidade
