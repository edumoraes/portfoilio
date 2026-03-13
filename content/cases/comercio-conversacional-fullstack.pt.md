---
title: Comércio conversacional fullstack com IA, checkout guiado e operação em tempo real
description: Solução fullstack para vender via conversa, combinar catálogo, atendimento automatizado, checkout controlado e acompanhamento em tempo real sem perder o controle da operação.
weight: 1
case:
  index: Case 01
  eyebrow: Solução fullstack
  summary: "Uma operação de venda por conversa só escala quando IA, regras de negócio e acompanhamento humano convivem sem atrito. Este case combina interface web, backend transacional, busca de catálogo, estado conversacional e pagamento em um fluxo único, feito para uso real."
  stack: "Next.js • FastAPI • PostgreSQL • Redis • Elasticsearch • LangGraph • WebSockets • WhatsApp"
  scope:
    - atendimento conversacional
    - catálogo e descoberta de produto
    - checkout determinístico
    - pagamentos e status de pedido
    - painel operacional em tempo real
  results:
    - 90% de redução no transbordo do atendimento de IA para humano
    - mais de 300 conversas gerenciadas nos primeiros 15 dias
    - R$ 8 mil em pedidos nos primeiros 15 dias
---
## Contexto

O objetivo era transformar um canal de conversa em uma operação comercial de verdade. Isso significava sair do padrão "chatbot que responde perguntas" e construir um sistema que entendesse intenção, consultasse catálogo, mantivesse contexto, criasse sacola, persistisse cliente, gerasse pedido, acompanhasse pagamento e ainda permitisse intervenção humana quando necessário.

Na prática, o problema não era só responder bem. Era manter consistência entre conversa, estado transacional e acompanhamento operacional.

## O problema

Em comércio conversacional, a parte mais perigosa não é a primeira resposta do agente. O risco real aparece quando a conversa sai do terreno aberto e entra em decisões que precisam de ordem rígida: confirmar itens, coletar dados do cliente, definir entrega, persistir registros e fechar pagamento.

Uma solução ingênua, baseada apenas em prompting, tende a falhar exatamente onde o negócio não pode falhar. Ela perde o estado do checkout, mistura intenção com execução e dificulta tanto auditoria quanto handoff humano. O desafio aqui foi separar o que podia continuar probabilístico do que precisava ser determinístico.

## Arquitetura e decisões

A solução foi desenhada como um sistema fullstack, com uma superfície web em Next.js e um backend operacional em FastAPI. No backend, a modelagem não foi organizada em torno de mensagens apenas, mas em torno das entidades reais da operação: conversas, clientes, carrinhos, pedidos, pagamentos e eventos de acompanhamento.

O fluxo conversacional foi dividido em duas camadas. A primeira continua flexível: triagem de intenção, descoberta de produto, dúvidas sobre programa de fidelidade, informações de loja e resposta geral. A segunda é rígida: quando a conversa entra em checkout, o fluxo passa a ser controlado por um grafo com etapas explícitas, validando dados e avançando apenas quando os pré-requisitos são atendidos.

Esse desenho aparece com clareza na combinação entre LangGraph e o orquestrador de checkout. O agente continua natural fora do fechamento do pedido, mas o momento transacional ganha ordem, rastreabilidade e previsibilidade. Isso reduz erro operacional sem matar a fluidez da conversa.

Também foi necessário tratar o catálogo como problema de recuperação, não só de geração. A busca usa Elasticsearch para lidar com texto livre, variação de termos e descoberta orientada por intenção. Em vez de pedir para o modelo "lembrar" produtos, a arquitetura força a consulta ao catálogo antes da recomendação.

## Como a tecnologia resolve

O FastAPI funciona como espinha dorsal da operação. Ele expõe as rotas de assistentes, conversas, produtos, pagamentos, pedidos, clientes e status, além de concentrar autenticação, observabilidade, persistência e integrações externas. PostgreSQL sustenta os dados transacionais e o histórico de execução; Redis e eventos em tempo real ajudam a manter a operação sincronizada.

WebSockets e fallback por polling foram usados para atualizar o painel operacional sem depender de refresh manual. Isso é importante para handoff, controle humano, leitura de timeline e mudança de status de conversa. A operação não precisa "procurar" o que mudou; ela recebe o evento quando algo crítico acontece.

No núcleo de IA, o trabalho ficou dividido por responsabilidade. Há triagem de intenção para decidir se o usuário está pedindo informação, produto, entrega, pagamento, status ou compra. Há agentes especializados para recuperação de informação de loja, consulta de catálogo e validação de dados. E há o fluxo de checkout, no qual o estado deixa de ser implícito e passa a ser governado por etapas como coleta de dados, tipo de entrega, endereço, oferta de programa de fidelidade, persistência de cliente e fechamento da sacola.

Essa separação é o ponto mais pragmático do projeto. A IA não tenta resolver tudo sozinha. Ela opera onde agrega flexibilidade, e entrega para regras explícitas quando o custo do erro sobe.

## Resultado e impacto

O resultado foi uma solução que funciona como produto e como operação. Ela reduz handoff desnecessário, preserva espaço para intervenção humana quando o caso exige e mantém o negócio auditável do começo ao fim.

Os indicadores da operação mostram o efeito desse desenho: redução expressiva no transbordo para atendimento humano, centenas de conversas gerenciadas por IA em produção e geração de receita já nas primeiras semanas. Mais importante do que o número isolado é o que ele representa: a tecnologia foi usada para sustentar o fluxo comercial inteiro, e não apenas para automatizar a camada mais visível da conversa.
---
