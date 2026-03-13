---
title: Classificação de catálogo com IA, busca assistida e fallback operacional
description: Pipeline para transformar um trabalho manual de classificação em um fluxo auditável, com busca web, decisão assistida por LLM, score de confiança e saídas prontas para operação.
weight: 2
case:
  index: Case 02
  eyebrow: Automação operacional
  summary: "Este case parte de um problema clássico de operação: planilhas grandes, contexto incompleto e muito trabalho manual para enquadrar produtos em categorias úteis para o negócio. A solução foi um pipeline que combina busca, LLM, validação e retomada de execução sem esconder incerteza."
  stack: "Python • LangGraph • OpenAI • DuckDuckGo Search • Excel • GUI/CLI"
  scope:
    - ingestão de planilhas
    - enriquecimento por busca
    - classificação com LLM
    - score de confiança
    - retomada e relatórios
  results:
    - reduziu para horas um processo que levaria pelo menos 3 semanas
    - automatizou a organização de catálogo e a consolidação operacional
    - manteve dúvida e erro como estados explícitos, sem mascarar incerteza
---
## Contexto

O trabalho começava em uma planilha e terminava em outra, mas o custo estava no meio: entender cada item, buscar contexto, decidir a categoria correta e registrar isso de forma consistente. Quando o volume cresce, a operação passa a ser dominada por tarefas repetitivas e revisão manual.

O objetivo não era só "classificar com IA". Era criar um fluxo confiável o bastante para virar ferramenta de uso real, com saídas úteis para o time e comportamento previsível quando a informação disponível não fosse suficiente.

## O problema

Planilhas desse tipo costumam ter descrições incompletas, nomes ambíguos e pouco contexto sobre aplicação real do produto. Se o sistema tenta decidir só com base no texto bruto da linha, o erro sobe rápido. Se ele responde sempre com segurança, mesmo quando está incerto, vira risco operacional disfarçado de automação.

Então o problema tinha duas partes. Primeiro, enriquecer o item antes da decisão. Depois, representar incerteza de forma explícita, para que a operação soubesse quando confiar e quando revisar.

## Arquitetura e decisões

A solução foi estruturada como um grafo de estados em LangGraph. Em vez de uma função única que recebe uma linha e devolve uma categoria, o fluxo foi quebrado em etapas pequenas e observáveis: construir a query de busca, buscar contexto, classificar com LLM, interpretar a resposta e decidir se o resultado é utilizável, duvidoso ou erro.

Essa decomposição foi importante por dois motivos. O primeiro é técnico: cada etapa pode ser testada, ajustada e instrumentada separadamente. O segundo é operacional: quando algo falha, fica claro onde e por quê.

Outro ponto de rigor foi manter um threshold de confiança e estados explícitos de saída. O sistema não foi desenhado para parecer sempre certo. Ele foi desenhado para ser útil mesmo quando não consegue decidir sozinho. Em vez de inventar categoria, ele marca dúvida, registra observação e permite revisão manual com contexto.

Além do fluxo principal, a aplicação ganhou duas superfícies de uso: CLI e interface gráfica. Isso evita que a automação fique restrita a quem programa e aproxima a ferramenta da rotina operacional.

## Como a tecnologia resolve

Python foi usado como base por ser adequado para o ecossistema de planilhas, automação, busca e integração com LLMs. A leitura e escrita de Excel preservam a estrutura original e adicionam colunas de classificação, confiança, status e observações, o que facilita adoção sem reestruturar o trabalho do time.

LangGraph resolve bem o que aqui importa: fluxo com etapas explícitas, retries controlados e estado bem definido. DuckDuckGo Search entra como fonte de contexto externo para reduzir a dependência de descrições ruins ou incompletas. O modelo da OpenAI fica responsável por sintetizar esse contexto e devolver uma classificação estruturada, não texto livre.

O desenho da aplicação também é pragmático fora do núcleo de IA. Há progresso persistido para retomada, logs estruturados, relatórios em TXT, CSV e JSON, além de estatísticas úteis para acompanhamento da execução. Em uma automação longa, isso vale tanto quanto a classificação em si.

## Resultado e impacto

O ganho principal foi transformar um processo que tomaria semanas em um fluxo concluído em horas, sem trocar velocidade por opacidade. A automação não esconde o que sabe e o que não sabe; ela explicita confiança, erro e dúvida como parte do produto.

Isso torna a solução mais confiável para uso operacional. O time recebe uma planilha enriquecida, um relatório claro do que aconteceu e uma ferramenta que pode ser usada tanto por terminal quanto por interface gráfica. O resultado não é apenas menos trabalho manual. É mais previsibilidade no processo inteiro.
---
