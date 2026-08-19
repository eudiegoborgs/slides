---
marp: true
theme: eudiegoborgs
paginate: true
---

# Arquitetura Evolutiva
## Como arquitetar software em tempos ágeis com IA

---

## oi, eu sou o Diego
<div style="position: absolute; top: 10vh; right: 0; width: 60vh; height: 60vh;">

![Diego Borges](./assets/diego.jpeg)

</div>

---

- mineiro, de `Belorizonti` **(oncovim)**
- pai do **Bryan**, do **Arthur** e da **Emily**
- esposo da **Stéfanny**
- **musico** de garagem
- **desenvolvedor** desde 2011
- tech manager de um **time incrível**
- e muitas outras coisas... 🍕🍰🍫🍖🌕🎸🚗🏍️🐶♾️

<div style="position: absolute; top: 10vh; right: 5vh; width: 300px;">

![Familia](./assets/familia.jpeg)

</div>
<div style="position: absolute; top: 50vh; right: 5vh; width: 300px;">

![equipe](./assets/equipe.jpeg)

</div>

---

# O Paradoxo do Código em 2026

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #51cf66;">
    <h3>⚡ Velocidade de Geração</h3>
    <p>Agentes geram código em segundos</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #ff6b6b;">
    <h3>🐢 Gargalo no Code Review</h3>
    <p>Humanos gastam horas revisando PRs</p>
  </div>
</div>

---

# Como acelerar com IA sem corromper a arquitetura e sem gastar horas revisando código?

---

> *"Arquitetura é o conjunto de decisões importantes e difíceis de serem mudadas no futuro."*
>
> — **Martin Fowler**

---

### ESTRUTURA DE PASTAS NÃO É ARQUITETURA
## É apenas organização de arquivos

---

## A arquitetura está na estrutura do serviço 
## e na sua interação com o ecossistema.
### *Como a escada e a planta baixa de uma casa.*

— **Uncle Bob (Arquitetura Limpa)**

---

### Toda decisão de arquitetura lida com complexidade

---

# Tipos de Complexidade

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🎯 Essencial</h3>
    <p>Inerente ao problema de negócio</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>💥 Acidental</h3>
    <p>Criada por decisões da solução</p>
  </div>
</div>

---

### Big Upfront Design (BUFD)
## Tomar decisões precoces no momento de menor entendimento gera rigidez e complexidade acidental.

---

### Enough Upfront Design (EUFD)
## Apenas a arquitetura necessária para começar.
## *Maximizar o número de decisões NÃO tomadas.* — Uncle Bob

---

> *"A mudança é inevitável, a evolução é opcional."*
>
> — **Tony Robbins**

---

> *"Uma arquitetura evolutiva suporta mudanças contínuas e incrementais como um primeiro princípio."*
>
> — **Rebecca Parsons**

---

### A arquitetura evolutiva não tenta prever o futuro.
## Ela prepara o sistema para coexistir de 
## forma saudável com as mudanças.

---
