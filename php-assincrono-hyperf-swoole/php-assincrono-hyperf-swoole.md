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

### PHP Assíncrono
## com Hyperf e Swoole
_performance e concorrência no mundo PHP_

---

### Introdução

## Programação Concorrente

---

## Blocking I/O x Non-blocking I/O
O Swoole transforma o PHP que é nativo Blocking I/O em Non-blocinkg I/O

---

### Blocking I/O

_o processo **espera** a resposta antes de continuar_

```
Requisição 1 (377ms): ██==WAIT QUERY DB==[RESPONSE]
Requisição 2 (434ms):                              ██==WAIT HTTP API==[RESPONSE]
Requisição 3 (280ms):                                                           ██==WAIT CACHE==[RESPONSE]

-------

Legendas
Em execução █
Aguardando resposta ==
```

⏱️ Tempo total = soma de todas as operações (1091ms)

---

### Non-blocking I/O

_o processo **não espera**, executa outras tarefas_

```
Requisição 1 (377ms): ██=====WAIT QUERY DB=====██[RESPONSE]
Requisição 2 (434ms):   ██========WAIT HTTP API========██[RESPONSE]
Requisição 3 (280ms):     ██==WAIT CACHE==██[RESPONSE]

-------

Legendas
Em execução █
Aguardando resposta ==
```

⚡ Tempo total = tempo da operação mais lenta (434ms)

---
### Qual a diferença entre
## Paralelismo x Concorrência
Com o Swoole o PHP trabalha de forma concorrente

---

### Paralelismo

_executar **múltiplas tarefas ao mesmo tempo**_
_requer múltiplos núcleos de CPU_

```
CPU Core 1: ████████████████
CPU Core 2: ████████████████
CPU Core 3: ████████████████
```

---

### Concorrência

_gerenciar **múltiplas tarefas alternando** entre elas_
_um único núcleo pode ser concorrente_

```
Somente 1 core: 
Tarefa A: ██==████==██
Tarefa B:   ██====██
Tarefa C:           ██==██

-------

Legendas
Em execução █
Aguardando resposta ==
```

---

### Na prática

- 🍳 **Paralelismo**: 3 cozinheiros 
    - 1 faz o arroz
    - 1 faz a batata frita
    - 1 faz a carne
- 🧑‍🍳 **Concorrência**: 1 cozinheiro
    - Começa a fazer o arroz
    - Enquanto espera cozinhar coloca a bata para fritar
    - Enquanto aguarda a evolução dos anteriores faz a carne
    - Alterna entre eles enquanto a ocio nas outras tarefas

_O Swoole trabalha com **concorrência** via corrotinas_

---

## Stateless x Stateful

---

### Stateless (PHP Tradicional)

- Cada requisição **recria tudo** do zero
- Conexões, variáveis, objetos: **nasce e morre**
- Escala horizontal fácil
- ⚠️ Desperdício de recursos

---

### Stateful (Swoole)

- Estado **persiste entre requisições**
- Conexões e objetos **reutilizados**
- Pool de conexões nativo
- ⚡ Menos overhead, mais performance

---

## Como o PHP funciona tradicionalmente?

---

### Ciclo de vida do PHP-FPM

```
Requisição → Nginx → PHP-FPM → Bootstrap → Executa → Responde → Morre ☠️
```

- Cada request = **novo processo**
- Autoload, config, DI container: **recriados**
- Conexão com DB: **aberta e fechada**
- Memória: **alocada e liberada**

---

### O problema

```
Request 1: [--bootstrap--][--DB connect--][--logic--][--response--] ☠️
Request 2: [--bootstrap--][--DB connect--][--logic--][--response--] ☠️
Request 3: [--bootstrap--][--DB connect--][--logic--][--response--] ☠️
```

_O bootstrap pode consumir **mais tempo** que a lógica em si_

---

## Como o Swoole entra na história?

---

### Ciclo de vida do Swoole

```
Server Start → Bootstrap (1x) → Worker Ready ♻️
  ├── Request 1 → Executa → Responde
  ├── Request 2 → Executa → Responde
  └── Request N → Executa → Responde
```

- Bootstrap acontece **uma única vez**
- Workers persistentes em memória
- Conexões **reutilizadas** via pool

---

### Reaproveitamento de recursos

```
Swoole Worker:
  ✅ DI Container    → carregado 1x
  ✅ Config          → carregado 1x
  ✅ DB Connections  → pool compartilhado
  ✅ Coroutines      → I/O não-bloqueante
```

_Resultado: **2x a 5x** mais performance_

---

### A analogia da marmita 🍱

- **PHP-FPM**: cozinhar do zero toda vez que bater fome
  - Lavar panela, picar legumes, temperar, cozinhar... _toda vez_
  - ⏱️ Lento, repetitivo e cansativo

- **Swoole**: fazer o _meal prep_ da semana
  - Cozinha tudo de uma vez no domingo
  - Nos outros dias: **pega a marmita e come** 🚀
  - Mesma refeição, **fração do tempo**

_O bootstrap é o "domingo de cozinha" — acontece **uma única vez**_

---

### Event Loop

_Um loop infinito que monitora e despacha eventos de I/O_

```
  ┌─────────────────────────────────────────────┐
  │               Event Loop                    │
  │                                             │
  │  1. Verifica eventos prontos (epoll/kqueue) │
  │  2. Despacha callbacks registrados          │
  │  3. Retoma corrotinas suspensas             │
  │  4. Processa timers expirados               │
  │  5. Volta ao passo 1                        │
  └─────────────────────────────────────────────┘
```

---

### Event Loop: o ciclo passo a passo

```
Corrotina A: consulta banco ──► SUSPENDE (aguarda I/O)
                                     │
                              Event Loop assume
                                     │
Corrotina B: requisição HTTP ──► SUSPENDE (aguarda I/O)
                                     │
                              Event Loop assume
                                     │
         [DB retorna resultado] ──► RETOMA Corrotina A ──► continua execução
         [HTTP retorna resposta] ──► RETOMA Corrotina B ──► continua execução
```

_A thread nunca fica ociosa esperando — sempre há algo sendo executado_

---

### Event Loop: por dentro

```
Thread principal (1 core):
  ├── Corrotina A: lógica de negócio     ← executando
  ├── Corrotina B: aguarda DB            ← suspensa (I/O)
  ├── Corrotina C: aguarda HTTP API      ← suspensa (I/O)
  └── Corrotina D: aguarda Redis         ← suspensa (I/O)

Event Loop monitora:
  ├── Socket do DB    → pronto? retoma B
  ├── Socket da API   → pronto? retoma C
  └── Socket do Redis → pronto? retoma D
```

_Centenas de corrotinas concorrentes em uma única thread_

---

## O que é o Hyperf?

---

### Hyperf

- Framework **alto desempenho** baseado em Swoole
- Inspirado no **Laravel**
- **Corrotinas nativas** em todo o framework
- Injeção de dependências via **container**
- Compatível com **PSR standards**

Por ser baseado no laravel, passamos a ter performance muito superior com poucos ajustes na forma de desenvolver.

---

### Hyperf: Ecossistema completo

🔧 **Core**: Router, Middleware, DI, AOP
📦 **Data**: Eloquent ORM, Migrations, Redis
🌐 **Network**: gRPC, WebSocket, JSON-RPC
📊 **Obs**: Logging, Metrics, Tracing
⚙️ **Infra**: Circuit Breaker, Rate Limiter, Cron

---

### Tradeoffs

## Vale a pena usar Hyperf + Swoole?

---

### ✅ Vantagens

- **Performance**: 2x a 10x mais requisições/segundo
- **Corrotinas nativas**: I/O não-bloqueante sem callbacks
- **Estado persistente**: bootstrap e conexões reutilizados
- **Ecossistema rico**: gRPC, WebSocket, filas, circuit breaker
- **Familiar**: sintaxe parecida com Laravel/Lumen

---

### ⚠️ Desafios

- **Curva de aprendizado**: corrotinas, state management e ciclo de vida diferentes
- **Memória compartilhada**: vazamentos persistem entre requisições
- **Variáveis globais**: singletons e `$_SERVER` não funcionam como esperado
- **Bibliotecas bloqueantes**: nem toda lib PHP é compatível com Swoole
- **Debug mais complexo**: stack traces de corrotinas são diferentes
- **Observabilidade**: Muitas libs se baseiam no FPM para oferecer obsrvabilidade

---

### 🧠 Cuidados com estado (stateful)

```php
// ❌ Problema: variável estática persiste entre requisições
class UserContext {
    public static ?User $current = null; // vaza entre requests!
}

// ✅ Correto: usar Context do Swoole por corrotina
class UserContext {
    public static function set(User $user): void {
        Context::set('current_user', $user);
    }
    public static function get(): ?User {
        return Context::get('current_user');
    }
}
```

---

### 🤔 Quando usar?

| Cenário | Recomendação |
|---|---|
| Alta concorrência (APIs, gateways) | ✅ Ótimo fit |
| I/O intensivo (DB, HTTP, cache) | ✅ Ótimo fit |
| Microsserviços com gRPC | ✅ Ótimo fit |
| Apps CRUD simples, baixo tráfego | ⚠️ Overhead desnecessário |
| Equipe sem experiência em async | ⚠️ Avaliar curva de aprendizado |
| Libs legadas bloqueantes no core | ❌ Evitar |

---

# Mãos à obra
## Criando um projeto Hyperf do zero

---

### Instalação

```bash
composer create-project hyperf/hyperf-skeleton my-app

cd my-app
php bin/hyperf.php start
```

_Servidor HTTP rodando em `http://0.0.0.0:9501`_ 🚀

---

### Controller

```php
// app/Controller/UserController.php

#[Controller(prefix: '/users')]
class UserController extends AbstractController
{
    #[Inject]
    private UserService $userService;

    #[GetMapping(path: '')]
    public function index(): array
    {
        return $this->userService->all();
    }

    #[PostMapping(path: '')]
    public function store(RequestInterface $request): array
    {
        return $this->userService->create(
            $request->all()
        );
    }
}
```

---

### Model (Eloquent)

```php
// app/Model/User.php

#[Table(table: 'users')]
class User extends Model
{
    protected array $fillable = [
        'name', 'email', 'password'
    ];

    protected array $hidden = ['password'];
}
```

_Sim, é o Eloquent que você já conhece_ ✅

---

### Migration

```php
// migrations/create_users_table.php

class CreateUsersTable extends Migration
{
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password');
            $table->timestamps();
        });
    }
}
```

```bash
php bin/hyperf.php migrate
```

---

### Seeder

```php
// seeders/UserSeeder.php

class UserSeeder extends Seeder
{
    public function run(): void
    {
        User::create([
            'name'     => 'Diego Borges',
            'email'    => 'diego@example.com',
            'password' => password_hash('secret', PASSWORD_DEFAULT),
        ]);
    }
}
```

```bash
php bin/hyperf.php db:seed
```

---

### Middleware

```php
// app/Middleware/AuthMiddleware.php

#[Middleware]
class AuthMiddleware implements MiddlewareInterface
{
    public function process(
        ServerRequestInterface $request,
        RequestHandlerInterface $handler
    ): ResponseInterface {
        $token = $request->getHeaderLine('Authorization');

        if (empty($token)) {
            throw new UnauthorizedException();
        }

        return $handler->handle($request);
    }
}
```

---

### Injeção de Dependências

```php
// via Annotation
class UserController
{
    #[Inject]
    private UserService $service;
}

// via Constructor
class UserService
{
    public function __construct(
        private UserRepositoryInterface $repo
    ) {}
}
```

---

### Configurando DI

```php
// config/autoload/dependencies.php

return [
    UserRepositoryInterface::class
        => UserRepository::class,
];
```

_Mapeamento de interface → implementação_

---

### Laravel x Hyperf — Comparativo

| Feature | Laravel | Hyperf |
|---------|---------|--------|
| ORM | Eloquent | Eloquent ✅ |
| Migrations | Artisan | Hyperf CLI ✅ |
| DI | Container | Annotations ✅ |
| Middleware | PSR-15 like | PSR-15 ✅ |
| Performance | ~500 req/s | ~5000 req/s 🚀 |

---

# Benchmark
## Laravel x Laravel Octane x Hyperf

---

### Cenário do teste

- **Endpoint**: `GET /users` (10 registros do banco)
- **Ferramenta**: wrk / Apache Bench
- **Condições**: mesma máquina, mesmo banco

---

### Laravel (PHP-FPM)

```
Requests/sec:    ~500
Avg Latency:     ~45ms
Memory/worker:   ~30MB
```

- Cada request = novo bootstrap
- Nova conexão com DB a cada request

---

### Laravel Octane (Swoole)

```
Requests/sec:    ~2.500
Avg Latency:     ~12ms
Memory/worker:   ~50MB (persistente)
```

- Bootstrap **uma vez**
- Pool de conexões
- ⚠️ Cuidados com estado

---

### Hyperf (Swoole nativo)

```
Requests/sec:    ~5.000+
Avg Latency:     ~5ms
Memory/worker:   ~20MB (persistente)
```

- Projetado para Swoole **desde o início**
- Corrotinas em **toda stack**
- Overhead mínimo

---

### Comparativo visual

```
Requests/sec (mais = melhor):

Laravel FPM   : ████░░░░░░░░░░░░░░░░░░░░░░  ~500
Laravel Octane: ████████████░░░░░░░░░░░░░░░░  ~2.500
Hyperf        : █████████████████████████░░░  ~5.000+
```

---

### ⚠️ Cuidados com a

### ⚠️ programação Concorrente em PHP

---

### O problema do Singleton

```php
// ❌ PERIGO: estado compartilhado entre requests
class AuthService
{
    private ?User $currentUser = null;

    public function setUser(User $user): void
    {
        $this->currentUser = $user;
    }
}
```

_Request A define o user → Request B lê o user de A_ 😱

---

### Variáveis estáticas

```php
// ❌ PERIGO: persiste entre requests
class Cache
{
    private static array $data = [];
}

// ✅ CORRETO: usar Context
class Cache
{
    public function getData(): array
    {
        return Context::get('cache_data', []);
    }
}
```

---

### Connection Pool

```php
// ❌ PERIGO: criar conexão por request
$pdo = new PDO($dsn, $user, $pass);

// ✅ CORRETO: usar pool do Hyperf
// config/autoload/databases.php
return [
    'default' => [
        'driver'   => 'mysql',
        'host'     => 'localhost',
        'pool'     => [
            'min_connections' => 1,
            'max_connections' => 10,
        ],
    ],
];
```

---

### Defer e Cleanup

```php
// ✅ Garanta limpeza após a corrotina
Coroutine::create(function () {
    defer(function () {
        // cleanup: fechar recursos, limpar estado
        Context::destroy('temp_data');
    });

    // sua lógica aqui
    Context::set('temp_data', 'value');
});
```

---

### Checklist de Cuidados

- ⚠️ **Singleton**: nunca armazene estado do request
- ⚠️ **Static**: evite variáveis estáticas mutáveis
- ⚠️ **Conexões**: sempre use connection pool
- ⚠️ **Memory leak**: limpe referências circulares
- ✅ **Context**: use `Context` para dados por request
- ✅ **Defer**: use `defer()` para cleanup

---

### Resumo

- 🔄 Swoole traz **concorrência** ao PHP
- 🚀 Hyperf é o framework **nativo** para Swoole
- ⚡ Performance **5-10x** superior ao PHP-FPM
- ⚠️ Exige **mentalidade diferente** do desenvolvedor
- 🧠 Entenda o ciclo de vida **antes de codar**

---

### E você, o que acha?
## Obrigado
_`@eudiegoborgs`_
