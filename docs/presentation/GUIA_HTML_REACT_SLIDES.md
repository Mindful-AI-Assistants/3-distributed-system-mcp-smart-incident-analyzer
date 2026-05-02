# Guia: slides em HTML + React (`react-dom`)

Este documento descreve como os slides do **MCP Smart Incident Analyzer** foram concebidos para serem gerados e mantidos como **aplicação single-page** com **React 18** e **`react-dom`** via CDN, sem bundler obrigatório.

## Stack recomendada

| Peça | Função |
|------|--------|
| `react@18` + `react-dom@18` (UMD) | Componentes e renderização |
| `@babel/standalone` | `type="text/babel"` no navegador para JSX |
| Fontes (ex.: Google Fonts) | Tipografia legível em projeção |

Arquivo de referência no repositório: `_Presentation/apresentacao-readme-mestre-completa.html`.

## Especificação visual (dark, turquesa, tipografia clara)

1. **Fundo**: gradiente escuro (`#020617` → `#000`) com halos discretos em turquesa/ciano para profundidade.
2. **Texto principal**: branco/off-white (`#f8fafc`, `#e2e8f0`).
3. **Destaques**: turquesa (`#14b8a6`, `#2dd4bf`) em títulos, chips, bordas e barra de progresso.
4. **Cartões / blocos de código**: fundo `rgba(15, 23, 42, 0.55)`, borda `rgba(148, 163, 184, 0.2)`.
5. **Monoespaçado** para ASCII e Protobuf: `ui-monospace`, `SF Mono`, `Consolas`.

Variáveis CSS sugeridas:

```css
:root {
  --bg-0: #020617;
  --ink: #f8fafc;
  --ink-soft: #cbd5e1;
  --turquoise: #14b8a6;
  --turquoise-soft: #0f766e;
  --border: rgba(148, 163, 184, 0.25);
}
```

## Animações suaves

- **Transição entre slides**: `opacity`, `translateX`, `blur` leve no slide inativo; easing `cubic-bezier(0.16, 1, 0.3, 1)`.
- **Entrada do conteúdo ativo**: keyframes `fadeRise` (opacity + `translateY(10px)` → 0) com atraso escalonado em subtítulo e corpo.
- **Fundo**: animação lenta `drift` em camadas decorativas (movimento mínimo, não distrai da leitura).

Evite animações agressivas em listas longas; priorize legibilidade em sala de aula.

## Modelo de dados do deck

Cada slide é um objeto JavaScript. Campos suportados no arquivo de referência:

| Campo | Uso |
|-------|-----|
| `section` | Rótulo curto (chip superior) |
| `title` | Título do slide |
| `subtitle` | Frase de apoio |
| `bullets` | Lista de pontos-chave |
| `columns` | Dois blocos lado a lado `{ title, text }` |
| `ascii` | Diagrama ou fluxo em texto monoespaçado |
| `code` | Objeto `{ lang, body }` para exemplos (Protobuf, JSON-RPC) |
| `closing` | Slide final institucional |

Para **Mermaid**: o README já contém os blocos ` ```mermaid ` **fonte de verdade**. Nos slides, use uma das estratégias:

1. **Exportar PNG/SVG** a partir do Mermaid Live Editor e inserir como `<img>` em um slide dedicado; ou
2. Manter o diagrama no README e, no slide, **referenciar** o fluxo + um **ASCII resumido** para leitura imediata sem dependências de rede.

## Navegação e apresentação

- **Setas** / **Page Down** / **Espaço**: próximo slide  
- **Backspace** / **Page Up**: slide anterior  
- **Home** / **End**: primeiro / último slide  
- **F**: tela cheia  

## Relação com o README

O mapeamento slide a slide está em [ESTRUTURA_APRESENTACAO.md](ESTRUTURA_APRESENTACAO.md). Qualquer alteração substantiva no `README.md` deve ser propagada para:

1. `ESTRUTURA_APRESENTACAO.md` (roteiro),
2. array `slides` em `_Presentation/apresentacao-readme-mestre-completa.html`.

## Checklist antes de apresentar

- [ ] Abrir o HTML localmente (`file://` ou servidor estático simples: `python -m http.server`).
- [ ] Conferir nomes da equipe e do professor no slide de encerramento.
- [ ] Testar resolução 1280×720 e 1920×1080.
- [ ] Se usar imagens Mermaid exportadas, validar contraste no projetor.
