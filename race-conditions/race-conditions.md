---
marp: true
theme: eudiegoborgs
paginate: true
---

## oi, eu sou o Diego
<div class="self-image">

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

<div class="family-image">

![Familia](./assets/familia.jpeg)

</div>
<div class="team-image">

![equipe](./assets/equipe.jpeg)

</div>

---

### Quando o sistema corre mais rápido que a lógica! 
# Entendendo e prevenindo Race Conditions

---

_Softwares são feitos do mesmo material dos sonhos, a mente humana, mas são executados no mundo físico, com as limitações que o mundo físico impõe._

## - Uncle Bob, Arquitetura Limpa.

---

## O Problema do Acoplamento

_O acoplamento é um problema do mundo físico que depende de **espaço e tempo** e race condition é o efeito colateral de um acoplamento temporal, a necessidade de algo ser execudado na ordem correta ou em um momento especifico._

<div class="horizontal-align">
<div>

💡 **Realidade:**
- É **impossível** não ter acoplamento
- Todo sistema tem dependências
- Race conditions surgem do acoplamento temporal

</div>
<div>

🎯 **O ideal:**
- Ter o **acoplamento adequado**
- No lugar certo
- Com as ferramentas certas

</div>
</div>

Não existe software sem acoplamento.

---

## Tipos de Acoplamento

<div class="horizontal-align">
<div>

### 🔴 Acoplamento Ruim
- Implícito
- Não documentado
- Sem proteção
- Estados compartilhados

</div>
<div>

### 🟢 Acoplamento Adequado
- Explícito
- Documentado
- Protegido

</div>
</div>

---

## O Problema do Acoplamento

_O race condition é o efeito colateral de um acoplamento temporal, a necessidade de algo ser execudado na ordem correta ou agora_

<div class="horizontal-align">
<div>

💡 **Realidade:**

- É **impossível** não ter acoplamento
- Todo sistema tem dependências
- Race conditions surgem do acoplamento temporal

</div>
<div>

🎯 **O ideal:**

- Ter o **acoplamento adequado**
- No lugar certo
- Com as ferramentas certas

</div>
</div>

---

## Tipos de Acoplamento

<div class="horizontal-align">
<div>

### 🔴 Acoplamento Ruim

- Implícito
- Não documentado
- Sem proteção
- Estados compartilhados

</div>
<div>

### 🟢 Acoplamento Adequado

- Explícito
- Documentado
- Protegido

</div>
</div>

---

## O Que São Race Conditions?

- Duas ou mais operações competem  
- O resultado depende da ordem
- Quem chega primeiro muda tudo

---

## Exemplo do Dia a Dia

**A conta da sua loja favorita tem um saldo de R$ 1.000**

Simultaneamente:

- Cliente 1 faz uma compra de **R$100**
- Cliente 2 faz uma compra de **R$1000**
- Funcionario paga **R$500** ao fornecedor

**Resultado esperado**: Saldo de **R$1600**

**Parece tudo bem, certo?**

---

### Código que faz o controle de saldo da conta

```php
// Três requests simultâneas com 100, 1000 e -500
function changeBalance(int $amount): boolean {
    $currentBalance = $this->repo->getBalance();
    $newBalance = $currentBalance + $amount;
    
    if ($newBalance >= 0) {
        $this->repo->setBalance($newBalance);
        return true;
    }
    return false;
}
```

---

## Como isso aconteceu?

<div class="horizontal-align">
<div>

**1. Leitura simultânea**
- A lê: saldo = 1000
- B lê: saldo = 1000
- C lê: saldo = 1000

</div>
<div>

->

</div>
<div>

**2. Processamento independente**
- A: 1000 + 100 = 1100
- B: 1000 + 1000 = 2000
- C: 1000 - 500 = 500

</div>
<div>

->

</div>
<div>

**3. Escrita conflitante**

- A escreve: 1100 ❌
- B escreve: 2000 ❌
- C escreve: 500 ❌

</div>
</div>

---

## Exemplo do Dia a Dia

**A conta da sua loja favorita tem um saldo de R$ 1.000**

Simultaneamente:

- Cliente 1 faz uma compra de **R$100**
- Cliente 2 faz uma compra de **R$1000**
- Funcionario paga **R$500** ao fornecedor

**Resultado esperado**: Saldo de **R$1600**

**Resultado real**: O saldo ficou em **R$1100**, **R$500** ou **R$2000**

---

## Impactos Reais

<div class="horizontal-align">
<div>

💰 **Financeiro**
- Saques duplicados
- Cobranças múltiplas
- Saldo inconsistente

</div>
<div>

📦 **Estoque**
- Vender mais que a disponibilidade
- Reservas duplicadas

</div>
</div>

<div class="horizontal-align">
<div>

🎫 **Reservas**
- Assentos, quartos ou ingressos vendidos 2x
- Conflitos de disponibilidade

</div>
</div>

---

## Tipos de Race Conditions

<div class="horizontal-align">
<div>

**Read-Modify-Write** 📖✏️

- Ler valor
- Modificar
- Escrever de volta

</div>
<div>

**Check-Then-Act** ✅➡️

- Verificar condição
- Agir com base nela

</div>
<div>

**Time-of-Check to Time-of-Use (TOCTOU)** ⏱️

- Estado muda entre verificação e uso

</div>
</div>

---

_Em outubro de 2025 houve uma race condition que_
_impactou o mundo da internet por 15 horas_
## Você sabe do que eu to falando?

---

_Nos dias **19 e 20 de outubro**, a AWS enfrentou uma indisponibildiade de **15 horas**, causada por uma Race Condition no sistema de atualização de DNS's_


Foram 15 horas, muitas warrooms e crises que geraram um:
### impacto financeiro de US$ 75 milhões por hora

---

## Como isso aconteceu?

**Atores:**

- DNS Planner: gera novos planos de DNS.
- DNS Enactors: aplicam esses planos.

O planejamento aconteceu na ordem certa, o problema foi na aplicação do plano

---

## Como isso aconteceu?

- Um dos Enactors ficou lentíssimo e tentava aplicar um plano muito antigo.
- Outro Enactor aplicou um plano novo rapidamente.
- Ele então executou uma limpeza e excluiu planos antigos.
- O Enactor atrasado aplicou seu plano antigo depois da limpeza — sobrescrevendo o novo.
- A limpeza apagou esse plano antigo sobrescrito, deixando o endpoint sem IPs e impedindo novos updates.

---

## Solução 1: Locks Pessimistas 🔒

```php
// Três requests simultâneas com 100, 1000 e -500
function changeBalance(int $amount): boolean {
    DB::beginTransaction();
    
    // SELECT ... FOR UPDATE (trava registro)
    $currentBalance = $this->repo->lockForUpdate()->getBalance();
    $newBalance = $currentBalance + $amount;
    
    if ($newBalance >= 0) {
        $this->repo->setBalance($newBalance);
        DB::commit();
        return true;
    }
    DB::rollback();
    return false;
}
```

---

## Trade-offs: Lock Pessimista

<div class="horizontal-align">
<div>

**Vantagens** ✅
- Garante exclusividade total
- Evita conflitos de escrita
- Simples de implementar
- Previsível e consistente

</div>
<div>

**Desvantagens** ⚠️
- Performance reduzida (espera)
- Risco de deadlock
- Pode bloquear operações de leitura

</div>
</div>

**Quando usar:** Operações críticas (financeiro, estoque)

---

## Solução 2: Locks Otimistas ✨

```php
// Adiciona coluna "version" na tabela
function setBalance(int $id, int $balance, int $version): boolean {
    $affected = DB::update(
        'UPDATE accounts
            SET balance = ?, version = version + 1
            WHERE id = ? AND version = ?',
        [$balance, $id, $version]
    );
    
    if ($affected === 0) {
        throw new ConcurrencyException();
    }

    return true;
}
```

---

## Trade-offs: Lock Otimista

<div class="horizontal-align">
<div>

**Vantagens** ✅
- Sem bloqueio de leitura
- Melhor performance em baixa contenção
- Não gera deadlocks
- Escala melhor

</div>
<div>

**Desvantagens** ⚠️
- Requer lógica de retry
- Falha em alta concorrência
- Complexidade no código cliente
- Desperdício de processamento

</div>
</div>

**Quando usar:** Operações com baixa probabilidade de conflito

---

## Solução 3: Semáforo com Cache 🚦

```php
function processOrder(int $orderId): void
{
    $lockKey = "lock:order:{$orderId}";
    
    // Tenta adquirir o semáforo
    $acquired = Cache::add($lockKey, true, 30); // 30 segundos
    
    if (!$acquired) {
        throw new ProcessingInProgressException();
    }
    
    try {
        // Executa a operação crítica
        $this->process($orderId);
    } finally {
        // Libera o semáforo
        Cache::forget($lockKey);
    }
}
```

---

## Trade-offs: Semáforo com Cache

<div class="horizontal-align">
<div>

**Vantagens** ✅
- Funciona em ambiente distribuído
- Simples de implementar
- Sem dependência de banco
- Performance excelente

</div>
<div>

**Desvantagens** ⚠️
- Depende de cache disponível
- Timeout pode causar locks órfãos
- Não garante atomicidade total
- Requer tratamento de falhas

</div>
</div>

**Quando usar:** Operações distribuídas que não podem duplicar

---

## Solução 4: Operações Atômicas ⚛️

```php
// View counter - correct version
function incrementViews(int $postId): void
{
    // Atomic database operation
    DB::update(
        'UPDATE posts SET views = views + 1 WHERE id = ?',
        [$postId]
    );
}

// Redis - atomic operation
function incrementCache(string $key): int
{
    return Redis::incr($key); // Thread-safe
}
```

---

## Trade-offs: Operações Atômicas

<div class="horizontal-align">
<div>

**Vantagens** ✅
- Performance máxima
- Sem overhead de locks
- Simples de implementar
- Suporte nativo (DB/Redis)

</div>
<div>

**Desvantagens** ⚠️
- Limitado a operações simples
- Não serve para lógica complexa
- Depende de suporte do sistema
- Difícil de debugar

</div>
</div>

**Quando usar:** Incrementos, contadores, operações matemáticas simples

---

## Solução 5: Filas e Processamento Serial 📨

```php
// Request apenas enfileira
function requestWithdrawal(int $amount): void
{
    Queue::push(new ProcessWithdrawalJob([
        'accountId' => $this->id,
        'amount' => $amount
    ]));
}

// Worker processa um por vez
class ProcessWithdrawalJob
{
    public function handle(): void
    {
        // Processa sequencialmente
        // Sem race condition
    }
}
```

---

## Trade-offs: Filas e Processamento Serial

<div class="horizontal-align">
<div>

**Vantagens** ✅
- Elimina race conditions
- Desacopla processamento
- Retry automático
- Escalável horizontalmente

</div>
<div>

**Desvantagens** ⚠️
- Não é síncrono/instantâneo
- Adiciona latência
- Requer infraestrutura (queue)
- Complexidade operacional

</div>
</div>

**Quando usar:** Operações que podem ser assíncronas

---

## Race Conditions Distribuídas 🌐

**Múltiplos servidores agravam o problema**

- Lock local não funciona
- Cache local diverge
- Estado compartilhado = perigo

**Soluções:**
- Redis locks (distribuídos)
- Database transactions
- Message brokers (Kafka, RabbitMQ)

---

## Redis Distributed Lock

```php
function processPayment(int $orderId): void
{
    $lock = Cache::lock("payment:{$orderId}", 10);
    
    if ($lock->get()) {
        try {
            $this->process($orderId);
        } finally {
            $lock->release();
        }
    } else {
        throw new ProcessingInProgressException();
    }
}
```

---

## Idempotência: Primeira Linha de Defesa 🛡️

```php
function processPayment(int $orderId, string $idempotencyKey): PaymentResult
{
    $processed = Cache::get("payment:{$idempotencyKey}");
    
    if ($processed) {
        return $processed;
    }
    
    $result = $this->charge($orderId);
    
    Cache::forever("payment:{$idempotencyKey}", $result);
    return $result;
}
```

**Webhooks, APIs, pagamentos = sempre idempotente**

---

## Detecção de Race Conditions

🔍 **Como identificar:**

- Bugs intermitentes que "somem sozinhos"
- Problemas apenas em produção (alto tráfego)
- Testes passam, produção falha
- Inconsistências de dados
- Logs mostram eventos impossíveis

---

## Ferramentas de Detecção

<div class="horizontal-align">
<div>

**Testes de Carga** 🧪
- Artillery
- K6

</div>
<div>

**Análise Estática** 🔬
- PHPStan (detecta alguns casos)
- Psalm

</div>
<div>

**Monitoramento** 📊
- Logs estruturados
- Métricas de concorrência
- Alertas de inconsistência

</div>
</div>

---

## Quando Se Preocupar? 🤔

<div class="horizontal-align">
<div>

**Alto Risco** 🔴
- Transações financeiras
- Gestão de estoque
- Reservas/agendamentos
- Processamento de pagamentos

</div>
<div>

**Médio Risco** 🟡
- Contadores, estatísticas
- Cache de dados
- Sessões de usuário

</div>
<div>

**Baixo Risco** 🟢
- Logs, analytics
- Dados aproximados
- Features não críticas

</div>
</div>

---

## Trade-offs

<div class="horizontal-align">
<div>

**Performance vs Segurança**

- Locks pessimistas: Mais lento, mais seguro
- Locks otimistas: Mais rápido, pode falhar
- Sem locks: Muito rápido, pode corromper

</div>
<div>

**Complexidade vs Simplicidade**

- Operações atômicas: Simples
- Distributed locks: Complexo
- Filas: Meio termo

</div>
</div>

---

## Conclusão

_Race conditions são inevitáveis em sistemas concorrentes e devem ser observadas e tratadas com muito cuidado_

🎯 **Chaves:**
- Identifique operações críticas
- Use ferramentas adequadas
- Teste com carga real
- Monitore em produção

---

### E você, o que acha?
## Obrigado
_`@eudiegoborgs`_
