# 🎨 Guia de Estilo, Princípios e Templates Pessoais

Este guia reúne a filosofia de design, princípios de escrita minimalistas, templates padrão de apresentação pessoal ("quem sou eu") e comandos Marp utilizados pelo Diego Borges.

---

## 🎯 Filosofia e Princípios de Escrita

- **Minimalismo Extremo**: "Menos é mais". Evite paredes de texto.
- **Uso Estrito de Bullets**:
  - **NÃO use bullets para frases soltas ou citações.**
  - Use bullets (`-`) **EXCLUSIVAMENTE** para listas reais (coleções de itens, comparações ou critérios).
- **Slides de Impacto (Frases & Citações Isoladas)**:
  - Citações de autores (Martin Fowler, Rebecca Parsons, Uncle Bob, Tony Robbins) e frases de efeito fortes devem ficar isoladas em **slides de impacto dedicados**, com títulos de destaque ou blocos de citação (`>`), sem listas ou marcadores.
- **Visual sobre Textual**: Prefira imagens, diagramas HTML, cards e ícones (✅, 🚀, 💡, ⚠️).
- **Uma Ideia por Slide**: Cada slide comunica estritamente um único conceito.
- **Suporte à Fala**: Os slides complementam o discurso verbal, sem substitui-lo ou repetir parágrafos.


---

## ⚙️ Configuração Padrão Marp

Sempre inicie os arquivos Markdown de slide com o cabeçalho:

```markdown
---
marp: true
theme: eudiegoborgs
paginate: true
---
```

---

## 👤 Template Padrão: Slide "Quem Sou Eu" (Apresentação Pessoal)

```markdown
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
```

---

## 📞 Template Padrão: Slide de Contato e Agradecimento

```markdown
### E você, o que acha?
## Obrigado
_`@eudiegoborgs`_
```

---

## 🔧 Comandos Úteis (Marp CLI)

### Gerar HTML
```bash
marp nome-da-apresentacao/nome-da-apresentacao.md --html --theme-set ./eudiegoborgs.css
```

### Gerar PDF
```bash
marp nome-da-apresentacao/nome-da-apresentacao.md --pdf --theme-set ./eudiegoborgs.css --allow-local-files
```

### Preview em Tempo Real (Watch Mode)
```bash
marp -w -s nome-da-apresentacao/nome-da-apresentacao.md --theme-set ./eudiegoborgs.css
```
