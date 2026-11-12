# 🦊 Raposa do Outono (Autumn Fox)

**Raposa do Outono** é um jogo de plataforma *endless runner* (corrida infinita) 2D construído para rodar nativamente no navegador. O projeto foi desenvolvido inteiramente com **HTML5 Canvas**, **CSS3** e **JavaScript puro (Vanilla JS)**, sem o uso de bibliotecas externas, motores de jogo (game engines) ou frameworks.

O jogador controla uma raposa que corre por uma floresta outonal gerada proceduralmente, coletando moedas de folhas douradas, desviando de abismos, saltando sobre inimigos e ativando *power-ups* especiais.

---

## ✨ Funcionalidades do Jogo

- 🌲 **Geração Procedural de Cenário:** Plataformas, vãos, moedas e inimigos são criados dinamicamente à medida que você avança, garantindo que cada partida seja única.
- 🦊 **Física e Movimentação Fluida:** Suporte a pulo duplo, aceleração suave, antecipação de câmera e mecânica de *Dash/Impulso*.
- ⚡ **Mecânicas Especiais e Power-ups:**
  - 🧲 **Ímã (`m`):** Atrai moedas próximas automaticamente para a raposa.
  - 🛡️ **Escudo (`s`):** Concede imunidade temporária contra colisões com inimigos.
  - ⚡ **Impulso (Dash):** Permite avançar rapidamente no ar ou no chão, derrotando inimigos no caminho.
  - 🔥 **Sistema de Combos:** Coletar moedas ou derrotar inimigos em sequência aumenta o multiplicador de pontuação (até 5x).
- 🔊 **Efeitos Sonoros Sintetizados (Web Audio API):** Áudios de pulo, aterrissagem, moedas, dano e game over gerados programaticamente em tempo real via código.
- 💾 **Persistência de Dados (`localStorage`):** Salva automaticamente o nome do jogador e os 10 maiores recordes (*High Scores*) no navegador.
- 📱 **Interface Adaptativa e Responsiva:** Ajuste automático de escala para qualquer resolução de tela (mantendo a proporção 16:9) com botões virtuais *Touch* para dispositivos móveis.

---

## 🎮 Controles

### 🖥️ Desktop (Teclado)
| Ação | Teclas |
| :--- | :--- |
| **Mover para Esquerda** | `←` (Seta Esquerda) ou `A` |
| **Mover para Direita** | `→` (Seta Direita) ou `D` |
| **Pular / Pulo Duplo** | `Espaço`, `↑` (Seta Cima) ou `W` |
| **Impulso (Dash)** | `Shift` ou `K` |
| **Pausar Jogo** | `P` ou `Esc` |

### 📱 Dispositivos Móveis (Touch)
- **Controles Virtuais:** Exibidos automaticamente em telas de toque na parte inferior da tela (`◀`, `▶`, `Pular` e `Impulso`).

---

## 🛠️ Arquitetura e Explicação do Código

Todo o jogo está contido em um único arquivo de alta performance, estruturado de forma modular através do JavaScript Vanilla:

### 1. Estrutura HTML e Layout (`#stage` e `<canvas>`)
* **`<div id="stage">`**: O container principal do jogo. Redimensiona dinamicamente a interface via JavaScript para manter a proporção **16:9** em qualquer tela.
* **`<canvas id="c">`**: Contexto 2D (`CanvasRenderingContext2D`) onde todos os elementos (cenário, partículas, raposa, moedas e inimigos) são renderizados a 60 FPS.
* **HUD (.hud)**: Camada de interface construída em HTML/CSS sobreposta ao Canvas para exibir estatísticas em tempo real (moedas, distância, recorde, vidas e status).
* **Controles Touch (`#touch`)**: Camada de botões virtuais com gerenciamento de eventos `pointerdown` / `pointerup`.

### 2. Ciclo de Vida e Loop Principal (`frame` e `update`)
* **`frame(now)`**: Função do loop principal chamada via `requestAnimationFrame`. Calcula o delta time (`dt`) para garantir que o jogo rode na mesma velocidade independente da taxa de atualização do monitor.
* **`update(dt)`**: 
  * Processa a física escalar (gravidade, aceleração horizontal e atrito).
  * Executa a detecção de colisões AABB (*Axis-Aligned Bounding Box*) com as plataformas e limites da tela.
  * Gerencia estados como tempo de *coyote time* (tolerância para pulos no limite de plataformas) e *jump buffering*.
  * Atualiza a posição da câmera com interpolação suave (`lerp`).

### 3. Geração Procedural (`gen`)
* A função `gen()` monitora a posição atual da câmera e constrói novas plataformas, inimigos e padrões de moedas antes que o jogador alcance o final da tela visível.
* Remove objetos que já ficaram para trás (`cam - 300px`) para liberar memória.

### 4. Renderização Canvas 2D (`draw...`)
* **`drawBG()`**: Desenha o fundo com gradientes dinâmicos, partículas de poeira estelar e colinas em **Parallax** (múltiplas camadas movendo-se em velocidades diferentes para criar efeito de profundidade).
* **`drawFox()`**: Constrói a raposa usando rotinas nativas de desenho (`arc`, `ellipse`, `bezierCurveTo`). Aplica animações de inclinação ao pular, esticamento/esmagamento (*squash & stretch*) e balanço da cauda.
* **`drawParts()`**: Sistema de partículas leve responsável pelo efeito visual de poeira ao correr/aterrissar e folhas caindo no vento.

### 5. Áudio Sintetizado (`Web Audio API`)
* A função `tone()` utiliza o `AudioContext` nativo do navegador para criar osciladores (`sine`, `square`, `sawtooth`, `triangle`) e rampas de frequência envelope. Não há necessidade de download de arquivos externos de áudio.

### 6. Persistência (`store`)
* O objeto `store` encapsula as chamadas de `localStorage.getItem` e `localStorage.setItem` com tratamento de exceção em `JSON.parse`, armazenando as pontuações da sessão.

---

## 🚀 Como Executar o Projeto

Como o jogo utiliza exclusivamente tecnologias nativas da Web, não é necessário instalar dependências (Node.js, npm, etc.).

### Execução Direta
1. Clone este repositório:
   ```bash
   git clone https://github.com/SkylineNando/GAME-HTML5-Canvas-CSS3-e-JavaScript-puro-Vanilla-JS-/tree/main
   ```
2. Abra a pasta do projeto e execute o arquivo HTML diretamente em qualquer navegador moderno.

### Execução via Servidor Local (VS Code)
1. Abra a pasta no **VS Code**.
2. Clique com o botão direito no arquivo `index.html` e selecione **"Open with Live Server"**.

---

🎮 Demonstração do Projeto

🌐 CLIQUE AQUI PARA JOGAR E VISUALIZAR A DEMONSTRAÇÃO https://skylinenando.github.io/GAME-Raposa-do-Outono-Autumn-Fox

## 📝 Licença

Este projeto está sob a licença [MIT](LICENSE) — sinta-se à vontade para utilizar, estudar e modificar o código.
