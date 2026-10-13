# Novos Pilotos (Jhony, Kercio, Jusimar, Tiago) & Otimização Mobile Completa

Atualização da identidade dos 4 pilotos do Cozy Plow e reformulação completa da experiência para dispositivos móveis, introduzindo controles por toque ergonômicos, textos contextuais para telas sensíveis ao toque e controle de taxa de quadros (30 FPS padrão para economia e estabilidade, com opção de 60 FPS).

---

## Revisão do Usuário & Decisões Confirmadas

> [!IMPORTANT]
> **Decisões confirmadas pelo usuário:**
> 1. **Atribuição dos Personagens**:
>    - 🦊 **Jhony** (Piloto 0 / Raposa de Fogo) — Habilidade: Espiral da Raposa
>    - 🐻 **Kercio** (Piloto 1 / Urso Escavadeira) — Habilidade: Giga-Pisada
>    - 🐰 **Jusimar** (Piloto 2 / Coelho Planador) — Habilidade: Arrancada Aurora
>    - 🐸 **Tiago** (Piloto 3 / Sapo do Vórtice) — Habilidade: Vórtice do Sapo
> 2. **Desempenho no Celular**: Padrão em 30 FPS para máxima estabilidade térmica e economia de bateria em smartphones, com botão de 1 toque no HUD para alternar para 60 FPS quando desejado.
> 3. **Controles Mobile Nativos**: Substituição completa de dicas de teclado (`[Espaço]`, `[E]`, `[1]`, `[2]`, `[Enter]`) por instruções táteis claras quando o usuário estiver no celular, além de aprimorar a sensibilidade do joystick virtual e botões táteis dedicados.

---

## 1. Visão Geral & Experiência de Jogo

- **Objetivo**: Permitir que qualquer jogador no celular consiga pilotar, arremessar bolas de neve, ativar habilidades e comprar melhorias de forma 100% natural com os dois polegares, sem ver atalhos de teclado que não existem no celular.
- **Público-Alvo**: Jogadores mobile em smartphones Android e iOS, mantendo a experiência desktop intacta via detecção de dispositivo/input.
- **Valor Principal**: Fluidez garantida, sem superaquecimento do celular (graças ao modo 30 FPS com limitação inteligente de resolução de renderização) e jogabilidade intuitiva com feedback visual responsivo.

---

## 2. Experiência do Usuário & Design Visual

### A. Layout Ergonômico para Telas de Toque
- **Polegar Esquerdo**: Joystick virtual analógico ancorado confortavelmente na parte inferior esquerda, com anel visual suave e resposta imediata de direção esférica.
- **Polegar Direito**: Botões de ação em formato acessível:
  - **Botão Esmagar (Arremesso de Bola de Neve)**: Grande, com indicador visual de dano e pulso luminoso quando um chefe estiver em preparação de golpe (contra-ataque).
  - **Botão Especial (Sobrecarga do Piloto)**: Posicionado acima do botão de ataque, com ícone temático e contagem regressiva clara.
  - **Botões Rápidos de Melhoria (Arado & Velocidade)**: Acessíveis no deck inferior com toque direto para comprar quando houver moedas estelares suficientes.

```
┌────────────────────────────────────────────────────────┐
│  [Jhony / Bioma]                     [30 FPS] [Menu ☰] │
│                                                        │
│                    [ CENA 3D ]                         │
│                                                        │
│                                                        │
│   (Analógico)                                (Especial)│
│       🕹️                                         ⚡    │
│  [Direcionar]                                [Esmagar] │
│                                                  💥    │
│   ✦ 120 Moedas    [Melhorar Arado]  [Melhorar Vel.]    │
└────────────────────────────────────────────────────────┘
```

### B. Textos Contextuais (Toque vs. Teclado)
- **Detecção Automática**: O jogo detecta se o dispositivo suporta toque (`ontouchstart` ou tela sensível ao toque).
- **No Celular**:
  - Em vez de `[Espaço] / Clique`, exibe `Toque para Esmagar`.
  - Em vez de `Tecla [E]`, exibe `Toque para Especial`.
  - Em vez de `Começar Limpeza [Enter]`, exibe um grande botão tátil `Começar Limpeza de Neve`.
  - Instruções da contagem: `Arraste para mover · Toque para esmagar`.
- **No Computador**: Mantém os atalhos de teclado convencionais (`[Espaço]`, `[E]`, `[Enter]`, `[1]`, `[2]`).

### C. Seletor de Taxa de Quadros (30 FPS ⟷ 60 FPS)
- Pílula elegante no menu de navegação e na gaveta mobile: `⚡ 30 FPS` / `⚡ 60 FPS`.
- Em 30 FPS: throttle temporal de renderização + limite de PixelRatio para 1.25x (evita renderizar em 3x/4x em telas Retina/OLED que consomem muita bateria).
- Em 60 FPS: taxa máxima nativa para aparelhos de alta performance.

---

## 3. Decisões Técnicas & Arquitetura

### Decisão 1: Identidade dos Pilotos
- Atualizar o array `PILOT_CONFIGS` e os elementos HTML correspondentes para refletir:
  - `Jhony` (Foxfire Spiral / Espiral da Raposa)
  - `Kercio` (Heavy Dozer / Giga-Pisada)
  - `Jusimar` (Aurora Glider / Arrancada Aurora)
  - `Tiago` (Vortex Drift / Vórtice do Sapo)
- Sincronizar o backend (`server.ts`) para usar os novos nomes nos canais de multijogador.

### Decisão 2: Motor de Taxa de Quadros (FPS Limiter)
- No loop principal `animate(nowMs)`:
  - Controlar o intervalo mínimo de renderização (`1000 / targetFps`).
  - Quando em modo 30 FPS, pular frames excedentes e limitar `renderer.setPixelRatio(Math.min(window.devicePixelRatio, 1.25))`.
  - Quando em modo 60 FPS, usar `Math.min(window.devicePixelRatio, 2.0)`.

```
┌─────────────────────────────────────────────────────────────────┐
│                       Fluxo de Animação                         │
└─────────────────────────────────────────────────────────────────┘
                               │
                      [ requestAnimationFrame ]
                               │
               Intervalo decorrido >= 1000/fps ?
                               │
                ├─── NÃO ───> Pular renderização gráfica
                │
               SIM
                │
                ├──> Atualizar Físicas & Entidades (Racers / Chefes)
                ├──> Atualizar Partículas & Joystick
                └──> renderer.render(scene, camera)
```

---

## 4. Etapas de Execução

1. **Atualização dos Pilotos**:
   - Modificar nomes, papéis e descrições no HTML do menu inicial (`#char-select-overlay`), cartões de seleção e `PILOT_CONFIGS` em `index.html`.
   - Atualizar a lista do modal multijogador e `server.ts`.
2. **Implementação do Controle de FPS (30/60 FPS)**:
   - Adicionar estado `targetFps = 30` (ou 60 se desktop).
   - Inserir botão de alternância no HUD superior e na folha mobile.
   - Adicionar controle de cadência no loop de renderização Three.js.
3. **Refinamento dos Controles e Textos Mobile**:
   - Ajustar textos e instruções de botões e tela inicial dependendo de suporte a toque.
   - Otimizar área de clique e resposta do analógico virtual.
4. **Validação & Testes**:
   - Executar `compile_applet` e `lint_applet`.
   - Atualizar `planejamento.md` e `todo.md` com as novas implementações.
