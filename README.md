# D-IA · SENAI Guarulhos × Google

Site do evento **D-IA (Dia da Inteligência Artificial)**, realizado pelo SENAI Guarulhos em parceria com a Google. Serve de guia para os alunos: esquenta, logística, divisão de turmas, espaços, programação, facilitadores, Socorro TI e FAQ.

O site é **mobile first**, mas foi ajustado para também ficar bom em notebooks e desktops.

## Ambiente

É um site **estático, de um único arquivo** (`index.html`). Não há build, servidor ou banco de dados.

| Item | O que é usado |
|---|---|
| Marcação | HTML5 (`lang="pt-BR"`) |
| Estilo | [Tailwind CSS](https://tailwindcss.com) via Play CDN (`cdn.tailwindcss.com`) + CSS próprio no `<style>` |
| Fontes | Google Fonts: **Sora** (títulos) e **Inter** (texto) |
| JavaScript | Vanilla JS, no fim do `index.html` (menu mobile, abas Manhã/Tarde e FAQ) |
| Dependências locais | Nenhuma (`npm`, `node` e bundlers não são necessários) |
| Internet | Necessária para carregar Tailwind e fontes |

### Como rodar

Abra o `index.html` no navegador. Para simular um servidor local:

```bash
python3 -m http.server 8080
# acesse http://localhost:8080
```

### Estrutura

```
.
├── index.html
├── README.md
└── img/
    └── facilitadores/     # fotos dos facilitadores (você cria esta pasta)
        ├── eduardo.jpg
        ├── claudiane.jpg
        ├── ailton.jpg
        ├── gilberto.jpg
        ├── fortini.jpg
        └── rubem.jpg
```

### Seções e âncoras

| Âncora | Seção |
|---|---|
| `#top` | Hero (título, brindes e aviso da conta @edu.senai.br) |
| `#brindes` | Card de brindes do Google |
| `#esquenta` | Passo a passo antes do evento |
| `#socorro-ti` | Socorro TI |
| `#logistica` | Logística e orientação |
| `#turmas` | Divisão das turmas (abas Manhã/Tarde) |
| `#espacos` | Guia de espaços e capacidade |
| `#programacao` | Programação (abas Manhã/Tarde) |
| `#facilitadores` | Facilitadores e especialistas |
| `#faq` | Perguntas frequentes (lista no array `faqs` do script) |

## Como editar

### Facilitadores: nome, sobrenome e foto

Cada facilitador é um `<article>` na seção `#facilitadores`.

1. Troque `SOBRENOME` pelo sobrenome real.
2. Salve a foto em `img/facilitadores/` com o nome do arquivo já indicado no `src` (ex.: `eduardo.jpg`).
3. Use foto **quadrada** (ex.: 400×400 px). O CSS (`.avatar`, com `rounded-full` e `object-fit: cover`) recorta em círculo automaticamente.

Enquanto a foto não existir, aparece um círculo colorido com a inicial do nome. Para adicionar mais alguém, copie um `<article>` inteiro e mude nome, cargo, `src` e `alt`.

### Brindes

Os brindes Google aparecem em três lugares: item **🎁 Brindes** no menu, card `#brindes` no hero e etiquetas nos cards Foyer e Biblioteca e na linha de ativação da programação. A regra comunicada é: **só quem fizer as ativações ganha o brinde**.

### Cabeçalho

- Até 1279 px de largura: logo + botão **Acessar e-mail** + menu hambúrguer.
- A partir de 1280 px (`xl`): menu completo em linha. Todos os itens usam `whitespace-nowrap` para não quebrar em duas linhas.
- O botão **Acessar e-mail** abre `https://mail.google.com/`. Troque o `href` se houver outro endereço.

### Cores

Definidas em variáveis CSS no `:root` (`--violet`, `--blue`, `--sky`, `--emerald` etc.), no topo do `<style>`.

## Publicação

Qualquer hospedagem estática serve (GitHub Pages, Netlify, Vercel, servidor do SENAI). Basta publicar o `index.html` junto com a pasta `img/`.

> **Produção:** o Tailwind Play CDN é ótimo para prototipar, mas o próprio Tailwind recomenda compilar o CSS em produção. Se o site tiver muito acesso, gere um CSS final com a [CLI do Tailwind](https://tailwindcss.com/docs/installation) e troque a tag `<script src="https://cdn.tailwindcss.com">` pelo `<link>` do CSS gerado.

## Acessibilidade

- Foco visível por teclado em links e botões.
- Menu mobile com `aria-expanded` e `aria-controls`.
- Animações desativadas para quem usa `prefers-reduced-motion`.
- Fotos com `alt` descritivo.