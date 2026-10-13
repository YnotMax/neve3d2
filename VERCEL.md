# Guia de Publicação no Vercel — Cozy Plow · 雪かき惑星

Este projeto está **100% configurado e pronto para deploy no Vercel** com um único clique ou comando.

---

## 🚀 Opção 1: Publicação Rápida pelo Painel da Vercel (Recomendado)

1. **Suba o código para o seu repositório Git** (GitHub, GitLab ou Bitbucket).
2. Acesse [vercel.com](https://vercel.com) e clique em **"Add New..." ➔ "Project"**.
3. Selecione o repositório do jogo.
4. O Vercel detectará as configurações automaticamente graças ao arquivo `vercel.json`:
   - **Framework Preset**: `Vite`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`
5. Clique em **"Deploy"**. Em menos de 1 minuto, seu jogo estará no ar com link global HTTPS (ex: `https://seu-jogo.vercel.app`).

---

## ⚡ Opção 2: Publicação via Terminal (Vercel CLI)

Se você tiver o Vercel CLI instalado na sua máquina:

```bash
# 1. Instalar Vercel CLI (se ainda não tiver)
npm i -g vercel

# 2. Fazer login
vercel login

# 3. Publicar em produção
vercel --prod
```

O CLI lerá automaticamente o `vercel.json` e enviará a pasta de build diretamente.

---

## 📂 Arquivos de Otimização Criados para a Vercel

| Arquivo | Função no Vercel |
|---|---|
| `vercel.json` | Configuração nativa de SPA (rewrites para `/index.html`), cabeçalhos de segurança (CSP, nosniff, frame-options) e cache imutável de 1 ano para arquivos estáticos (`/assets/*`). |
| `public/favicon.svg` | Ícone vetorial do jogo (trator limpa-neve e domo de neve) exibido na aba do navegador. |
| `public/site.webmanifest` | Permite instalar o jogo como PWA (App na tela inicial) no iPhone, Android e Desktop. |
| `public/robots.txt` | Permite que o Google e outros buscadores indexem seu jogo. |
| `public/sitemap.xml` | Mapa do site para otimização SEO. |
| `vite.config.ts` | Resolução ESM moderna sem warnings de build. |

---

## 🎮 Como Funciona o Jogo na Vercel

### 1. Modo Solo & Bots (100% Nativo na Vercel)
- Na Vercel, o jogo roda com **máxima velocidade via CDN Global de baixa latência**.
- Todo o motor 3D (Three.js), áudio procedural WebAudio, física das bolas de neve, 4 pilotos carismáticos (**Jhony, Kercio, Jusimar e Tiago**), chefes e estágios funcionam **100% no navegador do jogador**, sem consumir servidor backend e com custo zero.

### 2. Modo Co-Op Online com Amigos (Multiplayer em Tempo Real)
- O Vercel é uma plataforma de hospedagem de frontend estático/serverless (não mantém conexões WebSocket persistentes abertas continuamente).
- O Cozy Plow possui **inteligência de reconexão adaptativa**: quando executado no Vercel, ele detecta automaticamente e não trava o jogo nem gera spam no console.
- **Deseja jogar online com amigos pela internet?**
  1. Você pode rodar o arquivo `server.ts` gratuitamente no **Render.com**, **Railway.app** ou **Fly.io** (Node.js com WebSockets).
  2. No jogo publicado no Vercel, clique em **"Jogar com Amigos" ➔ "Opções ⚙️"**.
  3. Cole a URL do seu servidor (ex: `wss://meu-cozy-plow.onrender.com`) e clique em **"Salvar & Conectar"**.
  4. Ao clicar em **"Copiar Link de Convite"**, o link já é gerado contendo o código da sala e o endereço do servidor, conectando todos os seus amigos instantaneamente!
