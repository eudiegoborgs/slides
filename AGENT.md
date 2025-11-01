# 📝 Guia para Criação de Slides - AGENT.md

## 🎯 Filosofia dos Slides

Os slides deste repositório seguem uma abordagem **minimalista e objetiva**:

- **Menos é mais**: Evite paredes de texto
- **Visual sobre textual**: Prefira imagens, diagramas e ícones
- **Uma ideia por slide**: Cada slide deve comunicar um único conceito
- **Suporte à fala**: Os slides complementam o que você diz, não substituem

## ✍️ Princípios de Escrita

### 1. **Conteúdo Mínimo**
- Máximo de **3-5 palavras** por bullet point
- Máximo de **3-4 bullets** por slide
- Use frases curtas e impactantes
- Elimine artigos e conectivos desnecessários

### 2. **Estrutura Clara**
Cada apresentação deve ter:
- **Título** (1 slide): Nome da apresentação
- **Introdução** (1-2 slides): Quem sou e contexto rápido
- **Corpo** (5-10 slides): Conteúdo principal
- **Conclusão** (1-2 slides): Resumo e call-to-action
- **Contato** (1 slide): Informações de contato

> **📌 Importante**: Para os slides de apresentação pessoal ("quem sou eu") e contato final, use como referência a estrutura já definida na apresentação `ia-evolucao-do-trabalho/ia-evolucao-do-trabalho.md`. Esses slides seguem um padrão estabelecido com fotos pessoais e informações específicas.

### 3. **Formatação Marp**

#### Configuração Inicial
Sempre inicie o arquivo `.md` com:

```markdown
---
marp: true
theme: eudiegoborgs
paginate: true
---
```

#### Exemplo de Slide Título
```markdown
# Título da Apresentação
## Subtítulo ou contexto breve

---
```

#### Exemplo de Slide de Conteúdo
```markdown
# Tópico Principal

- Ponto chave 1
- Ponto chave 2
- Ponto chave 3

---
```

#### Exemplo de Slide com Imagem
```markdown
# Conceito Visual

![bg right:40%](assets/imagem.jpeg)

- Texto mínimo
- Deixe a imagem falar

---
```

#### Exemplo de Slide "Quem Sou Eu" (Padrão Estabelecido)
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

#### Exemplo de Slide de Contato (Padrão Estabelecido)
```markdown
### E você, o que acha?
## Obrigado
_`@eudiegoborgs`_
```

> **📌 Nota**: Consulte `ia-evolucao-do-trabalho/ia-evolucao-do-trabalho.md` para ver a implementação completa e as imagens utilizadas.

## 🎨 Boas Práticas Visuais

### Use Recursos Visuais
- **Imagens**: Prefira imagens de alta qualidade
- **Ícones**: Use emojis para destacar pontos (✅, 🚀, 💡, ⚠️)
- **Background**: Use `![bg](caminho)` para imagens de fundo
- **Colunas**: Use `![bg right:40%]` para dividir conteúdo

### Evite
- ❌ Parágrafos longos
- ❌ Listas com mais de 5 itens
- ❌ Texto em tamanho pequeno
- ❌ Informações que você pode simplesmente falar

## 📐 Estrutura de Arquivos

### Criando Nova Apresentação

1. Crie uma pasta com nome descritivo:
```bash
mkdir nome-da-apresentacao
```

2. Crie o arquivo markdown:
```bash
touch nome-da-apresentacao/nome-da-apresentacao.md
```

3. Crie pasta de assets se necessário:
```bash
mkdir nome-da-apresentacao/assets
```

4. Adicione imagens na pasta `assets/`

### Estrutura Esperada
```
nome-da-apresentacao/
├── nome-da-apresentacao.md
├── nome-da-apresentacao.html (gerado)
└── assets/
    ├── imagem1.jpeg
    ├── imagem2.png
    └── diagrama.svg
```

## 🔧 Comandos Úteis

### Gerar HTML
```bash
marp nome-da-apresentacao/nome-da-apresentacao.md --html --theme-set ./eudiegoborgs.css
```

### Gerar PDF
```bash
marp nome-da-apresentacao/nome-da-apresentacao.md --pdf --theme-set ./eudiegoborgs.css --allow-local-files
```

### Preview em Tempo Real
```bash
marp -w -s nome-da-apresentacao/nome-da-apresentacao.md --theme-set ./eudiegoborgs.css
```

## ✅ Checklist Antes de Finalizar

Antes de considerar uma apresentação pronta, verifique:

- [ ] Cada slide tem **no máximo 5 linhas de texto**
- [ ] Não há parágrafos, apenas bullets ou títulos
- [ ] As imagens estão na pasta `assets/`
- [ ] O tema `eudiegoborgs.css` está referenciado
- [ ] A apresentação tem slides de introdução e conclusão
- [ ] O arquivo HTML foi gerado e testado
- [ ] Os slides são legíveis em projetor (texto grande)
- [ ] Cada slide comunica **uma ideia clara**

## 💡 Exemplos de Transformação

### ❌ Evite (Muito Texto)
```markdown
# Gestão de Equipes

A gestão de equipes é um desafio complexo que envolve múltiplas 
habilidades incluindo comunicação efetiva, delegação de tarefas, 
resolução de conflitos e capacidade de motivar pessoas diferentes 
com objetivos distintos.
```

### ✅ Prefira (Minimalista)
```markdown
# Gestão de Equipes

- Comunicação clara
- Delegar com confiança
- Resolver conflitos
- Motivar pessoas

---
```

### ❌ Evite (Lista Longa)
```markdown
# Ferramentas que Uso

- Git e GitHub
- Docker e Kubernetes
- Jenkins e GitLab CI
- Terraform e Ansible
- Prometheus e Grafana
- Slack e Jira
- VSCode e IntelliJ
```

### ✅ Prefira (Agrupado e Visual)
```markdown
# Stack Principal

🔧 **DevOps**
- Docker • Kubernetes • Terraform

📊 **Observabilidade**
- Prometheus • Grafana

💬 **Colaboração**
- Git • Slack • Jira

---
```

## 🎯 Dicas Finais

1. **Teste em voz alta**: Apresente para si mesmo antes
2. **Menos slides, mais impacto**: Prefira 15 slides fortes a 30 fracos
3. **Histórias > Dados**: Use cases reais quando possível
4. **Interação > Leitura**: Slides devem provocar discussão
5. **Revisão**: Sempre elimine 30% do texto na primeira revisão

---

**Lembre-se**: Você é o protagonista, não os slides. Os slides são apenas apoio visual.
