# Lista de Tarefas (TODO) — Tradução e Melhorias Cozy Plow (PT-BR)

## Tarefas Concluídas

- [x] Criar arquivo de planejamento detalhado (`planejamento.md`)
- [x] Criar lista de acompanhamento (`todo.md`)
- [x] Traduzir metadados e tags HTML (`<title>`, `<meta>`, OpenGraph, Twitter Cards, `metadata.json`)
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

---

## Novas Ideias para o Futuro (Backlog de Ideias)

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
