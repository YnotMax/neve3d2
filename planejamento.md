# Planejamento — Cozy Plow (雪かき惑星) em Português do Brasil & Otimização Mobile

## 1. Visão Geral e Objetivo
Oferecer uma experiência acolhedora, 100% traduzida em Português do Brasil (PT-BR), com 4 novos pilotos carismáticos (**Jhony**, **Kercio**, **Jusimar** e **Tiago**), além de uma jogabilidade impecável em dispositivos móveis (smartphones Android e iOS), com controle ergonômico por toque, guia contextual, seletor de taxa de quadros (30 FPS econômico/estável por padrão, com opção de 60 FPS) e **acompanhamento dinâmico de rotação de tela (modo vertical e horizontal)**.

---

## 2. Decisões Confirmadas com o Usuário [EXECUTADAS]

1. **Personagens Renomeados**:
   - 🦊 **Jhony** (Piloto 0 / Raposa de Fogo) — Habilidade: Espiral da Raposa
   - 🐻 **Kercio** (Piloto 1 / Urso Escavadeira) — Habilidade: Giga-Pisada
   - 🐰 **Jusimar** (Piloto 2 / Coelho Planador) — Habilidade: Arrancada Aurora
   - 🐸 **Tiago** (Piloto 3 / Sapo do Vórtice) — Habilidade: Vórtice do Sapo
2. **Desempenho no Celular (30 FPS ⟷ 60 FPS)**:
   - Padrão em 30 FPS para estabilidade térmica, evitando que o celular esquente e poupando bateria.
   - Botão rápido de alternância no HUD e gaveta mobile para 60 FPS quando o usuário preferir máxima fluidez.
   - Ajuste adaptativo do `pixelRatio` (1.25x no modo 30 FPS, até 2.0x no modo 60 FPS).
3. **Controles Mobile e Dicas Contextuais de Tela**:
   - Detecção dinâmica de dispositivo com toque (`ontouchstart` / touchscreen).
   - Joystick virtual analógico posicionado no canto **inferior esquerdo** (ergonomia para o polegar esquerdo).
   - Botões de ação (**Esmagar** e **Especial**) e melhorias (**Arado** e **Velocidade**) acessíveis com o polegar direito.
   - Substituição automática de dicas de teclado (`[Espaço]`, `[E]`, `[1]`, `[2]`, `[Enter]`) por instruções de toque nativas no celular.
   - Painel explicativo de controles ("Como Jogar no Celular e no Computador").
4. **Comportamento ao Girar o Celular (Orientação Retrato ⟷ Paisagem)**:
   - Redimensionamento imediato e em estágios (com rAF e timeouts de 100ms e 300ms) ao detectar `orientationchange`, `screen.orientation` ou `resize`.
   - Câmera 3D inteligente com **FOV Adaptativo**: em modo vertical (retrato), o campo vertical se expande para manter o planeta esférico e os corredores visíveis sem cortes; em modo horizontal (paisagem), a visão panorâmica cinemática é preservada.
   - Isolamento de entalhes (notches) e gestos do sistema operacional através de `viewport-fit=cover` e `env(safe-area-inset-*)`.
   - Layout compacto para modo paisagem (`@media (orientation: landscape) and (max-height: 540px)`).

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
- **Posicionamento do Analógico**:
  - Ancorado no canto inferior esquerdo (`left: max(16px, env(safe-area-inset-left))` com rótulo tátil `🕹️ Mover`).
  - Suporte a arrasto contínuo com escuta global de ponteiro (`window.pointermove`).
- **Interação na Tela 3D**:
  - Metade esquerda da tela (46% da largura) direciona o analógico sem disparar ações acidentais.
  - Metade direita da tela dispara o arremesso de bola de neve (Esmagar / Contra-Ataque).
  - Botões dedicados no deck inferior (`#dash-attack-btn` e `#ability-btn`) com touch responsivo imediato.
- **Instruções Adaptativas**:
  - Dicas de teclas de computador ocultadas no mobile (`body.is-touch-device`).
  - Textos dinâmicos substituídos por ações de toque.
- **Modal de Controles**:
  - Botão `🎮 Controles` no HUD abrindo guia ilustrado com abas para Celular e Computador.

### Camada 4: Rotação de Tela & Adaptação de Orientação [CONCLUÍDO]
- **Listeners Abrangentes**: `resize`, `orientationchange`, `screen.orientation` e `visualViewport`.
- **Compensação de Animação do Browser**: Acionamento em cascata (0ms, rAF, 100ms e 300ms) para acomodar a animação de rotação em navegadores mobile (iOS Safari e Android Chrome).
- **FOV Adaptativo no Three.js**:
  - `aspect < 1.0` (retrato): `camera.fov = clamp(50 + (1.0 - aspect) * 16, 50, 62)`.
  - `aspect >= 1.0` (paisagem): `camera.fov = 50`.
- **Proteção de Safe Areas**:
  - `viewport-fit=cover` habilitado no `<meta name="viewport">`.
  - Espaçamentos e posições respeitando entalhes e barras de gestos na base (`env(safe-area-inset-*)`).
- **Layout Paisagem Otimizado**:
  - CSS dedicado para `@media (orientation: landscape) and (max-height: 540px)`.

---

## 4. Validação & Qualidade
- `compile_applet`: Compilação bem-sucedida sem erros.
- `lint_applet`: Validação TypeScript concluída com 100% de sucesso.
- Interface responsiva com layout fluido para telas móveis tanto em pé quanto deitadas.
