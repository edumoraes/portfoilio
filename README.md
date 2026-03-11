# Portfólio em Hugo

Este repositório agora usa Hugo para gerar um portfólio one-page pronto para GitHub Pages.

## Estrutura

- `content/_index.md`: conteúdo editável da home
- `layouts/`: templates Hugo
- `static/`: CSS e JavaScript da interface
- `.github/workflows/hugo.yml`: deploy automático no GitHub Pages

## Rodando localmente com Docker Compose

Preview:

```bash
docker compose up
```

Depois abra `http://localhost:1313`.

Build estático:

```bash
docker compose run --rm hugo --minify
```

## Rodando localmente com Docker

Preview:

```bash
docker run --rm -p 1313:1313 -v "$PWD":/src -w /src ghcr.io/gohugoio/hugo:latest server --bind 0.0.0.0
```

Build:

```bash
docker run --rm -v "$PWD":/src -w /src ghcr.io/gohugoio/hugo:latest --minify
```

## Publicação no GitHub Pages

1. Faça commit e push para `main`.
2. No GitHub, abra `Settings > Pages`.
3. Em `Build and deployment`, selecione `GitHub Actions`.
4. O workflow `Deploy Hugo site` vai gerar e publicar a pasta `public/`.

## Próximos ajustes

- Refinar a copy em `content/_index.md` conforme o foco das vagas.
- Adicionar novos tipos de conteúdo se quiser expandir além da home.
- Incluir um link real de GitHub se quiser exibi-lo na seção de contato.
