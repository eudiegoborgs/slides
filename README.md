# 🎤 Apresentações em Marp

Este repositório contém minhas apresentações feitas com [Marp](https://marp.app/), utilizando o tema customizado `eudiegoborgs.css`.

## 📂 Estrutura do repositório

Cada apresentação está organizada em sua própria pasta com a seguinte estrutura:

``` 
eudiegoborgs.css # Tema
nome-slide/
├── nome-slide.md # Arquivo Markdown com os slides
└── assets/ # (opcional) Imagens e arquivos auxiliares
```

## 🧪 Pré-requisitos

- [Node.js](https://nodejs.org/) instalado
- Marp CLI globalmente instalado:

```bash
npm install -g @marp-team/marp-cli
```

## 🚀 Como gerar uma apresentação

Use o comando abaixo para compilar sua apresentação em HTML:

```bash
marp {nome-slide}/{nome-slide}.md --html --theme-set ./eudiegoborgs.css
```

### Exemplo:
```
bash
marp apresentacao-phpmg/apresentacao-phpmg.md --html --theme-set ./eudiegoborgs.css
````

Isso irá gerar um arquivo HTML visualizável no navegador com o tema customizado.

## 🎨 Tema personalizado
O tema eudiegoborgs.css contém a identidade visual usada nas apresentações. Você pode ajustá-lo livremente para alterar fontes, cores, espaçamentos, etc.

## 🧑‍💻 Autor
Diego Borges — @eudiegoborgs
Tech Manager, entusiasta de comunidade, palestrante e defensor de código limpo.

---

Sinta-se à vontade para clonar, usar como base e adaptar para suas próprias apresentações.
