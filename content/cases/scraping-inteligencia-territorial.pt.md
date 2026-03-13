---
title: Scraping operacional com geocodificação, deduplicação e leitura territorial
description: Ferramenta para mapear presença física e cobertura territorial a partir de scraping, geração radial de CEPs e visualização geográfica em mapa interativo.
weight: 4
case:
  index: Case 04
  eyebrow: Aquisição de dados
  summary: "Este case organiza um problema de coleta territorial que costuma ser mal resolvido por scraping linear. Em vez de consultar poucos pontos fixos e aceitar lacunas, a solução gera cobertura por raio, transforma coordenadas em CEPs úteis e entrega dados limpos para análise geográfica."
  stack: "Python • Playwright • Geopy • Streamlit • CSV • geocodificação"
  scope:
    - scraping estruturado
    - geração radial de CEPs
    - geocodificação e cache
    - deduplicação
    - dashboard geográfico
  results:
    - amplia a cobertura de coleta a partir de um CEP central e raio configurável
    - remove duplicidades antes da análise
    - transforma dados brutos em mapa utilizável para operação
---
## Contexto

Quando a informação de presença física está espalhada em páginas de consulta, a coleta manual vira desperdício rápido. O desafio aqui não era só extrair registros. Era conseguir cobrir uma área geográfica de forma mais inteligente, consolidar resultados sem duplicidade e tornar a saída útil para leitura territorial.

O trabalho precisava servir tanto para coleta quanto para exploração posterior dos dados.

## O problema

Scraping baseado em consultas fixas costuma gerar visão incompleta. Se a busca depende apenas de alguns CEPs ou regiões escolhidas manualmente, parte da cobertura fica invisível. Além disso, o retorno bruto quase sempre vem com duplicidades, endereços inconsistentes e pouco apoio para exploração geográfica.

Então o problema era menos "raspar uma página" e mais construir um pipeline de aquisição territorial que cobrisse melhor a área, aceitasse imperfeições do dado de origem e devolvesse uma base utilizável.

## Arquitetura e decisões

A solução foi organizada em duas frentes. A primeira é a coleta: um scraper automatiza o preenchimento do fluxo de consulta e extrai os registros encontrados. A segunda é a expansão territorial: a partir de um CEP central, o sistema geocodifica a origem, calcula pontos em rosa dos ventos por raio e tenta transformar essas coordenadas em novos CEPs para ampliar a cobertura da busca.

Essa decisão é importante porque ataca a limitação estrutural do scraping simples. Em vez de depender de um conjunto pequeno de entradas manuais, a coleta passa a explorar a área ao redor de um ponto com um padrão replicável.

Depois da coleta, o pipeline ainda resolve três problemas típicos de dado operacional: deduplicação, geocodificação e visualização. A base não é entregue como uma lista crua para alguém "se virar". Ela já sai preparada para leitura em mapa e para análise de cobertura.

## Como a tecnologia resolve

Python foi usado como base para unificar automação do navegador, tratamento dos CSVs e componentes geográficos. Playwright entra no ponto em que é preciso reproduzir a consulta do site de forma confiável. Geopy e Nominatim cuidam da geocodificação direta e reversa, enquanto o uso de cache reduz custo e repetição de chamadas.

A geração radial de CEPs é a parte mais pragmática do desenho. Ela transforma um ponto central em uma área explorável, o que melhora a coleta sem exigir uma lista grande e manual de entradas. Quando a geocodificação não encontra o CEP exato, o fluxo tenta caminhos alternativos para aproximar a busca e não quebrar desnecessariamente.

O dashboard em Streamlit fecha o ciclo. Ele não existe como extra cosmético, e sim como camada de leitura operacional. Depois de limpar, deduplicar e geocodificar os dados, a visualização em mapa ajuda a enxergar concentração, lacunas e alcance territorial sem depender de tratamento externo.

## Resultado e impacto

O resultado é uma ferramenta que vai além do scraping pontual. Ela coleta, amplia a cobertura, limpa o dado e entrega uma base pronta para análise geográfica. Isso reduz o trabalho manual nas duas pontas: menos esforço para consultar e menos esforço para interpretar.

Tecnicamente, o valor está em tratar a coleta como pipeline e não como script isolado. A solução usa automação, geografia e visualização de forma integrada para resolver um problema operacional concreto: transformar consulta dispersa em visão territorial acionável.
---
