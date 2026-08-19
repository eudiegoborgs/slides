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

# Trate o máximo de decisões como reversíveis.
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
