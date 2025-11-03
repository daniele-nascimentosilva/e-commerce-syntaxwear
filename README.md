# SyntaxWear — e-commerce (protótipo)

Repositório com o protótipo front-end estático do site SyntaxWear (loja de tênis / sneakers).

Resumo

# Deploy — instruções mínimas

Este repositório contém um site estático em `ecommerce-sapatos/` (HTML + CSS). abaixo estão apenas as instruções necessárias para publicar no GitHub Pages.

Pré-requisitos
- Ter o repositório no GitHub.
- Ter permissões para modificar as configurações do repositório (Settings → Pages).

Opções de deploy (escolha uma)

1) Publicar via branch `gh-pages` (rápido, sem configurar Actions)

```powershell
# publica o conteúdo da pasta ecommerce-sapatos em gh-pages
git checkout --orphan gh-pages
git --work-tree ./ecommerce-sapatos add --all
git --work-tree ./ecommerce-sapatos commit -m "Deploy site to gh-pages"
git push origin HEAD:gh-pages --force
git checkout -
```

Depois, no GitHub: Settings → Pages → Source = `gh-pages` branch.

2) Publicar usando a pasta `docs/` na branch `main`

```powershell
# copiar conteúdo para docs/ e commitar na branch main
rm -rf docs; mkdir docs
cp -r ecommerce-sapatos/* docs/
git add docs && git commit -m "Add site to docs/ for GitHub Pages" && git push
```

Depois, no GitHub: Settings → Pages → Source = `main` branch / `docs/` folder.

3) Deploy automático com GitHub Actions (recomendado)

Crie o arquivo `.github/workflows/gh-pages.yml` com este conteúdo:

```yaml
name: Deploy to GitHub Pages

on:
	push:
		branches: [ main ]

jobs:
	deploy:
		runs-on: ubuntu-latest
		steps:
			- uses: actions/checkout@v4
			- name: Deploy
				uses: peaceiris/actions-gh-pages@v3
				with:
					github_token: ${{ secrets.GITHUB_TOKEN }}
					publish_dir: ./ecommerce-sapatos

```

Esse workflow publica automaticamente o conteúdo da pasta `ecommerce-sapatos` para o Pages.

Notas importantes
- Se os caminhos dos assets (CSS/IMAGES) usarem `/css/...` (barra inicial), troque para caminhos relativos `css/...` para evitar 404 quando o site estiver hospedado em um subpath (ex.: `/<repo>/`).
- Para usar domínio customizado, crie um arquivo `CNAME` com o domínio dentro da pasta publicada.

Se quiser que eu:
- crie o arquivo de workflow `.github/workflows/gh-pages.yml` automaticamente aqui no repositório;
- ou gere um `package.json` com script `deploy` usando `gh-pages` (npm);
me diga qual preferência e eu implemento.
```

Arquivos principais
- `index.html` — marcação semântica do site (header, main com hero/categorias/featured, footer).
- `css/reset.css` — reset/normalize baseado em Andy Bell.
- `css/variables.css` — variáveis (cores, fontes) e import de fontes (verifique ordering `@charset`/`@import`).
- `css/header.css` — layout do header, menu central, drawer (mobile), e regras para o ícone do hambúrguer.
- `css/hero.css` — estilo do hero (banner) com breakpoints para mobile.
- `css/product-grid.css` — grid responsivo para produtos/destaques e regras de posição do conteúdo.
- `css/footer.css` — footer responsivo; adaptado para empilhar conteúdo em telas pequenas.

Decisões importantes já aplicadas
- Header drawer: implementado com um checkbox toggle e painel off-canvas. Estilos do drawer foram escopados para `.header .container` para evitar conflito com outros usos de `.container`.
- Footer: estrutura em `.footer-content.container` com `.footer-top` (newsletter + grid de links) e `.separator-copyright` no final para colocar `<hr>` e copyright abaixo do conteúdo.
- Breakpoints principais usados: 1280px (drawer), 900px (tablet), 600px, 420px e 360px (ajustes finos mobile).
- Hero e product grid: regras para centralizar/empilhar em mobile e evitar overflow de botões.

Como desenvolver/editar
- Estilos: edite os arquivos em `css/`.
- HTML: edite `index.html` (use classes semânticas já definidas).
- Recomendações:
	- Evite usar a classe `container` globalmente para elementos que precisam de posicionamento fixo — prefira classes específicas (ex.: `.nav-drawer`) para painéis off-canvas.
	- Para imagens de banner/produto considere usar `img` responsivo ou `srcset` se precisar de imagens diferentes por breakpoint.

Testes manuais recomendados
- Verificar os seguintes breakpoints no DevTools:
	- Desktop grande (≥1280px): menu inline, hero grande, grid em 4 colunas, footer em 2 colunas.
	- Tablet (~900px): hero centralizado, grid 2 colunas, drawer ativado se a largura for <=1280px.
	- Mobile (≤420px e ≤360px): hero com texto reduzido, botões menores (ajustados), grid empilhado, footer empilhado.

Acessibilidade e melhorias pendentes
- Acessibilidade do drawer: foco e trap (tab trap) ao abrir; fechar com ESC; consider implementar com JS para melhor UX.
- Melhor contraste: avaliar contraste do texto sobre background do hero — adicionar overlay sutil se necessário.
- SEO básico: adicionar meta tags Open Graph, meta description (já existe), e titles nas páginas de produto quando adicionar rotas reais.

Sugestões de próximos passos (opcionais)
- Separar o drawer em uma classe própria (`.nav-drawer`) em `index.html`/`header.css` para eliminar qualquer risco de conflito com outros `container`.
- Converter imagens background para tags `<img>` responsivas com `srcset` para melhor carregamento em mobile.
- Adicionar um `package.json` simples com scripts para um server local (`live-server` / `http-server`) se quiser padronizar comandos.
- Implementar testes visuais (Storybook ou screenshots) para validar responsividade entre commits.

Contribuição
- Abra uma branch por feature/bugfix e envie PR para `main`.
- Mantenha CSS modular e siga o padrão de classes existente.

Licença
- Sem licença definida no repo. Se desejar, posso adicionar um `LICENSE` (MIT, Apache-2.0, etc.).

Contato
- Se quiser, me diga que partes quer que eu documente mais (por exemplo, legenda para cada arquivo CSS, exemplos de snippets, ou um checklist de QA) e eu atualizo o README.

---
