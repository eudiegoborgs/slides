---
marp: true
theme: eudiegoborgs
paginate: false
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

### Workshop de 
## Arquitetura Evolutiva
_Construindo software que escala na hora certa_

---

### Importante:
_O conteúdo é denso e tem muitos tópicos importantes a serem explorados._
Dito isso:
- Se algo estiver repetitivo ou for mais do mesmo, levante a mão e caso + 70% do grupo concorde pulamos o tema
- Se não concluirmos o conteúdo hoje, agendaremos a apresentação restante online.

---

<!-- _class: lead -->

# O Que é Arquitetura?

**Definindo os fundamentos**

---

## Design vs Arquitetura

**Design** 🎨
- Como o código é organizado
- Padrões aplicados
- Estrutura local/detalhada

**Arquitetura** 🏗️
- Decisões estruturais principais
- Componentes e suas relações
- Impacto no sistema como um todo

---

## O Que NÃO É Arquitetura

❌ **Estrutura de pastas não é design nem arquitetura**

```
/src
  /application
  /domain
  /infrastructure
```

_Isso é apenas organização de arquivos!_

---

_"Arquitetura de software é um conjunto de decisões importantes e difíceis de serem mudadas no futuro"_

**Martin Fowler**

---

_"A mudança é inevitável, evolução, entretanto, é opcional"_

**Tony Robbins**

---

## Arquitetura de Software em um Cenário de Incertezas

**Desafios:**
- Requisitos mudam constantemente
- Tecnologias evoluem rapidamente
- Mercado é imprevisível
- Time em constante mudança

**Como construir algo duradouro em um mundo volátil?**

---

_"Uma arquitetura evolutiva suporta mudanças contínuas e incrementais como um primeiro princípio por meio de vários aspectos"_

**Rebecca Parsons**

---

## De Onde Vêm as Mudanças?

<div class="horizontal-align">
<div>

**Negócio** 📈
- Novos requisitos
- Pivots de produto
- Expansão de mercado

</div>

<div>

**Tecnologia** 💻

- Novas ferramentas
- Deprecated libraries
- Performance necessária
</div>

</div>

<div class="horizontal-align">

<div>

**Organização** 👥
- Crescimento do time
- Mudança de pessoas
- Novas habilidades

</div>

<div>

**Regulamentação** ⚖️
- LGPD, GDPR
- Compliance
- Auditorias

</div>

</div>

---

## A Pressão do Mercado nunca diminui
- Concorrência aumenta
- Usuários mais exigentes
- Time-to-market crítico
- Expectativas crescem

_Precisamos de arquiteturas que acelerem, não travem_

---

_"Uma arquitetura não deve apenas atender as demandas dos usuários, desenvolvedores e proprietários em um determinado momento, mas também corresponder a essas expectativas ao longo do tempo."_

**Uncle Bob (Robert Martin)**

---

## Complexidade Essencial vs Acidental

<div class="horizontal-align">
<div>

**Complexidade Essencial** 🎯
- Inerente ao problema
- Regras de negócio
- Domínio complexo
- **Não pode ser eliminada**

</div>
<div>

**Complexidade Acidental** 💥

- Criada pela solução escolhida
- Frameworks desnecessários
- Over-engineering
- **Pode e deve ser eliminada**

</div>

---

## Exemplo: Complexidade

**Essencial** 🎯
```
Calcular imposto baseado em:
- Localização do cliente
- Tipo de produto
- Legislação vigente
- Isenções aplicáveis
```

**Acidental** 💥
```
- Usar 5 design patterns para um CRUD simples
- Microserviços para 3 desenvolvedores
- Kafka para 100 mensagens/dia
```

---

## O Objetivo da Arquitetura

**Maximizar produtividade** ao longo do tempo

**Como?**
- Facilitar mudanças
- Reduzir complexidade acidental
- Permitir evolução incremental
- Manter opções abertas

_Arquitetura é sobre decisões que você pode adiar_

---

## Fitness Functions

**Como saber se a arquitetura está evoluindo na direção certa?**

---

## O que é uma Fitness Functions?

_Mecanismos objetivos que verificam características arquiteturais_

Assim como testes unitários verificam comportamento do código, **fitness functions verificam características da arquitetura**

_"Qualquer mecanismo que forneça uma avaliação objetiva da integridade de alguma característica arquitetônica."_ 
**Building Evolutionary Architectures - Rebecca Parsons**

---

## Por Que Fitness Functions?

**Problema:** Como garantir que a arquitetura não degrada ao longo do tempo?

**Cenários comuns:**
- Módulos que deveriam ser independentes começam a se acoplar
- Performance degrada gradualmente sem perceber
- Dependências circulares aparecem "sem querer"
- Limites de contexto são violados

**Fitness functions detectam isso automaticamente**

---

## Exemplos de Fitness Functions

**1. Acoplamento entre módulos**
```php
// PHPArkitect - Regras arquiteturais
public function testDomainNaoDependeDeInfraestrutura(): void
{
    $this->assertDoesNotDependOn(
        'App\Domain',
        'App\Infrastructure'
    );
}
```

---

## Exemplos de Fitness Functions

**2. Tamanho de classes**
```php
// PHP_CodeSniffer custom rule
public function testClassesNaoDevemExceder300Linhas(): void
{
    $files = glob(__DIR__ . '/../src/**/*.php');
    foreach ($files as $file) {
        $lines = count(file($file));
        $this->assertLessThan(300, $lines, 
            "Classe {$file} tem {$lines} linhas");
    }
}
```

---

## Exemplos de Fitness Functions

**3. Performance de endpoint**
```php
public function testEndpointDeveDemorarMenosDe200ms(): void
{
    $start = microtime(true);
    $response = $this->get('/api/products');
    $duration = (microtime(true) - $start) * 1000;
    
    $this->assertLessThan(200, $duration,
        "Endpoint demorou {$duration}ms");
}
```

---

## Exemplos de Fitness Functions

**4. Dependências circulares**
```php
// PHPArkitect - Detecta ciclos
public function testNaoDeveHaverDependenciasCirculares(): void
{
    $this->assertDoesNotHaveCyclicDependencies([
        'App\\Domain',
        'App\\Application',
        'App\\Infrastructure'
    ]);
}
```

---

## Tipos de Fitness Functions

<div class="horizontal-align">
<div>

**Atômicas** 🎯
- Verificam uma única característica
- Exemplo: Tempo de resposta < 200ms

**Holísticas** 🌐
- Verificam múltiplas características
- Exemplo: Deploy completo com testes + segurança + performance

</div>

<div>

**Disparadas** ⚡
- Executam em eventos (commit, deploy, schedule)

**Contínuas** 🔄
- Monitoramento em produção (APM, logs, métricas)

</div>
</div>

---

## Ferramentas para Fitness Functions

- PHPArkitect - Regras arquiteturais como testes
- Deptrac - Análise de dependências entre camadas
- PHP_CodeSniffer - Padrões de código
- PHPStan/Psalm - Análise estática de tipos
- PHPMD - Métricas e complexidade
- SonarQube PHP - Qualidade e segurança

---

## Fitness Functions na Prática

**Integre ao CI/CD:**
1. Desenvolvedor faz commit
2. CI executa testes unitários ✅
3. CI executa fitness functions ✅
4. Se falhar, build quebra 🔴

**Resultado:** Violações arquiteturais são detectadas **antes** de chegar em produção

_Arquitetura se torna verificável, não apenas documentada_

---

# Tomada de Decisões Técnicas

---

### Antes de tudo...

## Comece pelo Problema

---

## 1. Entenda o Contexto

❌ **Não faça:**
_"Vamos usar microserviços!"_

✅ **Faça:**
_"Temos 3 devs, 100 usuários/dia, pouco dinheiro investido e precisamos entregar em um prazo curto... Monolito modular faz sentido agora"_

---

## Contexto Importa

**Pergunte:**
### Capacity
- Qual o tamanho do time?
### Impacto
- Quantos usuários?
### Prazo
- Qual a urgência/prazo?
### Escopo 
- O que é obrigatório? Quais as restrições?
- Qual o resultado esperado (MVP)?

---

## 2. Questione e explique o "Porquê"

_Proposito importa!_

❌ **Não faça:**
_"Precisamos migrar para Kubernetes"_

✅ **Faça:**
_"Por que precisamos de Kubernetes? Qual problema ele resolve?"_

---

## Os 5 Porquês
_Estresse o problema usando a técnica dos 5 porquês_

**Problema:** Deploy é lento

1. Por quê o deploy é lento? _Pipeline demora_
2. Por quê a pipeline demora? _Testes são lentos_
3. Por quê os testes são lentos? _Banco de teste é lento_
4. Por quê o banco de testes é lento? _Dados de produção_
5. Por quê usamos dados de produção? _Não temos fixtures_

_A proxima pergunta sempre usa a resposta anterior_

✅ **Solução real:** Criar fixtures, não refazer pipeline

---

## 3. Evite Soluções Prontas

❌ **Não faça:**
_"Netflix usa, vamos usar também"_

✅ **Faça:**
_"Netflix tem 10k+ devs e milhões de acessos simultaneos._
_Nós temos 5 devs e 100 usuários por dia. Não é o mesmo contexto"_

_Empresas grandes tem problemas diferentes, entenda o proposito de cada solução e adapte ao **SEU** contexto_

---

## 4. Problema Real vs. Imaginário

❌ **Não faça:**
- _"E se tivermos 1 milhão de usuários?"_ <small>(quando tem 100)</small>
- _"E se além de passagens aéreas vendermos passagens de trem?"_

---

## 4. Problema Real vs. Imaginário

✅ **Faça:**

- _"Hoje temos 100 usuários. O problema real é onboarding lento"_
- _"Hoje vendemos passagens aéreas. Como criamos uma solução que permita vender coisas sem depender do contexto? Devemos fazer isso agora?"_

---

## Foque no Presente

**✅ Problema Real:**

- Está acontecendo agora
- Impacta usuários hoje
- Tenha evidências e dados
- Solução orientada a problema

---

## Não Esteja Só

_"Tudo parece certo_
_até que alguém venha questionar. - **Provérbios 18:17**"_

- Busque perspectivas diferentes
- Code review como conversa
- Pair programming
- Decisões compartilhadas

---

## Três Tipos de Escalabilidade

**Código** 📝: _A complexidade da realização das tarefas é resultado de decisões arquiteturais?_

**Pessoas** 👥: _Novas pessoas são capazes de manter e evoluir seu projeto?_

**Carga** 📊: _O projeto se mantem disponivel quando a demanda por ele cresce?_

---

## Escalabilidade no Dia 0?

⚠️ **Cuidado com a armadilha**
_Escalabilidade no dia 0 é sobre time e código, nunca sobre carga_

---

## Código é Bagagem

_Vou usar Value Object e Command Bus nesse crud de cadastro de clientes._

**Resolutado: Código verboso sem resolver problema real**

- Mais código = mais manutenção
- Mais código = mais bugs
- Mais código = mais complexidade

**Pode parecer contra intuitivo, mas se preocupe menos código, e mais com o valor que ele entrega**

---

## A Equação da Entrega

**Escopo** ⚖️ **Qualidade** ⚖️ **Tempo**

- Se eu tenho menos tempo para fazer algo, devo reduzir o escopo ✅
- Nunca comprometer a qualidade ❌
- Redução de qualidade deve dar clareza dos riscos e ser assumida como débito <br/>_e débito cobra juros_

---

## Evite o HDD

**Hype Driven Development** _ou_ **DOL - Desenvolvimento Orientado a Legalzismo**

❌ Nova tech por ser "cool", sem maturidade e ecossistema
❌ Resolver problema inexistente causa complexidade acidental
❌ Ignorar custo de adoção e equipe despreparada

---

## Decisões Reversíveis
### Two way door 🚪↔️

_Reduz custo de mudança_

---

## Estratégias Reversíveis

**Use Feature Flags** 🎚️
- Liga/desliga sem deploy
- Teste em produção
- Rollback instantâneo

---

## Estratégias Reversíveis

**Testes A/B**
- Compare soluções
- Dados reais
- Decida com evidências

---

## Estratégias Reversíveis

**Rollout Incremental**

- Migração gradual
- Sistema antigo + novo
- Reverte facilmente

---

## Estratégias Reversíveis

**Desacoplamento e redução de dependencia**

- Cada contexto é enxuto e depende do essencial
- Mudanças em partes não impactam o todo
- Reverte facilmente

---

## Decisões Irreversíveis
### One way door 🚪➡️

_Alto custo de mudança_

---

## Como Lidar com Irreversível

**1. Documente tudo** 📝
- Por que decidiu?
- Quais as alternativas?
- Qual o trade-off?

**2. Busque consenso** 👥

- Envolva o time e valide riscos com stakeholders

**3. Faça PoC** 🧪
- Teste em pequena escala, valide hipóteses e meça riscos reais

---

## Dica de Ouro

💡 **Trate como reversível quando possível**

- Abstraia dependências
- Use interfaces
- Evite lock-in
- Mantenha opções abertas

_Mesmo o "irreversível" pode ser amenizado_

---

## Argumentação Efetiva

📊 **Dados** > Opiniões
🎯 **Fatos** > Achismos
🔍 **Contexto** > Abstração
💡 **Solução certa no tempo certo** > Solução perfeita

---

## Exemplo: Argumentação Ruim

❌ _"Precisamos migrar para microserviços porque é a melhor prática"_

**Problemas:**
- Sem dados
- Sem contexto
- Sem problema real
- Apenas opinião

---

## Exemplo: Argumentação Boa

✅ _Proposta: Modularizar em 4 serviços._
_Deploy leva 45min e impacta 3 times._
_Monorepo com 500k linhas._
_Trade-off: Complexidade operacional vs agilidade_

**Por quê funciona:**
- Dados concretos (45min, 3 times)
- Problema claro
- Solução específica
- Trade-offs explícitos

---

## Como Argumentar na Prática

**1. Apresente o problema**
_"Bugs em prod duplicaram no último mês"_

**2. Mostre dados**
_"15 bugs/mês → 30 bugs/mês. 70% em feature X"_

---

## Como Argumentar na Prática

**3. Explique trade-offs**
_"Adicionar testes: 2 dias + 10% mais lento CI"_
_vs_
_"Não fazer: bugs continuam, perda de confiança e aumento de custo de novas oportunidades"_

---

## Como Argumentar na Prática

**4. Proponha solução**
_"Adicionar testes E2E na feature X._
_Cobertura de 80% nos fluxos críticos"_

**5. Ouça feedback**
_"Equipe sugere começar com 50% e iterar"_

---

## Exemplo Real: Performance

❌ **Ruim:**
_"Sistema está lento, vamos usar cache"_

✅ **Bom:**
_"P95 latência: 800ms (SLA: 200ms)._
_80% das queries repetem em 5min._
_Redis cache: reduz para ~50ms._
_Custo: $50/mês + complexidade invalidação"_

---

## Exemplo Real: Refatoração

❌ **Ruim:**
_"Código está uma bagunça"_

✅ **Bom:**
_"Classe User: 2.5k linhas, 15 responsabilidades._
_PRs levam 3h+ review._
_Proposta: Extrair 5 classes por domínio._
_Reduz review para ~1h, melhora testes"_

---

## Evite Armadilhas

❌ Apelo à autoridade
_"Fulano famoso usa X"_

❌ Falsa urgência
_"Precisa ser AGORA"_

❌ Emoção sem dados
_"Eu acho que..."_

---

## Fortaleça Argumentos

✅ Use métricas
✅ Compare alternativas
✅ Mostre impacto no negócio
✅ Seja específico
✅ Admita limitações

---

## YAGNI

**You Aren't Gonna Need It**

_Você não vai precisar disso_

Quando NÃO é YAGNI?

_Quando tem proposito claro_

---

# Código de Qualidade

---

## Por Que Produzir um Código de Qualidade?

💰 **Custo de manutenção**
- 60-80% do tempo é manutenção
- Código ruim = lentidão constante

🐛 **Menos bugs**
- Código claro = menos erros

👥 **Onboarding mais rápido**
- Novos devs produzem mais rápido

---

## Código Limpo

### O Básico que Faz Diferença

---

## Nomes Revelam Intenção

❌ O que esse código faz?
```php
function calc($d, $t) {
    return $d * $t * 0.1;
}
```

---

## Nomes Revelam Intenção

✅ O que esse código faz?

```php
function calcularDescontoFidelidade($totalCompra, $tempoClienteAnos) {
    $percentualDesconto = 0.1;
    return $totalCompra * $tempoClienteAnos * $percentualDesconto;
}
```

---

## Funções Pequenas
### Single responsability
_Sua função deve ter apenas um motivo para mudar._ 

❌ **Não faça:**
- Função com 200+ linhas
- Faz validação, cálculo, persistência, email
- Impossível testar isoladamente

✅ **Faça:**
- Uma responsabilidade
- Fácil de testar e entender
- Se é dificil de testar, você tá fazendo errado

---

## Exemplo: Função Grande

❌ **Ruim:**
```php
function processarPedido($pedido) {
    // valida dados (30 linhas)
    // calcula frete (40 linhas)
    // aplica descontos (50 linhas)
    // gera nota fiscal (60 linhas)
    // envia email (20 linhas)
    // atualiza estoque (30 linhas)
}
```

---

## Exemplo: Função Pequena

✅ **Bom:**
```php
function processarPedido($pedido) {
    validarPedido($pedido);
    calcularValores($pedido);
    emitirNotaFiscal($pedido);
    notificarCliente($pedido);
    atualizarEstoque($pedido);
}
```

Cada função: 10-20 linhas, testável

---

## Comentários: Quando Usar?

❌ **Evite comentários óbvios:**
```php
// Define o nome do usuário
$usuario->setNome($nome);

// Retorna verdadeiro
return true;
```

✅ **Use para explicar "porquê":**
```php
// Workaround: API Pagamento retorna 500 após 3 tentativas
// Bug reportado: TICKET-1234. Remover quando corrigido
$maxTentativas = 2;

// Regex complexa para validar CPF com/sem formatação
// Fonte: Receita Federal - Portaria 123/2020
$pattern = '/^\d{3}\.?\d{3}\.?\d{3}-?\d{2}$/';
```

---

## Quando Abrir Mão?

⚠️ **Código limpo pode esperar:**
- Protótipo/PoC rápido
- Script descartável
- Prazo crítico (mas documente como débito!)

**Nunca abra mão em:**
- Código de produção
- Bibliotecas compartilhadas
- Lógica de negócio crítica

---

## Refatoração

### Melhorar Sem Quebrar

---

## O Que é Refatoração?

**Reestruturar código sem mudar comportamento**

✅ Melhorar legibilidade
✅ Reduzir complexidade
✅ Facilitar manutenção

❌ Não é: reescrever tudo
❌ Não é: adicionar features

---

## Técnicas de Refatoração

**Extract Method**
- Função grande → várias pequenas

**Rename**
- Nomes ruins → nomes claros

**Remove Duplication**
- DRY (Don't Repeat Yourself)

**Simplify Conditionals**
- IFs complexos → funções nomeadas

---

## Exemplo: Extract Method

❌ **Antes:**
```php
function calcularTotal($items) {
    $total = 0;
    foreach ($items as $item) {
        $total += $item->preco * $item->quantidade;
    }
    // aplicar desconto
    if ($total > 1000) {
        $total = $total * 0.9;
    }
    return $total;
}
```

---

## Exemplo: Extract Method

✅ **Depois:**
```php
function calcularTotal($items) {
    $subtotal = somarItems($items);
    return aplicarDesconto($subtotal);
}

function somarItems($items) {
    return array_reduce($items, function($sum, $item) {
        return $sum + $item->preco * $item->quantidade;
    }, 0);
}

function aplicarDesconto($valor) {
    return $valor > 1000 ? $valor * 0.9 : $valor;
}
```

---

## Quando Refatorar?

**Regrinha de escoteiro:**
_"Deixe o código mais limpo do que encontrou"_

✅ **Faça:**
- A cada feature
- No code review
- Quando adicionar testes
- Quando estiver difícil de entender

---

## Estratégia de Refatoração

1. **Tenha testes** ✅
2. **Pequenos passos** 🐾
3. **Commit frequente** 💾
4. **Um de cada vez** 1️⃣

_Sem testes = não é refatoração, é aventura_

---

## Quando NÃO Refatorar?

⚠️ **Evite:**
- Código sem testes (primeiro, adicione testes!)
- Véspera de release
- Código que será deletado
- Sistema legado crítico (use Strangler)

---

## Isolamento de Camadas

### Organize Seu Código

---

## Por Que Isolar Camadas?

🔄 **Mudança isolada**
- Troca banco sem mexer no domínio

🧪 **Testes mais fáceis**
- Mock da camada externa

📦 **Reutilização**
- Lógica não duplicada

---

## Arquitetura em Camadas

![Arquitetura em camadas](./assets/camadas.png)

---

## Exemplo: Sem Isolamento

❌ **Ruim:**
```php
function criarUsuario($request) {
    // valida request
    // conecta banco
    // salva dados
    // envia email
    // retorna response
    // tudo misturado!
}
```

**Problemas:**
- Impossível testar sem banco
- Troca de framework = reescrever tudo
- Lógica duplicada

---

## Exemplo: Com Isolamento

✅ **Bom:**

```php
// Camada Apresentação
class UserController {
    public function create(Request $request) { /* ... */ }
}

// Camada Domínio

class CreateUserUseCase {
    public function handle(User $user) { /* ... */ }
}

// Camada Infraestrutura
class UserRepository {
    public function save(User $user) { /* ... */ }
}
```

---

## Regra de Dependência

**Camadas internas NÃO dependem de externas**

✅ Domínio → independente
✅ Aplicação → depende do Domínio
✅ Infra → depende de tudo

❌ Domínio depender de Framework
❌ Domínio depender de Banco

_O dominio se comunica com o mundo através de contratos_

---

## Quando Usar Camadas?

✅ **Use quando:**
- Aplicação de médio/grande porte
- Múltiplas interfaces (web, API, CLI)
- Lógica de negócio complexa

⚠️ **Pode abrir mão:**
- CRUD simples
- Script pequeno
- Protótipo rápido

---

## Estratégia de Implantação

**Comece simples:**
1. Separe lógica de negócio da infra
2. Adicione camada de serviço
3. Isole repositórios
4. Refine conforme cresce

_Não precisa de Clean Architecture no dia 0_

---

## SOLID: Princípios Fundamentais

**S** - Single Responsibility Principle
**O** - Open/Closed Principle  
**L** - Liskov Substitution Principle
**I** - Interface Segregation Principle
**D** - Dependency Inversion Principle

_Base para código flexível e manutenível_

---

## S - Single Responsibility

**Uma classe deve ter apenas um motivo para mudar**

❌ **Ruim:**
```php
class User {
    public function save() { /* DB logic */ }
    public function sendEmail() { /* Email logic */ }
    public function generateReport() { /* Report logic */ }
    // 3 responsabilidades = 3 motivos para mudar
}
```

✅ **Bom:**
```php
class User { /* Apenas dados do usuário */ }
class UserRepository { /* Apenas persistência */ }
class EmailService { /* Apenas envio de email */ }
class ReportGenerator { /* Apenas relatórios */ }
```

---

## O - Open/Closed

**Aberto para extensão, fechado para modificação**

```php
// ❌ Ruim:
class CalculadoraFrete {
    public function calcular($tipo, $peso) {
        if ($tipo == 'normal') return $peso * 2;
        if ($tipo == 'expresso') return $peso * 5;
        // Para adicionar novo tipo = modificar classe
    }
}

// ✅ Bom:
interface FreteCalculator {
    public function calcular($tipo, $peso);
}
class FreteNormal implements FreteCalculator { /* */ }
class FreteExpresso implements FreteCalculator { /* */ }
// Novo tipo = nova classe, sem modificar existentes
```

---

## L - Liskov Substitution

**Objetos de subclasse devem substituir objetos da classe pai sem quebrar**

```php
// ❌ Ruim:
class Bird {
    public function fly() { /* voa */ }
}
class Penguin extends Bird {
    public function fly() {
        throw new Exception("Pinguim não voa!");
    }
}

// ✅ Bom:
interface Bird { }
interface FlyingBird extends Bird {
    public function fly();
}
class Eagle implements FlyingBird { /* voa */ }
class Penguin implements Bird { /* não voa */ }
```

---

## I - Interface Segregation

**Muitas interfaces específicas > Uma interface geral**

```php
// ❌ Ruim:
interface Worker {
    public function work();
    public function eat();
    public function sleep(); // Robô não dorme!
}

// ✅ Bom: Cada classe só implementa o que precisa
interface Workable {
    public function work();
}
interface Eater {
    public function eat();
}
interface Sleeper {
    public function sleep();
}
```

---

## D - Dependency Inversion

**Dependa de abstrações, não de concretizações**

```php
// ❌ Ruim:
class PedidoService {
    private $mysql; // Dependência concreta
    
    public function __construct() {
        $this->mysql = new MySQL(); // Acoplamento forte
    }
}

// ✅ Bom:
class PedidoService {
    // Injeção de dependência
    public function __construct(private readonly PedidoRepository $repository) {
    }
}
```

--- 

_SOLID é besteira o negocio é funcional, afinal em funcional tudo isso é só função._

### Não é bem assim amigo!
Se for pensar desse jeito em **POO tudo é objeto**

---

## SOLID vs Programação Funcional

**SOLID é orientado a objetos, mas conceitos se aplicam:**

<div class="horizontal-align">

<div>

**Single Responsibility** ↔️ **Pure Functions**
- Uma função, uma responsabilidade
- Sem side effects
- Entrada → Saída previsível

</div>

<div>


**Open/Closed** ↔️ **Higher-Order Functions**
- Extensão via composição
- Funções que recebem funções
- Pipeline de transformações

</div>

</div>

---

## SOLID vs Programação Funcional

**SOLID é orientado a objetos, mas conceitos se aplicam:**

<div class="horizontal-align">

<div>

**Liskov Substitution** ↔️ **Function Signatures**
- Tipos compatíveis
- Contratos respeitados via tipos
- TypeScript, Haskell garantem isso

</div>

<div>

**Interface Segregation** ↔️ **Function Composition**
- Funções pequenas e específicas
- Compose funções simples em complexas
- Evita "god functions"

</div>

<div>

**Dependency Inversion** ↔️ **Higher-Order Functions**
- Injetar comportamento via parâmetros
- Currying e partial application
- Inversão de controle funcional

</div>

</div>

---

## Padrões de Projeto

### Soluções Comprovadas

---

## O Que São Padrões?

**Soluções recorrentes para problemas comuns**

✅ Vocabulário comum
✅ Soluções testadas
✅ Menos bugs

❌ Não é: usar por usar
❌ Não é: over-engineering

---

## Quando Usar Padrões?

✅ **Use quando:**
- Problema se repete
- Solução conhecida se encaixa
- Time entende o padrão

❌ **Não use quando:**
- Código simples resolve
- Ninguém no time conhece
- Está apenas "seguindo livro"

---

## Cuidado: Pattern Fever

🚨 **Sintomas:**
- Factory de Factory ou Factory que só fabrica um tipo de item
- Padrão para problema inexistente
- Código mais complexo que problema

💡 **Lembre-se:**
_"Simplicidade é sofisticação máxima - Leonardo Davinci"_

---

## Gestão de Débitos Técnicos

### Controlando o Caos

---

## O Que é Débito Técnico?

💳 **Como empréstimo bancário**

**Principal:** Atalho tomado
**Juros:** Lentidão crescente
**Pagamento:** Refatoração

_Ignorar = juros compostos (MUITO caro)_

---

## Tipos de Débito

|                | Deliberado                      | Inadivertido                      |
|----------------|---------------------------------|-----------------------------------|
| **Imprudente** | Nós não temos tempo             | Nós não sabemos como              |
| **Prudente**   | Vamos lidar com isso mais tarde | Nós não deveriamos ter feito isso |

---

## Tipos de Débito

**Prudente & Deliberado**
_"Há conhecimento na decisão e estratégia de pagamento"_
✅ Aceitável

---

## Tipos de Débito

**Imprudente & Deliberado**
_"Há conhecimento na decisão, mas não tem estratégia de pagamento"_
❌ Evite

---

## Tipos de Débito

**Prudente & Inadvertido**
_"Não havia conhecimento no momento da decisão, mas a partir do conhecimento, nasce a estratégia"_
❌❌ Refatore!

---

## Tipos de Débito

**Imprudente & Inadvertido**
_"Não havia conhecimento no momento da decisão nem estratégia a partir do conhecimento"_
❌❌❌ Perigo!

---

## Como Identificar Débito?

🔍 **Sinais:**
- Código difícil de entender
- Bugs recorrentes
- Lentidão para adicionar features
- Medo de mexer no código

---

## Estratégia: Quadrante de Débito
|                   | Alta frequencia                 | Baixa frequncia  |
|-------------------|---------------------------------|------------------|
|**Alto Impacto**   | Refatore AGORA                  | Agende Sprint    |
|**Baixo Impacto**  | Próxima vez que mexer           | Ignore           |

---

## Quando Aceitar Débito?

✅ **Aceitável:**
- Validar hipótese de mercado
- Demo urgente para investidor
- Protótipo que pode ser descartado

**MAS:** Documente e planeje pagamento!

---

## Quando NÃO Aceitar?

❌ **Nunca:**
- Segurança
- Dados de clientes
- Transações financeiras
- Sistema crítico (saúde, etc)

_Alguns débitos são inadmissíveis_

---

## Cultura de Qualidade

_Qualidade não tem preço, mas a ausência dela custa caro_

- Code review rigoroso respeitando acordos do time
- Qualidade como parte do trabalho e não como extra
- Débito é visível no backlog
- Não busque por atalhos sempre
- Apresente os resultados

---

## Métricas de Qualidade

📊 **Acompanhe:**

- Cobertura de testes
- Complexidade ciclomática
- Duplicação de código
- Tempo de code review
- Frequência de bugs

**Ferramentas:** SonarQube

---

<!-- _class: lead -->

# Acoplamento Inteligente

**Nem todo acoplamento é ruim**
_O segredo está em saber quando e como_

---

## O Que é Acoplamento?

**Acoplamento** = dependência entre módulos

🎯 **Objetivo:**
- Baixo acoplamento (independência)
- Alta coesão (responsabilidade clara)

_Mas zero acoplamento é impossível!_

---

## Acoplamento Inteligente

**Indireção** 🔀
_Adicionar camada intermediária_

**Acoplamento Espacial** 📍
_Dependência de localização/ordem_

**Acoplamento Temporal** ⏰
_Dependência de tempo/sequência_

---

<!-- _class: lead -->

# Indireção

**Adicionar abstração entre componentes**

---

## Indireção: O Que É?

**Camada intermediária** entre dois componentes

✅ **Benefícios:**
- Reduz dependência direta
- Facilita mudanças
- Permite substituição

❌ **Cuidado:**
- Adiciona complexidade
- Mais difícil de debugar

---

## Exemplo: Indireção

❌ **Sem Indireção:**
```php
class PedidoController {
    public function finalizar($pedidoId) {
        // Acoplamento direto com implementação
        $smtp = new SMTPMailer('smtp.gmail.com');
        $smtp->setAuth('user@gmail.com', 'senha');
        $smtp->send(
            'cliente@email.com',
            'Pedido confirmado',
            'Seu pedido #' . $pedidoId
        );
        
        // Se trocar de serviço de email, precisa mudar aqui!
    }
}
```

---

## Exemplo: Indireção

✅ **Com Indireção (Interface):**
```php
interface EmailService {
    public function enviar($destinatario, $assunto, $mensagem);
}

class PedidoController {
    private $emailService;
    
    public function __construct(EmailService $emailService) {
        $this->emailService = $emailService;
    }
    
    public function finalizar($pedidoId) {
        $this->emailService->enviar(
            'cliente@email.com',
            'Pedido confirmado',
            'Seu pedido #' . $pedidoId
        );
    }
}
```

---

## Exemplo: Indireção

```php
// Implementações diferentes, mesma interface
class SmtpEmailService implements EmailService {
    public function enviar($dest, $assunto, $msg) {
        // Implementação SMTP
    }
}

class SendGridEmailService implements EmailService {
    public function enviar($dest, $assunto, $msg) {
        // Implementação SendGrid API
    }

class AwsSesEmailService implements EmailService {
    public function enviar($dest, $assunto, $msg) {
        // Implementação AWS SES
    }
}
```

Controller não precisa mudar!

---

## Quando NÃO Usar Indireção?

❌ **Evite quando:**
- Implementação única e não vai mudar
- Componentes muito simples
- Adiciona complexidade desnecessária

```php
// Indireção desnecessária!
interface StringHelper {
    public function uppercase($str);
}

// PHP já tem strtoupper()!
```

**Regra:** YAGNI - You Aren't Gonna Need It

---

---

<!-- _class: lead -->

# Acoplamento Espacial

**Ordem e localização importam**

---

## Acoplamento Espacial: O Que É?

**Dependência de ordem ou localização** de execução

❌ **Problema:**
```php
class Usuario {
    public function salvar() {
        $this->validar();
        $this->hashearSenha();
        $this->inserirNoBanco();
    }
}

// Se trocar a ordem, quebra!
// hashearSenha() DEVE vir antes de inserirNoBanco()
```

---

## Exemplo: Acoplamento Espacial

❌ **Ruim (ordem importa):**
```php
class RelatorioService {
    private $dados;
    
    public function carregarDados() {
        $this->dados = DB::query('SELECT * FROM vendas');
    }
    
    public function processar() {
        // PRECISA chamar carregarDados() primeiro!
        return array_map(fn($d) => $d * 1.1, $this->dados);
    }
    
    public function gerar() {
        // PRECISA chamar processar() antes!
        return PDF::create($this->dados);
    }
}
```

---

## Exemplo: Acoplamento Espacial

❌ **Uso perigoso:**
```php
$relatorio = new RelatorioService();

// Se esquecer uma etapa, erro!
$relatorio->carregarDados();
// Esqueceu de processar()
$relatorio->gerar(); // ERRO: dados não processados
```

---

## Exemplo: Acoplamento Espacial

✅ **Melhor (ordem garantida):**
```php
class RelatorioService {
    public function gerar() {
        // Encapsula a sequência correta
        $dados = $this->carregarDados();
        $processados = $this->processar($dados);
        return $this->criarPdf($processados);
    }
    
    private function carregarDados() {
        return DB::query('SELECT * FROM vendas');
    }
    
    private function processar($dados) {
        return array_map(fn($d) => $d * 1.1, $dados);
    }
    
    private function criarPdf($dados) {
        return PDF::create($dados);
    }
}
```

---

## Exemplo: Acoplamento Espacial

✅ **Uso simples:**
```php
$relatorio = new RelatorioService();
$pdf = $relatorio->gerar(); // Impossível errar a ordem!
```

**Princípio:** Torne impossível usar incorretamente

---

## Quando Evitar Acoplamento Espacial?

✅ **Estratégias:**

**1. Method Chaining (Fluent Interface):**
```php
$usuario = (new Usuario())
    ->setNome('Diego')
    ->setEmail('diego@example.com')
    ->validar()
    ->salvar();
```

**2. Builder Pattern:**
```php
$pedido = PedidoBuilder::novo()
    ->comProduto($produto)
    ->comCliente($cliente)
    ->comPagamento($pagamento)
    ->build(); 
    // Valida que tudo está completo
```

---

## Acoplamento Entre Serviços

**Frontend e Backend acoplados**

❌ **Problema:**
- Frontend depende da estrutura exata do backend
- Mudança no backend quebra o frontend
- API genérica forçando frontend a fazer transformações
- Multiple round trips

---

## Exemplo: Frontend Acoplado

❌ **Backend com estrutura genérica:**
```php
// API Backend
class ProdutoController {
    public function show($id) {
        return Produto::with([
            'categoria',
            'fabricante',
            'avaliacoes',
            'estoque'
        ])->findOrFail($id);
    }
}

// Retorna TUDO, mesmo que frontend não precise
```

---

## Exemplo: Frontend Acoplado

❌ **Frontend fazendo transformações:**
```javascript
// Frontend precisa fazer múltiplas chamadas e transformar
async function carregarProduto(id) {
    const produto = await api.get(`/produtos/${id}`);
    const promocao = await api.get(`/promocoes/${id}`);
    const similares = await api.get(`/produtos/${id}/similares`);
    
    // Frontend conhece a estrutura interna!
    return {
        nome: produto.data.nome,
        preco: produto.data.valor_venda,
        precoOriginal: promocao.data?.preco_de || produto.data.valor_venda,
        desconto: promocao.data?.percentual || 0,
        imagem: produto.data.imagens[0].url_grande,
        estoque: produto.data.estoque.quantidade > 0,
        similares: similares.data.map(s => ({
            id: s.id,
            nome: s.nome,
            thumb: s.imagens[0]?.url_pequena
        }))
    };
}
```

3+ requisições! Frontend acoplado à estrutura do backend!

---

## Solução: BFF (Backend For Frontend)

**Backend específico para cada frontend**

✅ **Benefícios:**
- API customizada para necessidade do frontend
- Uma requisição ao invés de múltiplas
- Frontend não conhece estrutura interna
- Evolução independente

---

## Exemplo: BFF

✅ **BFF Layer:**
```php
// BFF Controller - customizado para o frontend web
class ProdutoBffController {
    private $produtoService;
    private $promocaoService;
    private $recomendacaoService;
    
    public function show($id) {
        // Uma chamada retorna tudo que o frontend precisa
        $produto = $this->produtoService->buscar($id);
        $promocao = $this->promocaoService->buscarAtiva($id);
        $similares = $this->recomendacaoService->similares($id, 4);
        
        return [
            'nome' => $produto->nome,
            'preco' => $promocao?->precoFinal ?? $produto->preco,
            'precoOriginal' => $produto->preco,
            'desconto' => $promocao?->percentual ?? 0,
            'imagem' => $produto->imagemPrincipal(),
            'emEstoque' => $produto->temEstoque(),
            'similares' => $similares->map(fn($s) => [
                'id' => $s->id,
                'nome' => $s->nome,
                'thumb' => $s->thumbnail()
            ])
        ];
    }
}
```

---

## Exemplo: BFF

✅ **Frontend simplificado:**
```javascript
// Frontend agora é simples!
async function carregarProduto(id) {
    // Uma única requisição
    const response = await api.get(`/bff/produtos/${id}`);
    
    // Dados já no formato esperado
    return response.data;
    // { nome, preco, precoOriginal, desconto, imagem, 
    //   emEstoque, similares }
}
```

Uma requisição! Formato customizado! Desacoplado!

---

## Sinais de Acoplamento Espacial

🚨 **Cuidado quando:**
- Métodos precisam ser chamados em ordem específica
- Estado interno compartilhado entre métodos
- Documentação diz "chame X antes de Y"
- Testes quebram se mudar ordem
- Alterações no backend obrigam alterações no frontend

---

<!-- _class: lead -->

# Acoplamento Temporal

**Quando as coisas devem acontecer**

---

## Acoplamento Temporal: O Que É?

**Dependência de momento de execução**

❌ **Problema:**
- Operação só funciona em horário específico
- Sincronização forçada

---

## Exemplo: Race Condition

❌ **Acoplamento temporal perigoso:**
```php
// USO:
$saldo = $conta->getSaldo(); // Thread 1: R$ 100
if ($saldo >= 50) {
    // Thread 2 saca aqui!
    $conta->sacar(50); // Thread 1: Pode ficar negativo!
}
```

---

✅ **Solução (operação atômica):**
```php
class PaymentUseCase {
    public function pay($amount) {
        DB::transaction(function() use ($amount) {
            // Lock pessimista
            $conta = DB::table('accounts')
                ->where('id', $this->id)
                ->lockForUpdate()
                ->first();
            if ($conta->balance >= $amount) {
                DB::table('accounts')
                    ->where('id', $this->id)
                    ->decrement('balance', $amount);
                return true;
            }
            throw new Exception();
        });
    }
}
```

---

## Exemplo: Acoplamento Temporal

❌ **Ruim (sincronização forçada):**
```php
class PedidoService {
    public function criar($dados) {
        $pedido = Pedido::create($dados);
        
        // Espera resposta síncrona do gateway
        $pagamento = $this->gateway->processar($pedido);
        
        if ($pagamento->aprovado) {
            $pedido->confirmar();
        }
        
        return $pedido;
        // Cliente esperando 5+ segundos...
    }
}
```

---

## Exemplo: Acoplamento Temporal

✅ **Melhor (assíncrono):**
```php
class PedidoService {
    public function criar($dados) {
        $pedido = Pedido::create($dados);
        
        // Dispara job assíncrono
        ProcessarPagamentoJob::dispatch($pedido);
        
        return $pedido; // Resposta rápida!
    }
}

class ProcessarPagamentoJob {
    public function handle() {
        $pagamento = $this->gateway->processar($this->pedido);
        
        if ($pagamento->aprovado) {
            $this->pedido->confirmar();
            event(new PedidoConfirmado($this->pedido));
        }
    }
}
```

---

## Quando Evitar Acoplamento Temporal?

✅ **Estratégias:**

**1. Processamento assíncrono:**
- Jobs/Queues, Event-driven architecture e Message brokers (RabbitMQ, Kafka)

**2. Idempotência:**

**3. Eventual consistency:**
- Não precisa ser imediato e o sistema converge para estado consistente

--- 

## Sinais de Acoplamento Temporal

🚨 **Cuidado quando:**
- "Execute isso apenas até o horário X"
- Timeouts frequentes
- Falhas intermitentes (race conditions)
- Operações dependem de cron/scheduler
- Código "às vezes funciona, às vezes não"

---

O incidente global da AWS foi 
causado por 2 tipos acoplamentos
### Quais foram?


---

<!-- _class: lead -->

# Mensageria e Comunicação Assíncrona

**Desacoplando sistemas com filas, brokers e pub/sub**

---

## Por Que Mensageria?

**Problema:** Sistemas acoplados temporalmente

❌ **Sem mensageria:**
- Serviços dependem uns dos outros
- Falha em cascata
- Performance degradada
- Difícil de escalar

---

## Por Que Mensageria?

✅ **Com mensageria:**
- Serviços independentes
- Alta disponibilidade
- Processamento paralelo
- Escalabilidade horizontal

---

## Conceitos Fundamentais

**Message Queue (Fila)** 🎯
- Point-to-point (1 produtor → 1 consumidor)
- Mensagem processada exatamente uma vez
- Ordem garantida (FIFO)

---

## Conceitos Fundamentais

**Pub/Sub (Publicação/Assinatura)** 📢
- Broadcast (1 produtor → N consumidores)
- Mensagem pode ser consumida múltiplas vezes
- Consumidores independentes

---

## Conceitos Fundamentais

**Message Broker** 🏢
- Intermediário que gerencia mensagens
- Garante entrega, persistência, retry

---

## Arquitetura: Message Queue

```
┌──────────┐      ┌───────────┐      ┌──────────┐
│ Produtor │─────>│   FILA    │─────>│Consumidor│
└──────────┘      └───────────┘      └──────────┘
                       │
                       │ Persistência
                       │ Ordem FIFO
                       │ Retry
                       ▼
                   [Storage]
```

**Características:**
- Mensagem removida após consumo
- Um único consumidor por mensagem
- Ideal para tarefas distribuídas

---

## Arquitetura: Pub/Sub

```
                    ┌──────────────┐
              ┌────>│ Consumidor A │
              │     └──────────────┘
┌──────────┐  │     ┌──────────────┐
│Publisher │──┼────>│ Consumidor B │
└──────────┘  │     └──────────────┘
              │     ┌──────────────┐
              └────>│ Consumidor C │
                    └──────────────┘
```

**Características:**
- Mensagem replicada para todos
- Consumidores se inscrevem em tópicos
- Ideal para notificações e eventos

---

## Quando Usar Message Queue?

✅ **Use Filas quando:**

- **Processamento em background**
  - Envio de emails
  - Geração de relatórios
  - Processamento de imagens

---

## Quando Usar Message Queue?

✅ **Use Filas quando:**

- **Balanceamento de carga**
  - Múltiplos workers consumindo
  - Distribuição automática

---

## Quando Usar Message Queue?

✅ **Use Filas quando:**

- **Garantia de ordem**
  - Processamento sequencial importante
  - FIFO necessário

---

## Quando Usar Pub/Sub?

✅ **Use Pub/Sub quando:**

- **Múltiplos interessados**
  - 1 evento → várias ações
  - Sistemas diferentes reagindo

---

## Quando Usar Pub/Sub?

✅ **Use Pub/Sub quando:**

- **Event-Driven Architecture**
  - Eventos de domínio
  - Notificações do sistema

---

## Quando NÃO Usar Mensageria?

❌ **Evite quando:**

- **Resposta imediata necessária**
  - Validação de formulário
  - Login/Autenticação
  - Operações síncronas críticas

---

## Quando NÃO Usar Mensageria?

❌ **Evite quando:**

- **Operação muito simples**
  - Adicionar complexidade desnecessária
  - Overhead não justifica

---

## Quando NÃO Usar Mensageria?

❌ **Evite quando:**

- **Baixo volume**
  - Poucas mensagens/dia
  - Infraestrutura cara para uso mínimo

---

## Quando NÃO Usar Mensageria?

❌ **Evite quando:**

- **Debugging crítico**
  - Rastreabilidade difícil
  - Ambiente de desenvolvimento

---

## Ferramentas Disponíveis

**RabbitMQ** 🐰
**Apache Kafka** 🔥
**Redis** ⚡
**Amazon SQS/SNS** ☁️
**Google Pub/Sub** ☁️

Cada uma com seus tradeoffs...

---

## RabbitMQ

**Características:**
- Protocol: AMQP
- Exchanges (direct, topic, fanout, headers)
- Queues com prioridade
- Ack/Nack manual
- Dead Letter Queue nativo

---

## RabbitMQ

**Prós** ✅
- Fácil de configurar
- Interface administrativa excelente
- Suporte a múltiplos protocolos
- Comunidade grande

---

## RabbitMQ

**Contras** ❌
- Performance menor que Kafka
- Não é para streaming
- Consumo alto de memória

---

## Apache Kafka

**Características:**
- Log distribuído e particionado
- Retenção configurável (horas/dias/sempre)
- Consumer groups
- Exatamente uma vez (exactly-once semantics)

---

## Apache Kafka

**Prós** ✅
- Altíssimo throughput (milhões/seg)
- Reprocessamento de mensagens
- Event sourcing nativo
- Durabilidade extrema

---

## Apache Kafka

**Contras** ❌
- Complexo de configurar
- Requer Zookeeper (ou KRaft)
- Curva de aprendizado alta
- Overhead para casos simples

---

## Redis (Pub/Sub e Streams)

**Características:**
- In-memory (super rápido)
- Pub/Sub simples
- Streams (desde v5.0)
- Não garante persistência por padrão

---

## Redis (Pub/Sub e Streams)

**Prós** ✅
- Extremamente rápido
- Fácil de usar
- Já está na stack (cache)
- Bom para casos simples

---

## Redis (Pub/Sub e Streams)

**Contras** ❌
- Não durável por padrão
- Sem garantia de entrega
- Limitado pela memória
- Não é message broker completo

---

## Amazon SQS/SNS

**SQS (Simple Queue Service)** 📦
- Fila gerenciada
- Paga por uso
- Escalabilidade automática
- FIFO ou Standard

**SNS (Simple Notification Service)** 📢
- Pub/Sub gerenciado
- Integração com Lambda, SQS, HTTP
- Email, SMS, Push notifications

---

## Amazon SQS/SNS

**Prós** ✅
- Zero manutenção
- Escalabilidade infinita
- Integração AWS
- Pay-as-you-go

---

## Amazon SQS/SNS

**Contras** ❌
- Vendor lock-in
- Latência variável
- Custo em alto volume

---

## Comparação de Ferramentas

| Ferramenta | Throughput | Latência | Persistência | Complexidade | Custo |
|------------|------------|----------|--------------|--------------|-------|
| **RabbitMQ** | Média | Baixa | Alta | Média | Baixo |
| **Kafka** | Altíssima | Média | Muito Alta | Alta | Médio |
| **Redis** | Altíssima | Muito Baixa | Baixa | Baixa | Baixo |
| **SQS/SNS** | Alta | Média | Alta | Muito Baixa | Variável |

---

## Dead Letter Queue (DLQ)

**O que é?**
- Fila especial para mensagens que falham
- Evita perder mensagens problemáticas
- Permite análise e reprocessamento

---

## Dead Letter Queue (DLQ)

**Quando uma mensagem vai pra DLQ?**
- Excede número máximo de tentativas
- Erro irrecuperável
- Timeout de processamento
- Mensagem malformada

---

## DLQ: Estratégias

**1. Retry com Backoff Exponencial**
```
Tentativa 1: falha → espera 1 min
Tentativa 2: falha → espera 2 min
Tentativa 3: falha → espera 4 min
Tentativa 4: falha → DLQ
```

---

## DLQ: Estratégias

**2. Circuit Breaker na DLQ**
- Se muitas mensagens na DLQ
- Para de processar temporariamente
- Investiga causa raiz

---

## DLQ: Estratégias

**3. Análise Automatizada**
- Dashboard de erros
- Alertas por tipo
- Reprocessamento em lote

---

## Boas Práticas: Mensageria

✅ **Idempotência**
- Processar mensagem múltiplas vezes = mesmo resultado
- Use IDs únicos de mensagem

---

## Boas Práticas: Mensageria

✅ **Timeout configurável**
- Visibility timeout em filas
- Evita processar eternamente

---

## Boas Práticas: Mensageria

✅ **Monitoramento**
- Tamanho da fila
- Taxa de erro
- Latência de processamento
- Correlation ID

---

## Boas Práticas: Mensageria

✅ **Dead Letter Queue**
- Sempre configure DLQ
- Monitore e alerte

---

## Boas Práticas: Mensageria

✅ **Serialização**
- JSON para simplicidade
- Avro/Protobuf para performance
- Versionamento de schemas

---

## Boas Práticas: Mensageria

✅ **Batching**
- Processar múltiplas mensagens juntas
- Reduz overhead

---

## Boas Práticas: Mensageria

✅ **Retry inteligente**
- Backoff exponencial
- Limite de tentativas

---

## Antipadrões a Evitar

❌ **Usar como storage**
- Mensageria não é banco de dados
- Dados importantes devem persistir

---

## Antipadrões a Evitar

❌ **Mensagens gigantes**
- Envie referência, não o objeto completo
- Limite: 256KB (SQS), 1MB (Kafka)

---

## Antipadrões a Evitar

❌ **Ignorar DLQ**
- DLQ crescendo = problema no sistema
- Monitore e corrija causas

---

## Antipadrões a Evitar

❌ **Sincronia disfarçada**
- Esperar resposta da fila = anti-padrão
- Use request/response se precisa síncrono

---

<!-- _class: lead -->

# Testes de Software

**Garantindo qualidade e confiança no código**

---

## Por Que Testar?

❌ **Sem testes:**
- Medo de fazer mudanças e colocar bugs em produção
- Regressões constantes
- Código acoplado (difícil de testar)
- Deploys arriscados

---

## Por Que Testar?

✅ **Com testes:**
- Confiança para refatorar
- Bugs detectados cedo
- Documentação viva do código
- Design melhor (testabilidade força desacoplamento)
- Deploy contínuo

---

## Cultura de Testes

**Testes não são "extra", são parte do trabalho**

❌ **Evite:**

- "Depois eu testo"
- "Não tenho tempo pra testes"
- "Esse código é simples, não precisa"
- Testar só quando quebra

---

## Cultura de Testes

**Testes não são "extra", são parte do trabalho**

🎯 **Mentalidade:**
- Escrever teste não é perder tempo
- Teste é investimento, não custo
- Qualidade desde o início
- "Red, Green, Refactor" (TDD)

---

## Cultura de Testes

**Responsabilidade compartilhada**

👥 **Time todo testa:**
- Dev escreve testes unitários e integração
- QA foca em testes exploratórios e E2E
- Code review valida cobertura
- CI/CD roda testes automaticamente

---

## Cultura de Testes

📊 **Métricas:**
- Cobertura de código (>80% ideal)
- Tempo de execução dos testes
- Taxa de falsos positivos
- Bugs encontrados em produção

---

## Pirâmide de Testes

```
           /\
          /  \
         /    \
        /      \
       /  E2E   \        Poucos, lentos, caros
      /----------\
     /            \
    / Integração   \    Moderados
   /----------------\
  /                  \
 /   Testes Unitários \  Muitos, rápidos, baratos
/----------------------\
```

---

## Pirâmide de Testes: Detalhes

**Testes Unitários** 🔬
- Testam uma unidade isolada (função/classe)
- Rápidos (milissegundos)
- Sem dependências externas
- Fácil de debugar

---

## Pirâmide de Testes: Detalhes

**Testes de Integração** 🔗
- Testam interação entre componentes
- Moderadamente lentos (segundos)
- Podem usar banco de dados de teste
- Validam contratos

---

## Pirâmide de Testes: Detalhes

**Testes E2E (End-to-End)** 🌐
- Testam fluxo completo do usuário
- Lentos (minutos)
- Ambiente real ou staging
- Validam experiência completa

---

## Testes de Carga (Load Testing)

**O que testa?**
- Comportamento sob carga normal/alta
- Quantos usuários simultâneos suporta?
- Tempo de resposta sob pressão
- Identificar gargalos

**Ferramentas:**
- Apache Bench (ab)
- Artillery
- JMeter
- k6
- Gatling

---

## Testes de Stress

**O que testa?**
- Comportamento além do limite
- Onde o sistema quebra?
- Como ele se recupera?
- Qual o ponto de ruptura?

**Diferença de Load:**
- Load: comportamento normal/esperado
- Stress: comportamento extremo/além do limite

---

## Testes de Stress

**O que observar:**
- Em qual ponto começou a falhar?
- Erro 500? Timeout? OOM?
- Sistema se recuperou após stress?

---

## Métricas: Load vs Stress

**Teste de Carga** 📊
```
Usuários: 0 → 100 → 100 → 0
Response: ████████ 200ms (estável)
CPU:      ████████ 60% (estável)
Memória:  ████████ 2GB (estável)
```

**Teste de Stress** 🔥
```
Usuários: 0 → 500 → 1000 → 0
Response: ████████████ 200ms → 5s → TIMEOUT
CPU:      ████████████ 60% → 99% → 100%
Memória:  ████████████ 2GB → 6GB → OOM Kill
```

Descobre limites e comportamento em falha!

---

## Testes de Mutação

**O que testa?**
- Qualidade dos seus testes
- Testes realmente validam o código?
- "Quem testa os testes?"

---

## Testes de Mutação

**Como funciona:**
1. Mutante altera código (troca `>` por `>=`)
2. Roda testes
3. Se testes passam = MUTANTE SOBREVIVEU (ruim!)
4. Se testes falham = MUTANTE MORTO (bom!)

**Mutation Score:** % de mutantes mortos

---

## Testes de Contratos (Contract Testing)

**O que testa?**
- APIs mantêm contratos com consumidores
- Breaking changes em APIs
- Compatibilidade entre serviços

**Ferramentas:**
- Pact
- Spring Cloud Contract

---

## Antipadrões em Testes

❌ **Testes que dependem de ordem**
❌ **Testes lentos desnecessários**
❌ **Múltiplos conceitos no mesmo teste**
❌ **Magic numbers sem contexto**
❌ **Ignorar testes falhando**

---

## TDD (Test-Driven Development)

**Ciclo Red-Green-Refactor:**

🔴 **Red:** Escreve teste que falha
🟢 **Green:** Implementa código mínimo
♻️ **Refactor:** Melhora implementação

---

<!-- _class: lead -->

# Construindo um Software Moderno

**Do problema à solução: decisões de arquitetura**

---

## O Que Vamos Construir?

**Jornada completa:**
1. Entender o problema
2. Definir escopo essencial
3. Avaliar tradeoffs
4. Escolher tecnologias
5. Desenhar arquitetura
6. Decidir padrões

**Ao final:** 4 atividades práticas em grupo!

---

<!-- _class: lead -->

# Escolha de Linguagem

**A ferramenta certa para o problema certo**

---

## Escolha de Linguagem

**Não existe "melhor linguagem"**
_Existe a melhor para ESTE problema_

🎯 **Critérios de avaliação:**
- Tipo de aplicação
- Performance necessária
- Ecossistema e bibliotecas
- Time e conhecimento
- Mercado e contratação
- Comunidade e suporte

---

## Critérios de Decisão: Linguagem

**1. Performance necessária?**
**2. Time tem experiência?**
```
Sim → Use o que sabem bem
Não → Tem tempo e estratégia para aprender?
```
**3. Ecossistema maduro?**
**4. Contratação fácil?**

---

<!-- _class: lead -->

# Escolha de Banco de Dados

**SQL ou NoSQL? Depende do problema!**

---

## Tipos de Bancos de Dados

**SQL (Relacional)** 🗄️
- PostgreSQL, MySQL, SQL Server
- ACID garantido
- Schema rígido
- JOIN complexos

---

## Tipos de Bancos de Dados

**NoSQL Documento** 📄
- MongoDB, CouchDB
- Schema flexível
- Denormalização
- Escalabilidade horizontal

---

## Tipos de Bancos de Dados

**NoSQL Chave-Valor** 🔑
- Redis, DynamoDB
- Ultra rápido
- Cache, sessões
- Dados simples

---

## Quando Usar SQL?

✅ **Use SQL quando:**

- **Transações ACID críticas**
  - Consistência forte obrigatória (Financeiro, e-commerce)

- **Relacionamentos complexos**
  - JOINs frequentes e integridade referencial

- **Schema bem definido**
  - Estrutura de dados estável com validações rígidas

---

## Quando Usar NoSQL?

✅ **Use NoSQL quando:**

- **Escalabilidade horizontal**
  - Milhões de usuários
  - Petabytes de dados

- **Schema flexível**
  - Dados variados/dinâmicos
  - Evolução rápida

---

## Quando Usar NoSQL?

✅ **Use NoSQL quando:**

- **Alta performance leitura**
  - Cache distribuído
  - Sessões, logs

- **Big Data**
  - Analytics em tempo real
  - IoT, telemetria

---

## Critérios de Decisão: Banco

**1. Consistência vs Disponibilidade** (CAP)
```
Consistência forte → SQL
Disponibilidade → NoSQL
```

---

## Critérios de Decisão: Banco

**2. Volume de dados**
```
< 1TB → SQL está ótimo
> 10TB → Considere NoSQL
> 100TB → NoSQL/Data Lake
```

---

## Critérios de Decisão: Banco

**3. Tipo de queries**
```
Complexas (JOIN) → SQL
Simples (key-value) → NoSQL
```

---

## Critérios de Decisão: Banco

**4. Transações?**
```
Críticas → SQL
Eventual consistency OK → NoSQL
```

---

<!-- _class: lead -->

# Design de Código

**Padrões e arquiteturas disponíveis**

---

## Opções de Design de Código

**MVC (Model-View-Controller)** 📐
- Tradicional para web
- Separação de responsabilidades
- Laravel, Rails, Django

---

## Opções de Design de Código

**DDD (Domain-Driven Design)** 🏗️
- Foco no domínio de negócio
- Bounded contexts
- Aggregates, Entities, Value Objects

---

## Opções de Design de Código

**Clean Architecture** 🎯
- Independência de frameworks
- Testabilidade máxima
- Camadas bem definidas

---

## Opções de Design de Código

**Hexagonal (Ports & Adapters)** ⬡
- Core isolado
- Adapters para infra
- Similar a Clean

---


<!-- _class: lead -->

# REST APIs

**Boas práticas essenciais**

---

## REST APIs: Essenciais

**1. Use substantivos, não verbos**
```
✅ GET /users/123
✅ POST /users
✅ PUT /users/123
✅ DELETE /users/123

❌ GET /getUser?id=123
❌ POST /createUser
❌ POST /deleteUser/123
```

---

## REST APIs: Essenciais

**2. Use HTTP methods corretos**
```
GET    → Buscar (idempotente)
POST   → Criar
PUT    → Atualizar completo
PATCH  → Atualizar parcial
DELETE → Remover
```

---

## REST APIs: Essenciais

**3. Status codes apropriados**
```
1XX     → Mensagem recebida
2XX     → Sucesso
3XX     → Redirect
4XX     → Problema na solicitação
5XX     → Problema no servidor
```

---

## REST APIs: Essenciais

**4. Versionamento**
```
✅ /api/v1/users
✅ /api/v2/users
✅ Header: Accept: application/vnd.api.v2+json
```

---

## REST APIs: Essenciais

**5. Paginação**
```json
GET /users?page=2&limit=20

{
  "data": [...],
  "meta": {
    "current_page": 2,
    "total_pages": 10,
    "total_items": 200,
    "per_page": 20
  }
}
```

**6. Filtros e ordenação**
```
GET /products?category=electronics&sort=-price&min_price=100
```

---

<!-- _class: lead -->

# Microsserviços vs Monólitos

**Não é questão de melhor, é questão de contexto**

---

## Monólito

**O que é?**
- Aplicação única
- Deploy único
- Banco de dados compartilhado
- Tudo em um processo

---

## Monólito

```
┌─────────────────────────┐
│                         │
│   ┌──────┐  ┌──────┐    │
│   │Users │  │Orders│    │
│   └──────┘  └──────┘    │
│   ┌──────┐  ┌──────┐    │
│   │Paym. │  │Stock │    │
│   └──────┘  └──────┘    │
│                         │
│      Single DB          │
└─────────────────────────┘
```

---

## Monólito: Vantagens

✅ **Simplicidade:**
- Fácil de desenvolver
- Fácil de testar
- Fácil de deployar
- Sem complexidade de rede

---

## Monólito: Vantagens

✅ **Performance:**
- Sem chamadas de rede
- Transações ACID simples
- Joins no banco

---

## Monólito: Vantagens

✅ **Consistência:**
- Dados sempre consistentes
- Sem problemas de distributed transactions

---

## Monólito: Vantagens

✅ **Debugging:**
- Stack trace completo
- Fácil de rastrear bugs

---

## Monólito: Desvantagens

❌ **Escalabilidade:**
- Escala tudo junto (CPU + Memória)
- Não escala partes específicas

---

## Monólito: Desvantagens

❌ **Deploy:**
- Deploy de tudo junto
- Risco alto (tudo ou nada)
- Downtime necessário

---

## Monólito: Desvantagens

❌ **Time:**
- Código acoplado
- Conflitos de merge
- Difícil paralelizar trabalho

---

## Monólito: Desvantagens

❌ **Tecnologia:**
- Stack única
- Difícil experimentar

---

## Microsserviços

**O que é?**
- Múltiplos serviços independentes
- Deploy independente
- Banco de dados por serviço
- Comunicação via rede (HTTP/gRPC/MQ)

```
┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐
│Users │  │Orders│  │Paym. │  │Stock │
└───┬──┘  └───┬──┘  └───┬──┘  └───┬──┘
    │DB       │DB       │DB       │DB
```

---

## Microsserviços: Vantagens

✅ **Escalabilidade independente:**
- Escala só o que precisa
- Otimização de recursos

---

## Microsserviços: Vantagens

✅ **Deploy independente:**
- Zero downtime
- Rollback parcial
- Deploy frequente

---

## Microsserviços: Vantagens

✅ **Times autônomos:**
- Cada time seu serviço
- Menos conflitos
- Velocidade

---

## Microsserviços: Vantagens

✅ **Tecnologia:**
- Stack por serviço
- Linguagem adequada ao problema

---

## Microsserviços: Desvantagens

❌ **Complexidade:**
- Distributed systems
- Network latency
- Service discovery
- API Gateway

---

## Microsserviços: Desvantagens

❌ **Consistência:**
- Eventual consistency
- Distributed transactions (SAGA)
- Debugging complexo

---

## Microsserviços: Desvantagens

❌ **Operacional:**
- Múltiplos deploys
- Monitoramento complexo
- Logs distribuídos

---

## Microsserviços: Desvantagens

❌ **Overhead:**
- Infraestrutura complexa
- Kubernetes, service mesh
- Custo inicial alto

---

## Quando Usar Cada Um?

**Use Monólito quando:** 🏢
- Startup/MVP
- Time pequeno (< 10)
- Domínio simples
- Baixo tráfego
- Consistência forte necessária

---

## Quando Usar Cada Um?

**Use Microsserviços quando:** 🚀
- Múltiplos times
- Domínio complexo
- Escalabilidade independente necessária
- Deploy frequente
- Alto tráfego
- Times autônomos

**Regra de ouro:** Comece com monólito, evolua para micro quando necessário!

---

<!-- _class: lead -->

# Programação Concorrente

**Múltiplas coisas acontecendo ao mesmo tempo**

---

## O Que é Concorrência?

**Concorrência** ≠ **Paralelismo**

---

## O Que é Concorrência?

**Concorrência:** 🔄
- Lidar com múltiplas tarefas
- Pode ser em 1 CPU (time-sharing)
- Exemplo: Node.js (event loop)

---

## O Que é Concorrência?

**Paralelismo:** ⚡
- Executar múltiplas tarefas simultaneamente
- Precisa múltiplos cores
- Exemplo: Go routines, threads

---

## Quando Usar Concorrência?

✅ **Use quando:**

- **I/O bound:**
  - Múltiplas requisições HTTP
  - Leitura de arquivos
  - Database queries

---

<!-- _class: lead -->

# Race Conditions

**Quando múltiplas threads competem**

---

## O Que é Race Condition?

**Problema:**
```php
// Thread 1 e Thread 2 executam ao mesmo tempo
$saldo = $conta->getSaldo(); // R$ 100

if ($saldo >= 50) {
    // Thread 1: $saldo = 100, saca 50
    // Thread 2: $saldo = 100, saca 50 (ainda!)
    $conta->sacar(50);
}

// Saldo final = R$ 0 (deveria ser 50!)
```

**Resultado:** Dados inconsistentes! 💥

---

## Como Tratar Race Conditions?

**1. Locks (Pessimista)** 🔒
```php
DB::transaction(function() {
    $conta = Conta::lockForUpdate()->find($id);
    
    if ($conta->saldo >= 50) {
        $conta->saldo -= 50;
        $conta->save();
    }
});
```

Trava o registro até finalizar

---

## Como Tratar Race Conditions?

**2. Optimistic Locking** ✅
```php
$conta = Conta::find($id);
$versao = $conta->version;

$conta->saldo -= 50;
$conta->version++;

// Só atualiza se versão não mudou
$updated = DB::update(
    'UPDATE contas SET saldo = ?, version = ? 
     WHERE id = ? AND version = ?',
    [$conta->saldo, $conta->version, $id, $versao]
);

if (!$updated) {
    throw new ConcurrentModificationException();
}
```

---

## Como Tratar Race Conditions?

**3. Atomic Operations** ⚛️
```php
// Redis
$redis->decr('conta:123:saldo', 50);

// SQL
DB::statement('UPDATE contas SET saldo = saldo - 50 WHERE id = ?', [$id]);
```

Operação atômica (indivisível)

---

## Como Tratar Race Conditions?

**4. Queue/Serialização** 📬
```php
// Processa um de cada vez
Queue::push(new SacarJob($contaId, 50));
```

Remove concorrência

---

## Dicas: Race Conditions

✅ **Sempre considere:**
- Múltiplos usuários simultâneos
- Múltiplos servers/workers
- Operações que leem + escrevem

---

## Dicas: Race Conditions

✅ **Estratégias:**
- Lock apenas o necessário
- Minimize tempo dentro do lock
- Use atomic operations quando possível
- Idempotência para APIs

---

## Dicas: Race Conditions

❌ **Evite:**
- Locks globais (trava tudo)
- Locks longos (timeout)
- Nested locks (deadlock)

---

<!-- _class: lead -->

# Transações Distribuídas

**Como garantir consistência entre múltiplos bancos?**

---

## O Problema

**Cenário:**
```
Transferência bancária entre bancos diferentes

Banco A: debitar R$ 100
Banco B: creditar R$ 100
```

**Problema:**
- E se Banco A debitar mas Banco B falhar?
- Como garantir atomicidade (tudo ou nada)?
- Como garantir que ambos commitam ou ambos rollback?

**Não podemos usar transação simples!**
_Cada banco tem seu próprio BD_

---

## 2 Phase Commit (2PC)

**Solução clássica para transações distribuídas**

**Fases:**
1. **Prepare** (Voting)
2. **Commit** (Decision)

**Componentes:**
- **Coordinator** (coordenador)
- **Participants** (participantes)

---

## 2PC: Fase 1 - Prepare

```
Coordinator: "Prepare to commit"
    │
    ├──> Participant A: "OK, ready!" ✅
    ├──> Participant B: "OK, ready!" ✅
    └──> Participant C: "OK, ready!" ✅
```

**Cada participante:**
1. Executa operação
2. Trava recursos (lock)
3. Escreve log
4. Responde "ready" ou "abort"

**Se TODOS "ready" → vai para Fase 2**
**Se ALGUM "abort" → rollback em todos**

---

## 2PC: Fase 2 - Commit

**Todos "ready":**
```
Coordinator: "Commit!"
    │
    ├──> Participant A: Commit ✅
    ├──> Participant B: Commit ✅
    └──> Participant C: Commit ✅
```

**Algum "abort":**
```
Coordinator: "Rollback!"
    │
    ├──> Participant A: Rollback ↩️
    ├──> Participant B: Rollback ↩️
    └──> Participant C: Rollback ↩️
```

**Atomicidade garantida!**

---

## 2PC: Vantagens

✅ **ACID completo:**
- Atomicidade garantida
- Consistência forte
- Isolamento durante prepare
- Durabilidade com logs

---

## 2PC: Vantagens

✅ **Padrão consolidado:**
- Protocolo bem definido
- Implementações maduras
- Suporte em vários bancos (XA transactions)

---

## 2PC: Vantagens

✅ **Garante tudo ou nada:**
- Impossível ter inconsistência
- Commit ou rollback em todos

---

## 2PC: Desvantagens

❌ **Bloqueante (Blocking):**
- Recursos travados durante prepare
- Se coordinator cai, participantes ficam esperando
- Deadlock possível

---

## 2PC: Desvantagens

❌ **Performance:**
- 2 round-trips de rede
- Locks por tempo prolongado
- Throughput limitado

---

## 2PC: Desvantagens

❌ **Ponto único de falha:**
- Coordinator cai = transação trava
- Precisa de recovery complexo

---

## 2PC: Desvantagens

❌ **Não escala:**
- Latência aumenta com participantes
- Não funciona bem em microservices

---

## 2PC: Problemas Reais

**Problema 1: Coordinator cai após Prepare**
```
Phase 1: Todos responderam "ready"
Phase 2: Coordinator cai ANTES de enviar "commit"
         ↓
Participantes travados esperando decisão! 🔒
```

**Solução:** Timeout + assume rollback

---

## 2PC: Problemas Reais

**Problema 2: Participante cai após Prepare**
```
Phase 1: Participante A disse "ready" e cai
Phase 2: Coordinator envia "commit"
         ↓
Participante A não recebe! 💥
```

**Solução:** Coordinator reenviar até ACK (log)

---

## Quando Usar 2PC?

✅ **Use 2PC quando:**

- **Consistência forte obrigatória**
  - Transações financeiras
  - Inventário crítico

---

## Quando Usar 2PC?

- **Poucos participantes (2-3)**
  - Latência aceitável
  - Volume moderado

---

## Quando Usar 2PC?

- **Infraestrutura controlada**
  - Mesma rede
  - Alta confiabilidade

---

## Quando NÃO Usar 2PC?

❌ **Evite 2PC quando:**

- **Microservices distribuídos**
  - Latência de rede alta
  - Serviços independentes

---

## Quando NÃO Usar 2PC?

❌ **Evite 2PC quando:**

- **Alta escala**
  - Locks não escalam
  - Performance crítica

---

## Quando NÃO Usar 2PC?

❌ **Evite 2PC quando:**

- **Disponibilidade > Consistência**
  - Eventual consistency OK
  - CAP theorem (escolha AP)

---

## Quando NÃO Usar 2PC?

❌ **Evite 2PC quando:**

- **Cloud/Serverless**
  - Conexões efêmeras
  - Stateless

**Alternativa:** Use SAGA!

---

<!-- _class: lead -->

# Padrão SAGA

**Transações distribuídas sem 2PC**

---

## O Que é SAGA?

**Problema:**
```
Pedido → Reservar Estoque → Processar Pagamento → Enviar
```

Se **Pagamento falhar**, como reverter **Estoque**?

**SAGA:** Sequência de transações locais com compensação

```
T1 → T2 → T3 → ❌ FALHA
     ↓    ↓
    C2 ← C3 (Compensações)
```

Cada transação tem uma **compensação** (rollback)

---

## SAGA: Tipos

**1. Choreography (Coreografia)** 🎭

Serviços reagem a eventos, sem coordenador central

```
Order → [OrderCreated] → Stock → [StockReserved] 
                               → Payment → [PaymentProcessed]
                                         → Shipping
```

---

## SAGA: Tipos

**1. Choreography (Coreografia)** 🎭

**Vantagens:**
- Desacoplado
- Sem ponto único de falha

**Desvantagens:**
- Difícil de rastrear
- Lógica distribuída

---

## SAGA: Tipos

**2. Orchestration (Orquestração)** 🎼

Coordenador central controla o fluxo

```
         Orchestrator
         /    |    \
      Stock  Pay  Ship
```

---

## SAGA: Tipos

**2. Orchestration (Orquestração)** 🎼

**Vantagens:**
- Lógica centralizada
- Fácil de rastrear
- Controle total

**Desvantagens:**
- Acoplamento ao orquestrador
- Ponto único de falha

---

## SAGA: Quando Usar?

✅ **Use SAGA quando:**
- Microsserviços com transações distribuídas
- Não pode usar 2PC (Two-Phase Commit)
- Precisa de eventual consistency
- E-commerce, reservas, pagamentos

---

## SAGA: Quando Usar?

**Escolha Choreography:** 🎭
- Serviços independentes
- Eventos bem definidos
- Menos acoplamento

---

## SAGA: Quando Usar?

**Escolha Orchestration:** 🎼
- Fluxo complexo
- Precisa de controle central
- Fácil debug

---

<!-- _class: lead -->

# Serverless

**Código sem servidor (na verdade o servidor existe, mas não é você que cuida)**

---

## O Que é Serverless?

**Conceito:**
- Você escreve funções
- Provider executa sob demanda
- Paga por execução (não por servidor)
- Auto-scaling automático

```
Código → Upload → Provider gerencia tudo
                ↓
         Executa quando chamado
         Escala automaticamente
         Cobra por milissegundos
```

---

## O Que é Serverless?

**Providers:**
- AWS Lambda
- Google Cloud Functions
- Azure Functions
- Cloudflare Workers

---

## Serverless: Vantagens

✅ **Zero gerenciamento:**
- Sem servidor para administrar
- Sem patches, updates
- Sem escalar manualmente

---

## Serverless: Vantagens

✅ **Custo:**
- Pay-per-use
- Não paga quando idle
- Sem over-provisioning

---

## Serverless: Vantagens

✅ **Escalabilidade:**
- Auto-scaling instantâneo
- 0 → 1000 requisições/seg
- Sem configuração

---

## Serverless: Vantagens

✅ **Foco no código:**
- Só desenvolve lógica
- Infra é abstraída

---

## Serverless: Desvantagens

❌ **Cold Start:**
- Primeira execução lenta (1-5s)
- Afeta latência
- Mitigação: keep warm

---

## Serverless: Desvantagens

❌ **Limites:**
- Tempo de execução (15 min AWS)
- Memória (10GB AWS)
- Payload (6MB)

---

## Serverless: Desvantagens

❌ **Vendor Lock-in:**
- Difícil migrar
- API específica do provider

---

## Serverless: Desvantagens

❌ **Debugging:**
- Logs distribuídos
- Difícil reproduzir local

---

## Serverless: Desvantagens

❌ **Custos imprevisíveis:**
- Alto tráfego = $$$
- DDoS pode sair caro

---

## Serverless: Quando Usar?

✅ **Ideal para:**

- **Workloads esporádicos:**
  - Webhooks
  - Processamento batch noturno
  - CRON jobs

---

## Serverless: Quando Usar?

✅ **Ideal para:**

- **APIs com tráfego variável:**
  - Spikes imprevisíveis
  - Baixo tráfego constante

---

## Serverless: Quando Usar?

✅ **Ideal para:**

- **Event-driven:**
  - Processar uploads S3
  - DynamoDB streams
  - IoT events

---

## Serverless: Quando Usar?

✅ **Ideal para:**

- **Backend for frontend:**
  - Agregação de APIs
  - Transformação de dados

---

## Serverless: Quando Evitar?

❌ **Evite para:**

- **Latência crítica:**
  - Trading de alta frequência
  - Games real-time

---

## Serverless: Quando Evitar?

❌ **Evite para:**

- **Processamento longo:**
  - > 15 minutos
  - Machine Learning pesado

---

## Serverless: Quando Evitar?

❌ **Evite para:**

- **Alto tráfego constante:**
  - Pode sair mais caro que servidor
  - 1M req/dia = considere servidor

---

## Serverless: Quando Evitar?

❌ **Evite para:**

- **State complexo:**
  - Stateless por design
  - Difícil manter conexões

---

<!-- _class: lead -->

# Atividades Práticas

**4 desafios reais para aplicar o conhecimento**

---

# Atividades Práticas

## Como Funciona?

**Divisão:**
- 4 grupos
- 1 problema por grupo
- Tempo: 60 minutos

---

# Atividades Práticas

**Entregáveis:**
1. Mapeamento do problema
2. Escopo essencial (MVP)
3. Tradeoffs identificados
4. Desenho da arquitetura
5. Tecnologias escolhidas (linguagem, banco, etc)

---

# Atividades Práticas

**Apresentação:** 5-7 minutos por grupo

---

## Atividade 1: Plataforma de Cursos

**Problema:**
Criar uma plataforma de cursos

**Requisitos:**
- Catálogo de cursos e video aulas
- Perfis de usuários
- Histórico de visualização
- Sistema de assinaturas

**Constraints:**
- 1000 usuários esperados nos proximos 6 meses
- Prazo: 6 meses MVP

---

## Atividade 1: O Que Mapear?

**Problema central:**
- Armazenamento e entrega de conteúdo em escala

**Escopo essencial (MVP):**
- O que DEVE ter no MVP?
- O que pode ficar pra depois?

**Tecnologias:**
- Linguagem, banco, cache, CDN, cloud

---

## Atividade 2: Sistema de Delivery

**Problema:**
Criar app de delivery de comida estilo iFood

**Requisitos:**
- Cardápio digital
- Carrinho de compras
- Pagamento online
- Avaliações e reviews
- Chat entre cliente/restaurante/entregador

**Constraints:**
- 100 pedidos/dia esperado no primeiro ano
- Prazo: 4 meses MVP

---

## Atividade 2: O Que Mapear?

**Problema central:**
- Gerenciamento de estado dos pedidos em tempo real

**Escopo essencial (MVP):**

- Quais features são críticas?

**Tecnologias:**

- Linguagem, banco, cache, CDN, cloud

---

## Atividade 3: Carteira de pagamentos

**Problema:**
Criar um banco digital com conta corrente e investimentos

**Requisitos:**
- Transferências (TED, PIX)
- Extrato e comprovantes
- Controle de Saldo
- Notificações de transações

**Constraints:**
- Transações precisam ser sincronas
- Prazo: 8 meses MVP

---

## Atividade 3: O Que Mapear?

**Problema central:**

- Transações financeiras seguras e auditáveis

**Escopo essencial (MVP):**

- Quais features são críticas?

**Tecnologias:**

- Linguagem, banco, cache, CDN, cloud

---

## Atividade 4: Marketplace B2C

**Problema:**
Criar marketplace B2C

**Requisitos:**
- Catálogo de produtos (SKU)
- Múltiplos fornecedores
- Faturamento e NF-e
- Analytics e relatórios

**Constraints:**
- Prazo: 5 meses MVP

---

## Atividade 4: O Que Mapear?

**Problema central:**

- Entregar experiencia de compra otimizada

**Escopo essencial (MVP):**

- Quais features são críticas?

**Tecnologias:**

- Linguagem, banco, cache, CDN, cloud

---

## Mãos à Obra!

**Boa sorte! 🚀**

_Lembre-se: não existe solução perfeita, existe a melhor para o contexto!_

---

<!-- _class: lead -->

`Conceitual`
# Cloud, Containers, CI & CD
**Infraestrutura moderna e deployment automatizado**

---

## Cloud: Fundamentos

**Benefícios:**

- Escalabilidade sob demanda
- Pay-as-you-use
- Alta disponibilidade
- Manutenção reduzida

---

## Por Que Containers?

**Problemas tradicionais:**
- "Funciona na minha máquina" 🤷‍♂️
- Dependências conflitantes
- Ambientes inconsistentes com deploy manual e propenso a erro

**Containers resolvem:**
- Ambiente padronizado
- Isolamento de recursos
- Portabilidade total com deploy consistente

---

## Docker: Best Practices

<div class="horizontal-align">

<div>

✅ **Boas práticas:**
- Use `.dockerignore` (como .gitignore)
- Multi-stage builds para imagens menores
- Não rode como root
- Versione suas imagens (`app:v1.2.3`)

</div>

<div>

❌ **Evite:**
- Instalar tudo numa imagem só
- Senhas hardcoded
- Logs dentro do container
- Dados importantes em volumes não persistentes

</div>

</div>

---

## Kubernetes: Conceitos

<div class="horizontal-align">

<div>

**Cluster** 🏢
- Conjunto de máquinas (nodes)
- Master node (control plane) + Worker nodes

</div>

<div>

**Pod** 📦
- Menor unidade deployável
- Um ou mais containers
- Compartilham rede e storage

</div>

<div>

**Service** 🌐
- Abstração para acessar pods
- Load balancer interno
- DNS interno

</div>

</div>

---

## Kubernetes: Quando Usar?

<div class="horizontal-align">

<div>

✅ **Use Kubernetes quando:**
- Múltiplos microsserviços
- Necessita auto-scaling complexo
- High availability crítica
- Time DevOps experiente
- Orquestração sofisticada necessária

</div>

<div>

❌ **Evite quando:**
- Aplicação simples (monólito pequeno)
- Time sem experiência K8s
- Overhead não justifica (poucas aplicações)
- Cloud-managed alternatives suficientes (ECS, Cloud Run)

</div>

</div>

---

## Infrastructure as Code (IaC)

<div class="horizontal-align">

<div>

**O que é?**
- Infraestrutura definida em código
- Versionada, testável, reproduzível
- Declarativo (descreve estado desejado)

</div>

<div>

**Ferramentas:**
- **Terraform** - Multi-cloud, mais usado
- **CloudFormation** - AWS específico
- **Ansible** - Configuration management

</div>

</div>

---

## IaC: Benefícios

✅ **Vantagens:**
- **Reprodutível** - Mesmo ambiente sempre
- **Versionado** - Git para infraestrutura
- **Testável** - Validação antes deploy
- **Documentação viva** - Código é a documentação
- **Rollback** - Voltar versão anterior
- **Collaboration** - Code review para infra

---

## CI/CD: Conceitos

<div class="horizontal-align">

<div>

**Continuous Integration (CI)** 🔄
- Integração contínua de código
- Testes automatizados
- Build automatizado
- Feedback rápido

</div>

<div>

**Continuous Delivery (CD)** 🚀

- Deploy automatizado para staging
- Release manual para produção
- Sem intervenção manual

</div>

</div>

---

## Pipeline: Best Practices

<div class="horizontal-align">

<div>

✅ **Faça:**
- **Fail fast** - Testes rápidos primeiro
- **Parallel execution** - Execute em paralelo quando possível
- **Immutable deployments** - Nova versão, não atualizar existente
- **Rollback strategy** - Sempre tenha plano de volta
- **Monitoring** - Alertas em cada estágio

</div>

<div>

❌ **Evite:**
- Testes lentos no início
- Deploy manual de emergência
- Secrets hardcoded
- Pipeline sem rollback

</div>

</div>

---

## Auto Scaling: Estratégias

<div class="horizontal-align">

<div>

**Reactive Scaling** 📊
- Baseado em métricas atuais
- CPU, memória, fila, requests/sec
- Resposta após problema aparecer

</div>

<div>

**Predictive Scaling** 🔮
- Baseado em padrões históricos
- Machine learning
- Antecipa demanda

</div>

<div>

**Scheduled Scaling** 📅
- Baseado em horários conhecidos
- Black Friday, lunch time
- Previsível

</div>

</div>

---

## Monitoring e Observabilidade

**Três Pilares:**

<div class="horizontal-align">

<div>

**Metrics** 📊 ($)
- CPU, memória, latência, throughput
- Dashboards
- Alertas

</div>

<div>

**Traces** 🔍 ($)

- Request flow entre serviços
- Indentificar gargalos
- Distributed tracing

</div>

<div>

**Logs** 📝 ($$$)
- Eventos da aplicação
- Structured logging (JSON)
- Centralizados

</div>

</div>

---

## Alerting: Boas Práticas

<div class="horizontal-align">

<div>

✅ **Configure alertas para:**
- **Sintomas** do usuário (latência alta, errors)
- **Causas** técnicas (CPU alto, disk full)
- **Tendências** (crescimento insustentável)

</div>

<div>

❌ **Evite:**
- Alert fatigue (muitos alertas desnecessários)
- Alertas sem ação clara
- Alertas apenas para métricas técnicas

</div>

</div>

**Regra de ouro:** Se não é acionável, não alerte!

---

## Otimização de custos

**Estratégias:**

<div class="horizontal-align">

<div>

**Right-sizing** 📏
- Monitor uso real de CPU/memória
- Adjust requests/limits
- Remove recursos ociosos

</div>

<div>

**Spot/Preemptible Instances** 💰
- 60-90% mais barato
- Para workloads tolerantes a interrupção
- Batch jobs, development environments

</div>

<div>

**Reserved Instances** 💳
- Commit de 1-3 anos
- 30-60% desconto
- Para workloads estáveis

</div>

</div>

---

## Blue-Green Deployment

**Estratégia:**
- Dois ambientes idênticos (blue/green)
- Deploy nova versão no ambiente inativo
- Switch de tráfego instantâneo
- Rollback rápido se necessário

---

## Canary Deployment

**Estratégia:**
- Deploy gradual (5% → 25% → 50% → 100%)
- Monitor métricas em cada fase
- Rollback automático se métricas degradam

---

<!-- _class: lead -->

`Conceitual`
# Segurança

**Protegendo sistemas e dados**

---

## Por Que Segurança Importa?

**Cenário atual:**
- Ataques cibernéticos crescem 600% ao ano
- Custo médio de breach: $4.45 milhões
- Regulamentações rigorosas (LGPD, GDPR)
- Reputação da empresa em risco

**Princípio fundamental:**
_Security by Design, não Security by Patch_

---

## Programação Defensiva

**Mentalidade:**
- Assuma que tudo pode falhar
- Valide TODAS as entradas
- Nunca confie em dados externos
- Fail securely (falhe de forma segura)

---

## Programação Defensiva: Input Validation

❌ **Nunca confie:**
```php
$sql = "SELECT * FROM users WHERE id = " . $_GET['id'];

$file = $_POST['filename'];
file_get_contents($file);
```

✅ **Sempre valide:**
```php
$id = filter_var($_GET['id'], FILTER_VALIDATE_INT);
if ($id === false) {
    throw new InvalidArgumentException('ID deve ser inteiro');
}

$filename = basename($_POST['filename']);
if (!preg_match('/^[a-zA-Z0-9._-]+$/', $filename)) {
    throw new InvalidArgumentException('Filename inválido');
}
```

---

## Programação Defensiva: Sanitização

**Princípios:**
- **Whitelist** > Blacklist
- **Escape** output baseado no contexto
- **Encode** para formato correto

```php
// HTML Context
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// SQL Context
$stmt = $pdo->prepare("SELECT * FROM users WHERE name = ?");
$stmt->execute([$userInput]);

// JavaScript Context
echo json_encode($userInput, JSON_HEX_TAG | JSON_HEX_AMP);
```

---

## Programação Defensiva: Error Handling

❌ **Nunca exponha detalhes:**
```php
catch (Exception $e) {
    echo $e->getMessage();
    // "Connection failed: mysql://root:senha123@localhost"
}
```

✅ **Fail securely:**
```php
catch (Exception $e) {
    // Resposta genérica para usuários
    http_response_code(500);
    echo json_encode(['error' => 'Erro interno do servidor']);
}
```

---

## Autenticação vs Autorização

<div class="horizontal-align">

<div>

**Autenticação** 🔑
- **Quem** você é?
- Login/senha, 2FA, biometria
- Confirma identidade

</div>

<div>

**Autorização** 🚪
- **O que** você pode fazer?
- Permissions, roles, ACL
- Controla acesso

</div>

</div>

_Ambos necessários para segurança completa_

---

## Autenticação: Boas Práticas

<div class="horizontal-align">

<div>

✅ **Multi-Factor Authentication (MFA)**
```
Algo que você sabe (senha)
+ 
Algo que você tem (celular)
+
Algo que você é (biometria)
```

</div>

<div>

✅ **Senhas seguras:**
- Mínimo 12 caracteres
- Complexidade obrigatória
- Hash com salt (bcrypt, Argon2)
- Rate limiting em tentativas

</div>

</div>

---

## Criptografia: Conceitos

<div class="horizontal-align">

<div>

**Simétrica** 🔐
- Mesma chave para cifrar e decifrar
- Rápida, ideal para volumes grandes
- AES-256-GCM

</div>

<div>

**Assimétrica** 🔐🔓
- Par de chaves (pública/privada)
- Lenta, ideal para troca de chaves
- RSA, ECC

</div>

<div>

**Hash** #️⃣
- Via única (não reversível)
- Verifica integridade
- SHA-256, SHA-3

</div>

</div>

---

## Criptografia: Quando Usar?

<div class="horizontal-align">

<div>

**Dados em Trânsito** 🚀
- HTTPS (TLS) sempre
- VPN para comunicação interna
- Certificados válidos

</div>

<div>

**Dados em Repouso** 💾
- Encrypt database
- Encrypt backups
- Encrypt logs sensíveis

</div>

</div>

---

## Rate Limiting

**Por que?**
- Prevenir DDoS
- Evitar brute force
- Proteger APIs caras
- Garantir fair usage

---

## Cuidados com Cloud

**Shared Responsibility Model**
```
Cloud Provider é responsável por:
- Segurança DA cloud (física, rede, hypervisor)

Você é responsável por:
- Segurança NA cloud (dados, apps, configuração)
```

---

## Cloud Security: IAM

**Princípios:**
- **Least Privilege** - Mínimos privilégios necessários
- **Zero Trust** - Nunca confie, sempre verifique
- **Defense in Depth** - Múltiplas camadas

---

## Cloud Security: Network

**VPC (Virtual Private Cloud)**
- Rede isolada
- Subnets públicas e privadas
- Security Groups (firewall)
- NACLs (Network ACL)

**Best Practices:**
- Nunca exponha DB diretamente
- WAF para aplicações web
- DDoS protection sempre ativo

---

## OWASP Top 10 (2021)

1. **Broken Access Control** 🚪
2. **Cryptographic Failures** 🔐
3. **Injection** 💉
4. **Insecure Design** 🏗️
5. **Security Misconfiguration** ⚙️
6. **Vulnerable Components** 📦
7. **Authentication Failures** 🔑
8. **Software Integrity Failures** ✅
9. **Logging & Monitoring Failures** 📊
10. **Server-Side Request Forgery** 🌐

_Estude cada um destes!_

---

## Security Testing

<div class="horizontal-align">

<div>

**SAST (Static Analysis)**
- Analisa código fonte
- Detecta vulnerabilidades conhecidas
- Integra no CI/CD
- Ferramentas: SonarQube, Checkmarx

</div>

<div>

**DAST (Dynamic Analysis)**
- Testa aplicação rodando
- Black-box testing
- Ferramentas: OWASP ZAP, Burp Suite

</div>

<div>

**IAST (Interactive Analysis)**
- Combina SAST + DAST
- Real-time analysis

</div>

</div>

---

<!-- _class: lead -->

# Cultura de Aprendizado Contínuo

---

## Por Que Aprendizado Contínuo?

**Cenário tecnológico:**
- Novas tecnologias surgem constantemente
- Mercado valoriza adaptabilidade
- Times que aprendem juntos performam melhor

**Princípio fundamental:**
_Learning Organizations > Individual Expertise_

---

## Documentação: Por Que Importa?

**Problemas sem documentação:**
- "Conhecimento na cabeça" de uma pessoa
- Onboarding lento e frustrante
- Decisões repetidas sem contexto
- Perda de conhecimento quando pessoas saem

---

## Documentação: Por Que Importa?

**Benefícios:**
- Reduz dependência de pessoas específicas
- Acelera onboarding
- Preserva contexto histórico
- Facilita manutenção

---

## Documentação: O Que Documentar?

**Arquitetura** 🏗️
- Decisões arquiteturais (ADRs)
- Diagramas de componentes
- Fluxos de dados
- Trade-offs escolhidos

**Processos** ⚙️
- Como fazer deploy
- Como debugar problemas comuns
- Runbooks para emergências
- Guidelines de desenvolvimento

---

## Documentação: O Que Documentar?

**Contexto** 🧠
- Por que escolhemos X e não Y?
- Qual problema estávamos resolvendo?
- Quais foram as restrições na época?
- Lições aprendidas

**Código** 💻
- README com setup
- Comentários explicando "porquê", não "como"
- Exemplos de uso
- APIs e contratos

---

## ADR: Architecture Decision Records

**O que é?**
- Documento que captura decisões arquiteturais importantes
- Contexto, decisão, consequências
- Imutável (histórico de decisões)

---

## Documentação: Como Manter Atualizada?

✅ **Estratégias que funcionam:**

**Definition of Done inclui docs**
- Pull request sem docs = não aceito
- Mudança arquitetural = ADR obrigatório

**Docs próximas ao código**
- README no repositório
- Docs em Markdown versionadas
- Diagramas como código (PlantUML, Mermaid)

---

## Documentação: Como Manter Atualizada?

**Review de documentação**
- Quarterly doc review
- Métricas: docs acessadas vs não acessadas

**Automação**
- API docs geradas automaticamente
- Diagramas atualizados por CI
- Links quebrados detectados automaticamente

---

## Documentação: Antipadrões

❌ **Evite:**

**Wiki separado do código**
- Fica desatualizado rapidamente
- Desenvolvedores esquecem de atualizar

**Documentação excessiva**
- Documentar o óbvio
- Duplicar o que o código já expressa

**Vamos documentar depois**
- Nunca acontece na prática

---

## Code Review: Além de Bugs

**Objetivos:**
- ✅ Encontrar bugs
- ✅ **Compartilhar conhecimento**
- ✅ **Manter consistência**
- ✅ **Mentorar desenvolvedores**
- ✅ **Discutir design**

_Code review é uma das melhores ferramentas de aprendizado!_

---

## Code Review: O Que Revisar?

<div class="horizontal-align">

<div>

**Funcionalidade** 🎯
- Código faz o que deveria?
- Edge cases considerados?
- Performance adequada?

</div>

<div>

**Design** 🏗️
- Abstração apropriada?
- Segue padrões estabelecidos?
- SOLID principles?

</div>

<div>

**Legibilidade** 📖
- Nomes claros?
- Função pequenas?
- Comentários necessários?

</div>

</div>

<div class="horizontal-align">

<div>

**Segurança** 🔒
- Input validation?
- SQL injection risks?
- Secrets hardcoded?

</div>

<div>

**Testes** 🧪
- Testes suficientes?
- Casos importantes cobertos?
- Testes legíveis?

</div>

<div>

**Documentação** 📚
- README atualizado?
- API docs necessárias?
- Comentários explicativos?

</div>

</div>

---

## Code Review: Como Fazer Bem?

✅ **Para quem revisa:**

**Seja construtivo, não destrutivo**
❌ "Esse código está uma porcaria"
✅ "Que tal extrairmos essa lógica para uma função?"

**Explique o porquê**
❌ "Mude isso"
✅ "Isso pode causar memory leak porque..."

**Sugira soluções**
❌ "Está errado"
✅ "Que tal usarmos Strategy pattern aqui?"

---

## Code Review: Como Fazer Bem?

**Aprenda também**
- "Interessante essa abordagem, por que escolheu?"
- "Não conhecia essa lib, como funciona?"

**Priorize feedback**
- **Critical:** Security, bugs sérios
- **Major:** Performance, design
- **Minor:** Estilo, naming

**Seja específico**
❌ "Tem problema na linha 50"
✅ "Linha 50: variable $user pode ser null"

---

## Code Review: Para Quem Submete

✅ **Boas práticas:**

<div class="horizontal-align">

<div>

**PRs pequenos e focados**
- Máximo 400 linhas
- Uma feature/fix por PR
- Facilita revisão de qualidade

</div>

<div>

**Contexto claro**
- Descreva o problema resolvido
- Link para issue/ticket
- Screenshots se UI

</div>

<div>

**Self-review primeiro**
- Revise seu próprio código
- Teste locally

</div>

</div>

<div class="horizontal-align">

<div>

**Responda construtivamente**
- Agradeça feedback
- Explique seu raciocínio se discordar
- Faça perguntas para entender

</div>

<div>

**Aprenda com feedback**
- Note padrões nos comentários
- Melhore para próxima vez
- Não leve para o pessoal

</div>

</div>

---

## Arquiteto como Guia Turístico

**Guia turístico** vs **Arquiteto Civil**

<div class="horizontal-align">

<div>

❌ **Arquiteto Civil:**
- "Façam exatamente como eu digo"
- Decisões top-down sem explicação
- Não ouve feedback do time
- Cria dependência total

</div>

<div>

✅ **Guia turístico:**
- "Deixem-me mostrar o caminho"
- Explica o porquê das decisões
- Adapta rota baseado no grupo
- Ensina a pescar

</div>

</div>

---

## Arquiteto como Guia: Características

<div class="horizontal-align">

<div>

**Conhece o território** 🗺️
- Domina tecnologias e padrões
- Entende trade-offs
- Conhece as armadilhas comuns
- Experiência prática

</div>

<div>

**Adapta ao grupo** 👥
- Considera skill level do time
- Ajusta complexidade da solução
- Respeita constraints (tempo, budget)
- Evolui arquitetura gradualmente

</div>

</div>

<div class="horizontal-align">

<div>

**Ensina durante a jornada** 🎓
- Explica decisões arquiteturais
- Faz pair programming
- Documenta raciocínio
- Responde perguntas pacientemente

</div>

<div>

**Permite exploração** 🔍
- Deixa time descobrir alguns caminhos
- Intervém só quando necessário
- Encourage experimentação controlada
- Learn from mistakes together

</div>

</div>

---

## Shuhari: Jornada de Aprendizado

**Conceito do Aikido aplicado ao desenvolvimento:**

<div class="horizontal-align">

<div>

**守 (Shu) - Proteger/Obedecer** 👨‍🎓
- Seguir regras e formas estabelecidas
- Imitar mestres
- Não questionar ainda
- Foco na execução correta

</div>

<div>

**破 (Ha) - Quebrar/Desprender** 🔄
- Entender princípios por trás das regras
- Começar a modificar e adaptar
- Questionar quando apropriado
- Desenvolver estilo próprio

</div>

<div>

**離 (Ri) - Deixar/Separar** 🧙‍♂️
- Transcender formas tradicionais
- Criar novos caminhos
- Ensinar outros
- Inovação baseada em maestria

</div>

</div>

---

## Shuhari: Aplicado ao Desenvolvimento

**Shu - Seguir Padrões** 👨‍🎓
```
Junior Developer:
- Segue style guide religiosamente
- Usa patterns estabelecidos
- Copia soluções que funcionam
- Foco: não quebrar nada
```

**Exemplo:** Sempre usar Repository pattern, mesmo em CRUDs simples

---

## Shuhari: Aplicado ao Desenvolvimento

**Ha - Adaptar Contexto** 🔄
```
Mid-level Developer:
- Entende quando quebrar regras
- Adapta patterns ao contexto
- Questiona decisões arquiteturais
- Foco: soluções apropriadas
```

**Exemplo:** "Repository é overhead aqui, mas Event Sourcing faz sentido"

---

## Shuhari: Aplicado ao Desenvolvimento

**Ri - Criar Novos Caminhos** 🧙‍♂️
```
Senior/Arquiteto:
- Cria novos patterns
- Define padrões para o time
- Innovation based on deep understanding
- Foco: evoluir a arte
```

**Exemplo:** Criar novo pattern específico para o domínio da empresa

---

## Shuhari: Para Líderes Técnicos

<div class="horizontal-align">

<div>

**Com Juniors (Shu):**
- Forneça regras claras
- Code reviews detalhados
- Pair programming frequente
- Não sobrecarregue com opções

</div>

<div>

**Com Plenos (Ha):**
- Explique o porquê das regras
- Encoraje experimentação controlada
- Discuta trade-offs
- Permita erros educativos

</div>

<div>

**Com Seniors (Ri):**
- Dê autonomia total
- Facilite compartilhar conhecimento
- Desafios complexos
- Deixe eles inovarem

</div>

</div>

---

## Obrigado

### E você, o que acha?
_`@eudiegoborgs`_
<div class="conduta">

![Feedback](./assets/feedback.png)
_Deixe aqui seu Feedback_

</div>
