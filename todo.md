# Lista de Tarefas (TODO) — Tradução e Melhorias Planeta Limpa-Neve 3D (PT-BR)

## Tarefas Concluídas

- [x] Criar arquivo de planejamento detalhado (`planejamento.md`)
- [x] Criar lista de acompanhamento (`todo.md`)
- [x] **Tradução Total do Título da Página & Identidade Visual (100% PT-BR)**:
  - [x] `<title>` da aba do navegador alterado para: `Planeta Limpa-Neve 3D — Jogo Acolhedor de Limpeza de Neve` (eliminando qualquer texto em inglês ou kanji japonês/chinês)
  - [x] Metatags OpenGraph (`og:title`, `og:site_name`), Twitter Cards e `apple-mobile-web-app-title` atualizadas para `Planeta Limpa-Neve 3D`
  - [x] Banner principal do menu de seleção (`.select-title`), logotipo da HUD no topo esquerdo (`.brand-logo`), resumo da partida e guia de comandos atualizados para `Planeta Limpa-Neve`
  - [x] Manifesto PWA (`public/site.webmanifest`) e Schema.org JSON-LD sincronizados com o nome em português
  - [x] Log do servidor Node.js atualizado para `Planeta Limpa-Neve 3D`
- [x] Traduzir Menu Inicial e Seleção de Pilotos (cabeçalhos, badges, cartas de pilotos, botões de ação e explicações)
- [x] Traduzir Contagem Regressiva e Subtextos de Tutorial ("3 · 2 · 1 · Já!")
- [x] Traduzir HUD Superior (Esquerdo, Central e Direito: Biomas, Placar, Painel de Conquistas, Chefes, Controles)
- [x] Traduzir HUD Inferior (Deck de Melhorias de Arado e Velocidade, Botões de Esmagar/Contra-Ataque e Habilidades Especiais)
- [x] Traduzir Modais (Resumo da Partida / Relatório do Estágio e Sala Multijogador Co-Op)
- [x] Traduzir Textos e Efeitos Dinâmicos no Motor JavaScript (Popups de combate, estados de chefes, tiers de equipamentos, toasts, tags de amigos)
- [x] Traduzir Fallbacks e Mensagens do Servidor WebSocket (`server.ts` — "Piloto X")
- [x] **Novos Nomes Oficiais dos 4 Pilotos**:
  - [x] 🦊 **Jhony** (Piloto 0 / Espiral da Raposa)
  - [x] 🐻 **Kercio** (Piloto 1 / Giga-Pisada)
  - [x] 🐰 **Jusimar** (Piloto 2 / Arrancada Aurora)
  - [x] 🐸 **Tiago** (Piloto 3 / Vórtice do Sapo)
  - [x] Sincronização em `index.html`, `PILOT_CONFIGS`, menu inicial, modal multijogador e `server.ts`
- [x] **Desempenho Otimizado no Celular (30 FPS ⟷ 60 FPS)**:
  - [x] Limitador temporal com padrão em 30 FPS para manter o celular frio e poupar bateria
  - [x] Botão interativo `⚡ 30 FPS` / `⚡ 60 FPS` no menu superior e drawer mobile
  - [x] Pixel ratio adaptativo (1.25x no modo 30 FPS, até 2.0x no modo 60 FPS)
- [x] **Controles Mobile Nativos & Toque na Tela**:
  - [x] Analógico virtual reposicionado no canto inferior esquerdo (ergonomia com o polegar esquerdo) com rótulo tátil `🕹️ Mover`
  - [x] Botões de ação (**Esmagar** e **Especial**) e melhorias (**Arado** e **Velocidade**) posicionados no deck inferior para acesso confortável com o polegar direito
  - [x] Toque na metade direita da tela para esmagar com bola de neve; toque na metade esquerda para guiar o joystick
  - [x] Detecção dinâmica de touchscreen com classe `body.is-touch-device`
  - [x] Textos adaptados para toque (ex: `Toque / Esmagar`, `Botão Especial`, `Toque em Esmagar para contra-atacar`)
  - [x] Modal explicativo completo **🎮 Guia de Controles (Celular e Computador)** acessível no HUD
- [x] **Rotação de Tela e Orientação Fluida (Paisagem ⟷ Retrato)**:
  - [x] Escuta simultânea de eventos `resize`, `orientationchange`, `screen.orientation` e `visualViewport`
  - [x] Redimensionamento em múltiplas etapas (imediato, `requestAnimationFrame`, 100ms e 300ms) para compensar a animação nativa do navegador mobile
  - [x] Ajuste adaptativo do Campo de Visão 3D (`camera.fov` e `camera.aspect`): em modo retrato vertical o campo se expande dinamicamente para o planeta e o piloto não serem cortados; em modo paisagem horizontal a vista cinematográfica de 50° é preservada
  - [x] Suporte a entalhes e recortes (`viewport-fit=cover` e `env(safe-area-inset-*)`) protegendo o joystick, o dock e o menu de botões contra notches e barras de gestos
  - [x] Regras de CSS dedicadas para smartphone na horizontal (`orientation: landscape` e `max-height: 540px`) mantendo menus compactos sem transbordamento
  - [x] Rastreamento contínuo de arrasto do polegar esquerdo via `pointermove` e `pointerup` globais
- [x] **Prontidão Completa para Publicação na Vercel**:
  - [x] Criar arquivo de configuração `vercel.json` (Framework Vite, rewrites de SPA para `/index.html`, headers de segurança e cache imutável de 1 ano para assets estáticos)
  - [x] Criar ícone vetorial temático acolhedor `public/favicon.svg` (trator limpa-neve, domo de neve e estrelas)
  - [x] Criar manifesto de aplicativo web `public/site.webmanifest` para instalação como PWA (tela inicial iOS e Android)
  - [x] Criar arquivos de indexação `public/robots.txt` e `public/sitemap.xml`
  - [x] Atualizar cabeçalho de `index.html` com `lang="pt-BR"`, tags de Web App móvel e Schema.org JSON-LD para jogos
  - [x] Atualizar `vite.config.ts` com `fileURLToPath` para compilação moderna e limpa sem warnings
  - [x] Tornar o sistema de Multiplayer e WebSocket resiliente no Vercel (fallback silencioso para Solo & Bots, reconexão com backoff exponencial sem travamentos ou flood de console)
  - [x] Adicionar opções no modal multijogador para conectar a servidores externos de WebSocket na nuvem (ex: Render, Railway, Fly.io) e compartilhamento automático via link `?ws=...`
  - [x] Criar guia completo de publicação em português (`VERCEL.md`) com tutorial passo a passo via interface web e Vercel CLI

---

## Novas Ideias para o Futuro (Backlog de Ideias)

- [ ] **Badge Dinâmico na Aba do Navegador**: Exibir contador de bolas de neve ou pontuação no título da aba enquanto a aba estiver em segundo plano (ex: `(⚪ 4.5m) Planeta Limpa-Neve 3D`).
- [ ] **Efeito Sonoro de Entrada na Neve**: Som acolhedor ao iniciar uma nova partida no planeta.
- [ ] **Service Worker Offline (PWA Completo)**: Armazenar assets do jogo em cache para permitir jogar 100% offline (em aviões ou sem conexão à internet).
- [ ] **Web Share API Nativa**: No celular, acionar o menu nativo de compartilhamento do sistema operacional (WhatsApp, Telegram, etc.) ao clicar em "Convidar Amigo".
- [ ] **Vercel Web Analytics & Speed Insights**: Adicionar script opcional de telemetria de performance da Vercel para monitorar taxas de FPS e tempo de carregamento em diferentes modelos de celulares.
- [ ] **Modo Tela Cheia Imersivo**: Botão no menu mobile para alternar para fullscreen nativo (`requestFullscreen`) ocultando a barra de navegação do browser.
- [ ] **Controle Opcional por Giroscópio**: Opção experimental de inclinar o aparelho para guiar a direção do limpa-neve pelo planeta esférico (`deviceorientation`).
- [ ] **Feedback Tátil Háptico (Vibração)**: Acionar `navigator.vibrate([20])` ao esmagar bola de neve e contra-atacar chefes no celular.
- [ ] **Modo Canhoto**: Opção no menu para inverter o analógico (para a direita) e botões de ação (para a esquerda).
- [ ] **Calibração de Zona Morta (Deadzone)**: Ajuste de tolerância e sensibilidade no analógico virtual para toques rápidos.
- [ ] **Modo Bateria Ultra**: Opção de desativar pós-processamento pesado e reduzir densidade de partículas de neve para smartphones de entrada.
- [ ] **Seletor de Idiomas Dinâmico**: Adicionar alternador de idiomas no menu de configurações (PT-BR / EN / JA) sem recarregar a página.
- [ ] **Falas e Reações Dubladas / Textuais**: Balões de quadrinhos com frases curtas de cada piloto (ex: Jhony dizendo "Fogo!", Kercio dizendo "Sai da frente!", Jusimar dizendo "Velocidade total!", Tiago dizendo "Salto mortal!").
- [ ] **Biomas Brasileiros / Temas Especiais**: Adicionar um bioma temático comemorativo com estética invernal mista (ex: "Geada da Serra").
- [ ] **Efeitos Sonoros de Voz Procedural**: Síntese de áudio para contagem regressiva em português com tons de sintetizador ("Três... Dois... Um... Já!").
- [ ] **Placar Global de Recordes**: Persistência de melhores pontuações de jogadores locais e da sala para competir em tempo real.
- [ ] **Modo Foto / Cartão Postal**: Permitir pausar a cena, remover a interface e gerar um cartão postal estilizado com carimbo do planeta limpo para download.
