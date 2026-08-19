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

# Agentes Autônomos de Código em 2026

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🤖 Alta Produtividade</h3>
    <p>Escrevem arquivos, rodam testes e corrigem bugs sozinhos</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🎲 Saída Probabilística</h3>
    <p>Geram código plausível, não necessariamente correto ou seguro</p>
  </div>
</div>

---

# A IA não tem memória arquitetural.
## Sem limites, ela escolhe o caminho mais curto — violando camadas e criando acoplamento silencioso.

---

### Pedir no prompt "respeite a Clean Architecture" NÃO impede a erosão.
## Instruções em linguagem natural sofrem obsolescência e alucinação.

---

# Quando a IA Atua sem Delimitação de Escopo

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 30px;">
  <div style="background: rgba(255,107,107,0.1); border: 1px solid rgba(255,107,107,0.3); padding: 18px; border-radius: 8px;">
    <h3 style="color: #ff6b6b; font-size: 1rem;">🔥 Amazon Kiro</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Agente deletou e recriou ambiente produtivo durante incidente de 13h.</p>
  </div>
  <div style="background: rgba(255,107,107,0.1); border: 1px solid rgba(255,107,107,0.3); padding: 18px; border-radius: 8px;">
    <h3 style="color: #ff6b6b; font-size: 1rem;">💥 Claude Code</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Executou terraform destroy com estado desatualizado, apagando 2.5 anos de dados.</p>
  </div>
  <div style="background: rgba(255,107,107,0.1); border: 1px solid rgba(255,107,107,0.3); padding: 18px; border-radius: 8px;">
    <h3 style="color: #ff6b6b; font-size: 1rem;">⚠️ Replit Agent</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Deletou banco de produção durante janelas de freeze explícito.</p>
  </div>
  <div style="background: rgba(255,107,107,0.1); border: 1px solid rgba(255,107,107,0.3); padding: 18px; border-radius: 8px;">
    <h3 style="color: #ff6b6b; font-size: 1rem;">🚨 Cursor Plan Mode</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Ignorou instrução de "somente planejar" e deletou 70 arquivos de código.</p>
  </div>
</div>

---

# O problema não foi a IA falhar.
## Foi o escopo de execução não estar restrito fora dela.

---

# A Evolução do Papel do Engenheiro

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; opacity: 0.6;">
    <h3>❌ Ontem</h3>
    <p>Digitador de código e implementador manual de linhas</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border: 2px solid #6c63ff;">
    <h3>✅ Hoje</h3>
    <p>Arquiteto de soluções, pensador crítico e definidor de limites</p>
  </div>
</div>

---

# Como construir barreiras objetivas e automatizadas que impeçam a IA de quebrar nossas regras?

---

# O Conceito de Harness
## O Harness envolve o agente de IA com regras de segurança e verificações executáveis fora da IA.

---

# Onde o Modelo Entra no Harness

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🤖 Unidade Isolada de Execução</h3>
    <p>A LLM opera restrita pela caixa do Harness, sem acesso direto ou não autorizado ao ambiente</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #6c63ff;">
    <h3>🔄 Loop de Feedback Fechado</h3>
    <p>O Harness injeta o contexto, executa as verificações e devolve logs de erro objetivos para a IA refazer</p>
  </div>
</div>

---

# Spec-Driven Development (SDD) & Frameworks

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🛠️ O que o Framework Entrega</h3>
    <p>Estrutura genérica, orquestração de subagentes, fluxos de validação e gates de DoR/DoD</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #ffd43b;">
    <h3>🎯 Responsabilidade Humana</h3>
    <p>Definição das regras de negócio, limites de domínio e premissas específicas do produto</p>
  </div>
</div>

---

# SDD na Prática: Ecossistemas para Experimentar

<div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; margin-top: 30px;">
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #6c63ff; font-size: 1.1rem;">⚡ Superpowers</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Skills e workflows altamente modulares para delimitar ações de agentes</p>
  </div>
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #51cf66; font-size: 1.1rem;">🧪 TLC</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Especificação formal de contratos e verificação rigorosa pré-execução</p>
  </div>
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #ffd43b; font-size: 1.1rem;">🧬 Genesis</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Geração guiada por specs arquiteturais e isolamento de dependências</p>
  </div>
</div>
<p style="text-align: center; margin-top: 24px; font-size: 1rem; color: #8888a0;">Experimente no seu time: adote a ferramenta que melhor se conecta ao seu CI/CD</p>

---

# Redução Drástica de Tokens via SDD

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 30px;">
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #6c63ff;">🎯 Progressive Disclosure</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Injeta apenas a spec do módulo e interfaces, sem enviar o codebase inteiro</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #51cf66;">📦 Batches Atômicos</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">A spec divide o trabalho em sub-tarefas pequenas com consumo mínimo por prompt</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ffd43b;">🚫 Fim do Context Drift</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">DoR e DoD claros impedem a IA de explorar arquivos irrelevantes ou alucinar</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ff6b6b;">💰 Economia de Custo</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Menos idas e vindas de conversa = até 70% de redução no consumo de tokens</p>
  </div>
</div>

---

### Nenhum framework substitui o entendimento do seu problema.
## O framework dá a estrutura; você define as 
## premissas e os limites da solução.

---

> *"Fitness Function é qualquer mecanismo que fornece uma avaliação objetiva da integridade de uma característica arquitetural."*
>
> — **Rebecca Parsons (Building Evolutionary Architectures)**

---

# O Espectro de Verificação

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 30px;">
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #6c63ff;">Análise Estática & Segurança</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">PHPStan, Psalm, SonarQube, SAST, Snyk (Zero secrets e zero vulnerabilidades)</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #51cf66;">Testes de Unidade & Integração</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Garantia comportamental rápida em nível de método e serviços</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ffd43b;">Mutação & Contratos</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Infection PHP (quem testa os testes?) e Pact (contratos de API)</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ff6b6b;">Regras Arquiteturais</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Deptrac e PHPArkitect (Camada de Domínio isolada da Infraestrutura)</p>
  </div>
</div>

---

# Fitness Functions Não Convencionais

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 30px;">
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #6c63ff;">⚡ Teto de Latência (P95)</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Falha no CI se o endpoint ultrapassar 200ms em teste de carga</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #51cf66;">🛢️ Limite de Queries por Request</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Detector automático de N+1 queries no ORM durante integração</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ffd43b;">📦 Teto de Bundle Size</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Bloqueio se dependências inflarem o tamanho do artefato final</p>
  </div>
  <div style="background: #1a1a2e; padding: 18px; border-radius: 8px;">
    <h4 style="color: #ff6b6b;">🌱 Eficiência Energética</h4>
    <p style="font-size: 0.95rem; margin-top: 6px;">Medição de consumo de CPU/pegada de carbono por transação</p>
  </div>
</div>

---

# O Ciclo Autônomo Protegido

### Agente gera o código ➔ Harness roda Fitness Functions
### Se falhar: Harness rejeita e devolve o erro para a IA corrigir
### Se passar: Merge seguro.

---

# A Divisão do Esforço de Revisão

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>🤖 Máquina (Harness)</h3>
    <p>Valida tipos, sintaxe, padrões de arquitetura, segurança e cobertura de testes</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border: 2px solid #51cf66;">
    <h3>🧠 Humano</h3>
    <p>Revisa intenção, alinhamento com a necessidade de negócio e valor entregue</p>
  </div>
</div>

---

# Arquitetura verificável é a única forma de garantir escalabilidade em times acelerados por IA.

---

# A Regra de Dependência em Camadas
## Camadas internas NUNCA dependem de camadas externas.
### *O Domínio comunica-se com o mundo exterior exclusivamente através de contratos.*

---

# O Valor do Isolamento de Camadas

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #51cf66;">
    <h3>🧪 Testabilidade Isolada</h3>
    <p>Testa o domínio sem subir banco de dados, HTTP ou serviços de terceiros</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-left: 4px solid #6c63ff;">
    <h3>🔄 Reversibilidade Tecnológica</h3>
    <p>Troca de framework ou banco de dados sem alterar uma linha da regra de negócio</p>
  </div>
</div>

---

# Two-Way Doors vs. One-Way Doors

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-top: 4px solid #51cf66;">
    <h3>🚪↔️ Two-Way Doors (Reversíveis)</h3>
    <p>Baixo custo de mudança. Feature Flags, BFF, abstração por interfaces e rollouts graduais.</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border-top: 4px solid #ff6b6b;">
    <h3>🚪➡️ One-Way Doors (Irreversíveis)</h3>
    <p>Alto custo de mudança. Escolha de linguagem/paradigma, schema de banco e fornecedor de nuvem.</p>
  </div>
</div>

---

### Trate o máximo de decisões como reversíveis.
## Abstraia dependências e mantenha as opções abertas pelo maior tempo possível.

---

# Desacoplamento Espacial & Temporal

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>📍 Espacial (Endereço)</h3>
    <p>O consumidor não conhece o endereço exato do produtor (BFF, Barramentos)</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px;">
    <h3>⏰ Temporal (Momento)</h3>
    <p>O produtor e o consumidor não precisam estar disponíveis ao mesmo tempo (Mensageria, Filas)</p>
  </div>
</div>

---

# Quando a arquitetura é bem isolada, o código gerado por IA torna-se modular e facilmente descartável ou substituível.

---

# Shu-Ha-Ri na Era da Inteligência Artificial

<div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; margin-top: 30px;">
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #6c63ff; font-size: 1.1rem;">守 (Shu) — Siga as Regras</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Usar o Harness e as Fitness Functions como guia rígido de conformidade</p>
  </div>
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #51cf66; font-size: 1.1rem;">破 (Ha) — Adapte</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Entender os trade-offs e flexibilizar limites conforme o contexto amadurece</p>
  </div>
  <div style="background: #1a1a2e; padding: 20px; border-radius: 8px;">
    <h3 style="color: #ffd43b; font-size: 1.1rem;">離 (Ri) — Crie</h3>
    <p style="font-size: 0.9rem; margin-top: 8px;">Evoluir a arquitetura e desenhar novos guardrails para a organização</p>
  </div>
</div>

---

# O Arquiteto como Guia Turístico

<div style="display: flex; gap: 40px; margin-top: 40px;">
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; opacity: 0.6;">
    <h3>❌ O Ditador Top-Down</h3>
    <p>Impõe regras arbitrárias sem explicação e cria dependência no time</p>
  </div>
  <div style="flex: 1; background: #1a1a2e; padding: 24px; border-radius: 12px; border: 2px solid #51cf66;">
    <h3>✅ O Guia e Guardião</h3>
    <p>Mostra o caminho, ensina os porquês e constrói a automação que protege o time</p>
  </div>
</div>

---

### Use a IA como alavanca de velocidade e 
### a arquitetura como direção de precisão.
## Ferramentas geram código; 
## engenheiros constroem sistemas duradouros.

---

### E você, o que acha?
## Obrigado
_`@eudiegoborgs`_
