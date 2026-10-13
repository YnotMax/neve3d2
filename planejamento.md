# Planejamento — Cozy Plow (雪かき惑星) em Português do Brasil, Otimização Mobile & Deploy Vercel

## 1. Visão Geral e Objetivo
Oferecer uma experiência acolhedora, 100% traduzida em Português do Brasil (PT-BR), com 4 novos pilotos carismáticos (**Jhony**, **Kercio**, **Jusimar** e **Tiago**), jogabilidade impecável em dispositivos móveis (smartphones Android e iOS), controle ergonômico por toque, seletor de taxa de quadros (30 FPS econômico/estável por padrão, com opção de 60 FPS), **acompanhamento dinâmico de rotação de tela (modo vertical e horizontal)** e **preparação completa para publicação em produção na Vercel**.

---

## 2. Decisões Confirmadas com o Usuário [EXECUTADAS]

1. **Personagens Renomeados**:
   - 🦊 **Jhony** (Piloto 0 / Raposa de Fogo) — Habilidade: Espiral da Raposa
   - 🐻 **Kercio** (Piloto 1 / Urso Escavadeira) — Habilidade: Giga-Pisada
   - 🐰 **Jusimar** (Piloto 2 / Coelho Planador) — Habilidade: Arrancada Aurora
   - 🐸 **Tiago** (Piloto 3 / Sapo do Vórtice) — Habilidade: Vórtice do Sapo
2. **Desempenho no Celular (30 FPS ⟷ 60 FPS)**:
   - Padrão em 30 FPS para estabilidade térmica, evitando aquecimento do smartphone e poupando bateria.
   - Botão rápido de alternância no HUD e gaveta mobile para 60 FPS quando o usuário preferir máxima fluidez.
   - Ajuste adaptativo do `pixelRatio` (1.25x no modo 30 FPS para evitar sobrecarga de GPU, até 2.0x no modo 60 FPS).
3. **Controles Mobile e Dicas Contextuais de Tela**:
   - Detecção dinâmica de dispositivo com toque (`ontouchstart` / touchscreen).
   - Joystick virtual analógico posicionado no canto **inferior esquerdo** (ergonomia para o polegar esquerdo com rótulo `🕹️ Mover`).
   - Botões de ação (**Esmagar** e **Especial**) e melhorias (**Arado** e **Velocidade**) acessíveis com o polegar direito.
   - Substituição automática de atalhos de teclado por instruções de toque nativas no celular.
   - Painel ilustrado de controles ("Como Jogar no Celular e no Computador").
4. **Comportamento ao Girar o Celular (Orientação Retrato ⟷ Paisagem)**:
   - Redimensionamento imediato e em cascata (0ms, rAF, 100ms e 300ms) ao detectar `orientationchange`, `screen.orientation` ou `resize`.
   - Câmera 3D inteligente com **FOV Adaptativo**: em modo vertical (retrato), o campo vertical se expande para manter o planeta e os corredores visíveis sem cortes; em modo horizontal (paisagem), a visão panorâmica cinemática é preservada.
   - Isolamento de entalhes (notches) e gestos do sistema operacional através de `viewport-fit=cover` e `env(safe-area-inset-*)`.
   - Layout compacto para modo paisagem (`@media (orientation: landscape) and (max-height: 540px)`).
5. **Prontidão de Produção para Vercel [NOVO]**:
   - Criação de `vercel.json` com detecção de framework Vite, rewrites de SPA para `/index.html`, cabeçalhos de segurança (CSP, nosniff, frame-options) e cache imutável de 1 ano para assets estáticos.
   - Criação da pasta `/public` com `favicon.svg` temático acolhedor, `site.webmanifest` (PWA para iPhone/Android), `robots.txt` e `sitemap.xml`.
   - Atualização do cabeçalho HTML com metadados SEO, tags de PWA móvel e Schema.org JSON-LD para VideoGame/WebApplication.
   - Conexão WebSocket resiliente: no ambiente serverless estático da Vercel, o jogo detecta automaticamente e roda em modo Solo e Bots nativo com desempenho máximo, sem erros de console ou loops de reconexão.
   - Suporte a servidores co-op online externos (ex: Render, Railway, Fly.io) configuráveis via UI do modal multijogador, query string `?ws=...` e links de convite compartilháveis.

---

## 3. Escopo Detalhado por Camadas e Status

### Camada 1: Metadados, Identidade & Pilotos [CONCLUÍDO]
- `PILOT_CONFIGS` em `index.html`: Jhony, Kercio, Jusimar e Tiago.
- Cartões de seleção no menu inicial, lista no modal multijogador (`#mp-pilot-choices`) e animações secundárias no Three.js.
- Servidor `server.ts` atualizado para sincronização dos pilotos.

### Camada 2: Motor de Taxa de Quadros (30 FPS Padrão / 60 FPS Opcional) [CONCLUÍDO]
- Variável de estado `targetFps` controlando a cadência de renderização no loop `animate(nowMs)`.
- Pílula interativa `#fps-toggle-btn` com ícone de raio: `⚡ 30 FPS` / `⚡ 60 FPS`.
- Modulação adaptativa de `renderer.setPixelRatio` (1.25x no modo 30 FPS para evitar sobrecarga de GPU, até 2.0x no modo 60 FPS).

### Camada 3: Ergonomia e Controles Touch no Celular [CONCLUÍDO]
- **Posicionamento do Analógico**: Ancorado no canto inferior esquerdo com rótulo tátil `🕹️ Mover` e escuta global de ponteiro.
- **Interação na Tela 3D**: Metade esquerda direciona o analógico; metade direita arremessa bola de neve.
- **Botões no Deck**: Acesso direto a Esmagar, Especial, Arado e Velocidade com o polegar direito.
- **Instruções Adaptativas**: Teclas de computador ocultadas no mobile (`body.is-touch-device`).
- **Modal de Controles**: Guia completo acessível no HUD.

### Camada 4: Rotação de Tela & Adaptação de Orientação [CONCLUÍDO]
- **Listeners Abrangentes**: `resize`, `orientationchange`, `screen.orientation` e `visualViewport`.
- **Compensação de Animação do Browser**: Acionamento em cascata (0ms, rAF, 100ms e 300ms) para acomodar a animação de rotação em navegadores mobile (iOS Safari e Android Chrome).
- **FOV Adaptativo no Three.js**: Em retrato vertical o FOV expande dinamicamente para preservar visão do planeta; em paisagem mantém 50°.
- **Proteção de Safe Areas**: `viewport-fit=cover` e `env(safe-area-inset-*)` protegendo HUD e joystick.
- **Layout Paisagem Otimizado**: CSS dedicado para smartphones na horizontal.

### Camada 5: Prontidão para Vercel & Deploy em Produção [CONCLUÍDO]
- **Arquivo `vercel.json`**: Configurações de build Vite (`dist`), rotas de SPA e cabeçalhos de segurança e cache.
- **Pasta `/public` e Ativos de Produção**:
  - `favicon.svg`: Ícone vetorial do limpa-neve e domo de neve.
  - `site.webmanifest`: Instalação como Web App (PWA) no iOS e Android.
  - `robots.txt` e `sitemap.xml`: Otimização para rastreadores de busca.
- **Metatags & SEO em `index.html`**: Idioma `pt-BR`, Schema.org JSON-LD para VideoGame e tags de Web App iOS/Android.
- **Resiliência do Multiplayer na Nuvem**:
  - Detecção automática de ambiente sem WebSocket na Vercel com fallback transparente para Solo & Bots.
  - Reconexão inteligente com backoff exponencial (3s, 5s, 10s, 20s, max 30s) eliminando loops e mensagens no console.
  - Seção no modal "Jogar com Amigos" para informar URL de servidor WebSocket customizado (ex: Render/Railway).
  - Links de convite inteligentes que incluem o servidor configurado via parâmetro `&ws=...`.
- **Guia de Deploy `VERCEL.md`**: Instruções passo a passo em português para deploy via painel web ou Vercel CLI.

---

## 4. Validação & Qualidade
- `compile_applet`: Compilação Vite do cliente concluída com 100% de sucesso.
- `lint_applet`: Validação TypeScript sem nenhum erro ou aviso.
- `vite.config.ts`: Modernizado com `fileURLToPath` para compilação limpa em qualquer ambiente Node.js.
