# GoBots

Plugin oficial da GoBots para o Claude. Ele conecta o Claude à sua conta GoBots pelo MCP GoBots e traz skills que sabem usar esses dados como um especialista em Mercado Livre.

## O que vem no plugin

| Componente | O que faz |
|---|---|
| MCP `gobots` | Servidor `https://open-api.live.gobots.com.br/mcp` com as ferramentas da GoBots: lojas, Product Ads (campanhas, adgroups, desempenho, relatórios), itens, competição de catálogo, promoções, recomendações GoBots e métricas de atendimento da IA e do vendedor. |
| Skill `ads-diagnostico` | Lê a conta e responde "como está": placar de 30 dias da loja, campanhas travadas por orçamento ou por rank, catálogo e promoções de um item, e atendimento da IA contra o do vendedor. Nunca altera nada. |
| Skill `gobots-ads-base` | Base de conhecimento compartilhada: glossário, régua de decisão, receitas de chamada do MCP, guardrails de escrita, formato de resposta e margens por grupo de produto. |

## Instalação

No Claude Code:

```sh
/plugin marketplace add gobots-ai/claude-merchant-plugins
/plugin install gobots@gobots
```

## Configuração

1. Crie uma chave de API no painel GoBots ([Primeiros passos](https://developers.gobots.com.br/guias/primeiros-passos/)).
2. No Claude Code, rode `/mcp`, escolha `gobots` e faça o login: a tela de autorização da GoBots pede a chave de API.
3. Pergunte, por exemplo: "como estão minhas campanhas?", "esse anúncio ganha o catálogo?" ou "a IA está respondendo rápido?".

O acesso dura 1 hora e renova sozinho por até 30 dias. Revogar a chave no painel desconecta o Claude na hora.

## Segurança

As ferramentas de escrita do MCP pedem confirmação antes de mudar algo no Mercado Livre. A skill `ads-diagnostico` só chama ferramentas de leitura.

## Links

- Documentação: https://developers.gobots.com.br/guias/assistente-de-ia/
- Política de privacidade: https://gobots.com.br/politica-de-privacidade
