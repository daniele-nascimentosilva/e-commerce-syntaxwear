# SyntaxWear — e-commerce (protótipo)

Repositório com o protótipo front-end estático do site SyntaxWear (loja de tênis / sneakers).

Resumo
- Projeto: e-commerce estático (HTML + CSS)
- Pasta principal do site: `ecommerce-sapatos/`
- Propósito: demonstrar layout responsivo (header com drawer, hero, grid de produtos, footer responsivo)

Como abrir localmente
- Recomendado (rápido): abra `ecommerce-sapatos/index.html` no navegador.
	- No Windows PowerShell você pode executar:

```powershell
# a partir da raiz do repo
Start-Process .\ecommerce-sapatos\index.html
```

- Desenvolvedor (recomendado para refresh automático): rode um Live Server (VS Code Live Server ou `npx http-server`) a partir da pasta `ecommerce-sapatos`.

Estrutura do projeto (resumida)

```
/ (repo root)
	README.md
	ecommerce-sapatos/
		index.html
		assets/
		css/
			reset.css
			variables.css
			base.css
			header.css
			hero.css
			product-card.css
			product-grid.css
			footer.css
		images/
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
