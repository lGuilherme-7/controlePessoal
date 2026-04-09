# 💸 Fluxo — Controle Financeiro Pessoal

> Dashboard financeiro moderno, responsivo e funcional — desenvolvido com HTML, CSS e JavaScript puro, sem dependências externas.

---

## 📋 Sobre o Projeto

O **Fluxo** é um sistema de controle financeiro pessoal com dashboard, gráficos e gestão de transações completa. Desenvolvido como um único arquivo `index.html`, não requer servidor, framework ou instalação. Todos os dados são persistidos no navegador via LocalStorage.

---

## 🌐 Link para acessar

https://lguilherme-7.github.io/controlePessoal/

---

## ✨ Funcionalidades

- **Dashboard** com visão geral de saldo, entradas e saídas
- **Gráfico de barras** dos últimos 6 meses (entradas × saídas) desenhado com Canvas API puro
- **Cards de resumo** com saldo total, total de entradas e total de saídas
- **Lista de transações recentes** no dashboard (últimas 5)
- **Página de transações** com:
  - Filtro por tipo (todas, entradas, saídas)
  - Busca em tempo real por descrição, categoria ou observação
  - Ordenação por data (mais recentes/antigas) e valor (maior/menor)
  - Exclusão individual com modal de confirmação
  - Exclusão em lote ("Apagar todas")
- **Formulário de nova transação** com:
  - Toggle de tipo (Entrada / Saída) com feedback visual
  - Máscara de valor monetário automática
  - Seleção de categoria com ícones (14 categorias disponíveis)
  - Campo de data com padrão no dia atual
  - Campo de observação opcional
  - Preview em tempo real antes de salvar
  - Validação de formulário com mensagens de erro inline
- **Persistência total via LocalStorage** — dados mantidos ao fechar o navegador
- **Toasts de feedback** para todas as ações (adicionar, remover, limpar)
- **Modal de confirmação** para remoção de transações
- **Sidebar de navegação** fixa (desktop) com menu hambúrguer (mobile)
- **Design responsivo** (mobile first)

---

## 🗂️ Estrutura do Projeto

```
fluxo/
└── index.html        # Aplicação completa (HTML + CSS + JS em um único arquivo)
```

O projeto é intencionalmente um arquivo único para facilitar deploy e distribuição. O código interno está organizado em três blocos bem delimitados por comentários:

| Bloco | Localização | Conteúdo |
|---|---|---|
| HTML | `<body>` | Estrutura e marcação semântica |
| CSS | `<style>` | Estilos, variáveis e responsividade |
| JS | `<script>` | Dados, lógica, gráfico e interatividade |

---

## 🚀 Como Usar

**1. Clone ou baixe o projeto:**
```bash
git clone https://github.com/seu-usuario/fluxo-financeiro.git
```

**2. Abra o arquivo no navegador:**
```bash
# Simplesmente abra o arquivo:
open index.html

# Ou com um servidor local (opcional):
npx serve .
```

Não é necessário instalar nada. Funciona offline diretamente no navegador.

---

## ⚙️ Configuração

### Chave de armazenamento (LocalStorage)

Os dados são salvos sob a chave `fluxo_transactions`. Para resetar todos os dados do usuário, basta limpar essa chave no navegador (DevTools → Application → LocalStorage) ou usar o botão "Apagar todas" na página de transações.

Para alterar a chave (ex.: múltiplas instâncias do app):

```javascript
const STORAGE_KEY = 'fluxo_transactions'; // ← Altere aqui
```

### Categorias

As categorias e seus ícones são definidos no objeto `CAT_ICON` no bloco `<script>`:

```javascript
const CAT_ICON = {
  'Salário':        '💼',
  'Freelance':      '💻',
  'Alimentação':    '🍽️',
  'Moradia':        '🏠',
  // ...
};
```

Para adicionar uma nova categoria, inclua a entrada no objeto `CAT_ICON` e adicione a `<option>` correspondente no `<select id="txCategory">` no HTML.

### Meses no gráfico

O gráfico exibe os últimos **6 meses** por padrão. Para alterar a janela de tempo, edite a constante no script:

```javascript
for (let i = 5; i >= 0; i--) { // ← Altere o "5" para o número de meses desejado - 1
```

---

## 🎨 Tecnologias

| Tecnologia | Uso |
|---|---|
| HTML5 semântico | Estrutura e acessibilidade |
| CSS3 (variáveis, grid, flexbox) | Layout e design responsivo |
| JavaScript ES6+ | Lógica, DOM e LocalStorage |
| Canvas API | Gráfico de barras sem bibliotecas externas |
| Google Fonts (Plus Jakarta Sans + JetBrains Mono) | Tipografia |

Sem frameworks, sem bundlers, sem dependências de terceiros.

---

## 📱 Responsividade

| Breakpoint | Layout |
|---|---|
| `> 1024px` | Sidebar fixa, formulário em duas colunas |
| `720px – 1024px` | Sidebar fixa, formulário em coluna única |
| `< 720px` | Topbar + menu hambúrguer, sidebar deslizante |
| `< 860px` | Cards em grid 2 colunas |
| `< 520px` | Cards em coluna única, filtros em linha |

---

## 🔧 Personalização Rápida

**Alterar as cores principais** — edite as variáveis CSS no topo do `<style>`:

```css
:root {
  --blue:    #2563EB;  /* Cor primária / botões / destaque */
  --green:   #12B76A;  /* Entradas */
  --red:     #F04438;  /* Saídas / erros */
  --ink:     #0F1117;  /* Cor do texto principal */
  --bg:      #F4F5FA;  /* Fundo da página */
  --sidebar-bg: #0F1117; /* Fundo da sidebar */
}
```

**Adicionar uma nova página** — inclua no HTML um nav-item e um bloco `<main class="page">`, depois registre a rota na função `navigate()` no script.

---

## 🗃️ Estrutura dos Dados

Cada transação é um objeto JSON salvo no array em LocalStorage:

```javascript
{
  id:          "abc123xy",          // ID único (timestamp + random)
  type:        "income",            // "income" | "expense"
  description: "Salário outubro",   // Texto livre
  amount:      3500.00,             // Número (sempre positivo)
  category:    "Salário",           // Categoria selecionada
  date:        "2025-10-05",        // ISO 8601 (YYYY-MM-DD)
  note:        "Adiantamento 13°",  // Observação opcional
  createdAt:   "2025-10-05T14:23:00.000Z" // Timestamp de criação
}
```

---

## 📦 Deploy

Por ser um único arquivo estático, o Fluxo pode ser hospedado em qualquer serviço:

- **GitHub Pages** — suba o repositório e ative Pages na branch `main`
- **Netlify / Vercel** — arraste a pasta para o dashboard
- **Qualquer hospedagem compartilhada** — upload via FTP

> ⚠️ Os dados ficam no **navegador do usuário** (LocalStorage). Cada dispositivo/navegador terá seu próprio conjunto de dados. Não há sincronização em nuvem.

---

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar, modificar e distribuir.

---

Feito com 💚 e muito saldo positivo.

