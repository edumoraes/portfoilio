---
title: ViraLaTeX, uma workstation local-first para documentos com renderização e IA assistiva
description: Produto open source para escrever, estruturar e renderizar documentos profissionais com arquivos locais como fonte da verdade e IA operando com aprovação explícita.
weight: 3
case:
  index: Case 03
  eyebrow: Produto open source
  summary: "O ViraLaTeX parte de uma premissa forte: arquivos do usuário devem continuar sendo o centro do produto. A aplicação combina interface desktop, renderização local e um sidecar de IA que ajuda sem sequestrar o workspace nem tomar decisões silenciosas."
  stack: "Tauri • Rust • React • TypeScript • Python • LangGraph • Tectonic"
  scope:
    - desktop local-first
    - workspace em arquivos
    - renderização local de PDF
    - sidecar de IA com aprovações
    - testes em múltiplas camadas
  results:
    - preserva arquivos locais como fonte da verdade
    - renderiza PDFs localmente com pipeline inspecionável
    - exige aprovação humana antes de mutações no workspace
  links:
    - label: GitHub
      url: https://github.com/edumoraes/viralatex
---
## Contexto

Ferramentas de escrita costumam forçar um trade-off ruim. Algumas têm boa experiência de edição, mas pouca estrutura. Outras trabalham bem com markup, mas afastam o usuário. E muitas usam IA de forma opaca, escondendo onde os dados ficam, o que foi alterado e como reverter.

O ViraLaTeX nasce como resposta a esse problema. Em vez de tratar documentos como dados presos em uma plataforma, ele trata o workspace local como contrato principal e faz a aplicação trabalhar em cima dele.

## O problema

Se o produto depende de armazenamento remoto, renderização remota e edição não auditável, o usuário perde controle rápido. Isso é ainda mais sensível quando o documento tem valor profissional, histórico de revisão e estrutura reutilizável.

Então o desafio não era apenas montar um editor bonito. Era desenhar uma workstation de documentos em que arquivos locais continuassem sendo legíveis, versionáveis e reprodutíveis, enquanto a IA atuasse como assistente e não como caixa-preta.

## Arquitetura e decisões

O projeto foi dividido em camadas com responsabilidades claras. A interface desktop usa React e TypeScript dentro de uma aplicação Tauri. O backend local em Rust expõe comandos para abrir workspace, salvar dados estruturados, renderizar documentos e gerenciar o ciclo de vida do serviço de IA. Já o sidecar em Python cuida do agente, do estado conversacional e da integração com modelos.

O ponto central da arquitetura é o workspace baseado em arquivos. Perfil, blocos reutilizáveis, definições de currículo, histórico de renderização e estado operacional mínimo ficam em YAML e artefatos locais. Isso faz com que o usuário consiga inspecionar, copiar, versionar e migrar seus dados sem depender da aplicação para entender o que existe ali.

Outro acerto importante está na fronteira da IA. O sidecar não recebe liberdade irrestrita para editar o workspace. Quando propõe uma mutação, o fluxo interrompe, expõe a mudança e exige aprovação explícita. Esse detalhe parece pequeno, mas muda completamente a relação entre automação e confiança.

## Como a tecnologia resolve

Tauri e Rust entregam um aplicativo desktop leve e com acesso nativo ao sistema de arquivos sem abrir mão de uma interface moderna. React e TypeScript cuidam da experiência de uso e da orquestração do workspace. Tectonic entra como motor de renderização local, mantendo o PDF reproduzível e inspecionável.

No lado da IA, Python e LangGraph ajudam a estruturar o sidecar como um serviço local persistente, com threads, checkpoints e streaming compatível com um modelo de agente. O design fica melhor porque o agente conhece o workspace, mas continua limitado por fronteiras explícitas.

Também há um cuidado claro com qualidade de engenharia. O repositório mantém testes e validações em múltiplas camadas, cobrindo frontend, sidecar Python, backend Rust e verificações de lint e segurança. Isso reforça a proposta do produto: não é um protótipo de interface com IA, e sim uma base séria para evolução.

## Resultado e impacto

O resultado é um produto local-first coerente do início ao fim. O usuário continua dono dos seus arquivos, a renderização permanece no ambiente local e a IA só atua dentro de um fluxo que pode ser auditado e aprovado.

Esse tipo de decisão técnica resolve um problema real de confiança. Em vez de pedir que o usuário aceite abstrações escondidas, o produto deixa visível onde os dados estão, como o documento é gerado e quando a IA está propondo uma mudança. É uma arquitetura que privilegia autonomia, previsibilidade e longevidade.
---
