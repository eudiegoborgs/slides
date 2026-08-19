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

# Nenhum framework substitui o entendimento do seu problema.
## O framework dá a estrutura; você define as premissas e os limites da solução.

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
