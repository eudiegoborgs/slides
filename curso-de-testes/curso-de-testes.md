---
marp: true
theme: eudiegoborgs
paginate: true
---

## oi, eu sou o Diego
<div style="position: absolute; top: 10vh; right: 0; width: 60vh; height: 60vh;">

![Diego Borges](./assets/diego.jpeg)

</div>

---

- mineiro, de `Belorizonti` **(oncovim)**
- pai do **Bryan**, do **Arthur** e da **Emily**
- esposo da **Stéfanny**
- **músico** de garagem
- **desenvolvedor** desde 2011
- tech manager coordenador de um **time incrível**
- e muitas outras coisas... 🍕🍰🍫🍖🌕🎸🚗🏍️🐶♾️

<div style="position: absolute; top: 10vh; right: 5vh; width: 300px;">

![Familia](./assets/familia.jpeg)

</div>
<div style="position: absolute; top: 50vh; right: 5vh; width: 300px;">

![equipe](./assets/equipe.jpeg)

</div>

---

# CURSO DE TESTES DE SOFTWARE

- **Parte 1**: Testes de Unidade
- **Parte 2**: Testes de Integração
- **Parte 3**: Continuous Integration (CI/CD)
- **Parte 4**: Testes de Contrato (Pact)
- **Parte 5**: Testes de Mutação
- **Parte 6**: Testes End to End com Cypress
- **Parte 7**: Testes de Carga e Estresse (Artillery)

---

# PARTE 1
## TESTES DE UNIDADE

---

# INTRODUÇÃO AOS
# TESTES DE UNIDADE

---

# O QUE É UM TESTE DE UNIDADE?

O teste de unidade é a fase do teste de software em que as classes e funções são testadas de maneira atômica, sem interferência de qualquer coisa externa a ela.

---

# PORQUE FAZER UM TESTE UNITÁRIO?

---

# Testes de unidade

Têm por objetivo isolar cada parte do sistema para garantir que elas estejam funcionando conforme especificado.

---

# NÃO SE PODE SIMPLESMENTE
# REFATORAR SEM TESTES

![bg right:50%](./assets/meme-boromir.png)

---

# COMO FUNCIONA UM TESTE DE UNIDADE?

---

# Exemplo de Teste de Unidade

```typescript
const addCharge = (value: number): number => {
⛔const databaseValue = await this.repo.getDatabaseValue({
    value: value
  })
⛔const apiValue await this.client.getClientValue(value)
✅return value + apiValue + databaseBalue
}
```

---

# Antecipando Mocks na Unidade

Um **Mock** na unidade é um substituto controlado para isolar a função testada das suas dependências externas.

---

# Exemplo de Teste Unitário (Jest)

```typescript
// Mockando dependências externas e validando chamadas
describe('addCharge', () => {
  it('deve mockar o banco e a API e validar as chamadas', async () => {
    const getDatabaseValue = jest.fn().mockResolvedValue(10);
    const getClientValue = jest.fn().mockResolvedValue(5);

    const context = {
      repo: { getDatabaseValue },
      client: { getClientValue },
      addCharge
    };

    const result = await context.addCharge(100);

    expect(getDatabaseValue).toHaveBeenCalledWith({ value: 100 });
    expect(getClientValue).toHaveBeenCalledWith(100);
    expect(result).toBe(115);
  });
});
```

---

# NÃO FAÇA MOCK DO QUE VOCÊ NÃO É DONO

### Código que VOCÊ POSSUI:
- Interfaces, modelos e regras do seu domínio.

### Código que VOCÊ NÃO POSSUI:
- SDKs de terceiros (AWS, Axios, Prisma, Stripe).

> **Regra de Ouro**: Crie abstrações (wrappers/interfaces suas) e faça mock apenas das suas abstrações no teste unitário!

---

# QUANDO USAR UM TESTE DE UNIDADE?

---

# QUEM FAZ UM TESTE DE UNIDADE?

---

# O PRINCÍPIO
# F.I.R.S.T

---

# FAST

Os testes devem ser rápidos o suficiente para que você não desanime de utilizá-los.

---

# INDEPENDENT

Os testes não devem depender do resultado ou do estado do teste anterior.

---

# REPEATABLE

Os testes devem poder ser reproduzidos repetidamente em ambientes diferentes sem variar seus resultados.

---

# SELF-VALIDATING

Os testes devem ser capazes de se auto-validar sem que seja necessária alguma interpretação.

---

# TIMELY

Os testes devem ser escritos antes do código que faz o teste passar.

---

# BIBLIOTECAS PARA TESTES

- **Jest**
- **Sinon.JS**
- **Mocha**
- **Chai**

---

# DE NOVO O JEST?

---

# TALK IS CHEAP,
# SHOW ME THE CODE...

---

# PARTE 2
## TESTES DE INTEGRAÇÃO

---

# INTRODUÇÃO AOS
# TESTES DE INTEGRAÇÃO

---

# O QUE É UM TESTE DE INTEGRAÇÃO?

O teste de integração é a fase do teste de software em que módulos são combinados e testados em grupo.

---

# Testes de Integração

Têm por objetivo encontrar falhas de integração entre as unidades, e não mais em testar as funcionalidades da mesma.

Nesta fase as categorias de testes aplicáveis são:
- Testes de interface
- Testes de dependências entre os componentes

---

# PORQUE FAZER UM TESTE DE INTEGRAÇÃO?

---

# COMO FUNCIONA UM TESTE DE INTEGRAÇÃO?

---

# QUANDO USAR UM TESTE DE INTEGRAÇÃO?

---

# QUEM FAZ UM TESTE DE INTEGRAÇÃO?

---

# O QUE É UM TEST DOUBLE?

Substitutos de componentes reais (dublês de teste).

---

# NEM TODO MOCK É UM MOCK!

- **Spy**
- **Mock**
- **Stub**

---

# STUB

### QUANDO USAR?
- Prover uma pré determinada resposta para quem chama
- Fazer uma pré determinada ação, como dar throw

### CASO DE USO:
Simular retornos de cotações financeiras ou forçar falhas registradas de conexão de rede sem disparar I/O real.

---

# STUB: Exemplo de Código (Jest)

```typescript
// Caso 1: Stub para retorno fixo de valor
const getDolarRateStub = jest.fn().mockResolvedValue(5.25);
const totalInBrl = await convertToBrl(100, getDolarRateStub); // 525

// Caso 2: Stub para simulação de falha (Throw)
const failingPaymentStub = jest.fn().mockRejectedValue(
  new Error('Gateway de Pagamento Indisponível')
);

await expect(checkout(failingPaymentStub)).rejects.toThrow('Gateway de Pagamento Indisponível');
```

---

# SPY

### QUANDO USAR?
- Verificar se foi chamado a quantidade de vezes esperada
- Verificar se foi chamado com os parâmetros esperados

### CASO DE USO:
Observar e gravar chamadas ao serviço de log/auditoria do sistema ao concluir um cadastro ou transação.

---

# SPY: Exemplo de Código (Jest)

```typescript
// Caso de Uso: Espionar a execução do serviço de log real
const loggerSpy = jest.spyOn(logger, 'info');

await userService.registerUser({ email: 'diego@email.com' });

// Validações do Spy
expect(loggerSpy).toHaveBeenCalledTimes(1);
expect(loggerSpy).toHaveBeenCalledWith('Usuário criado: diego@email.com');

loggerSpy.mockRestore(); // Restaura a função original
```

---

# MOCK

### QUANDO USAR?
- Evitar dependências externas à aplicação durante os testes
- Verificar se foi chamado a quantidade de vezes esperada
- Pré determina o retorno das funções
- Verificar se foi chamado com os parâmetros esperados

### CASO DE USO:
Substituir o serviço de e-mail por um dublê para testar o envio de confirmação de compra com os dados corretos.

---

# MOCK: Exemplo de Código (Jest)

```typescript
// Caso de Uso: Objeto Mock completo com expectativas de contrato
const emailServiceMock = {
  sendWelcomeEmail: jest.fn().mockResolvedValue({ status: 'SENT' })
};

const registerService = new RegisterService(emailServiceMock);
await registerService.execute({ email: 'diego@email.com' });

// Validação da expectativa do Mock
expect(emailServiceMock.sendWelcomeEmail).toHaveBeenCalledWith({
  to: 'diego@email.com',
  template: 'welcome-user'
});
```

---

# QUANDO NÃO USAR UM TEST DOUBLE?

---

# System Under Test (SUT)

Se a classe que você tá fazendo mock/spy é a mesma que você faz o assert.

---

# NÃO MOCK O QUE NÃO É SEU

https://github.com/testdouble/contributing-tests/wiki/Don't-mock-what-you-don't-own

---

# E OS MOCKS DE BANCO DE DADOS E API'S?

### Prós:
- Garantir que com determinada resposta nosso código vai realizar determinado fluxo
- Rapidez
- Sem internet

### Contras:
- Você pode não saber todos os possíveis comportamentos
- O teste não garante 100% a integração

---

# BIBLIOTECAS PARA TESTES DE INTEGRAÇÃO

- **Jest**
- **Sinon.JS**
- **Mocha**
- **Chai**

---

# O QUE É O JEST?

---

# JEST É UM PODEROSO FRAMEWORK DE TESTES EM JAVASCRIPT COM FOCO NA SIMPLICIDADE.

---

# Recursos do Jest

- **zero configuração**: Jest visa trabalhar fora da caixa, sem configuração, na maioria dos projetos JavaScript.
- **snapshots**: Faça testes que tenham objetos grandes com facilidade. Snapshots vivem ao lado de seus testes, ou embutidos.
- **isolado**: Os testes são paralelos e executados em seus próprios processos para maximizar o desempenho.
- **excelente api**: De `it` para `expect` - Jest tem todo o conjunto de ferramentas em um só lugar. Bem documentado e mantido.

---

# CARACTERÍSTICAS DO JEST (1/2)

- **Rápido e Seguro**: Executa testes paralelamente em processos isolados para máximo desempenho.
- **Cobertura de Código**: Gera relatórios nativos de cobertura sem depender de plugins externos.
- **Mock com Facilidade**: Sistema completo de Spies, Stubs e Mocks integrado à API.
- **Resultados Claros**: Exibe relatórios de falha legíveis com diffs visuais no terminal.

---

# CARACTERÍSTICAS DO JEST (2/2)

- **Linguagem Base é JavaScript**: Feito para o ecossistema JS/TS sem necessidade de novas linguagens.
- **Tudo em um Só Lugar**: Junta runner, asserções, mocks e snapshots em uma única ferramenta.
- **CI/CD Friendly**: Execução headless rápida com suporte nativo a pipelines de integração contínua.

---

# INSTALANDO O JEST

```bash
> npm install --save-dev jest supertest
```

---

# Configuração Básica

`// package.json`
```json
{
  "scripts": {
    "test": "jest"
  }
}
```

---

# Executando os Testes

```bash
> npm run test
```

---

# ESTRUTURA

Todo arquivo testável deve ser considerado com:
`*.spec.*` ou `*.test.*`

---

# CONFIGURAÇÃO ADICIONAL

```bash
> npx jest init
```

---

# USANDO TYPESCRIPT COM JEST (TS-JEST)

Instalação oficial recomendada para TypeScript + Jest com **validação real de tipos (`type-checking`)**:

```bash
> npm install --save-dev ts-jest @types/jest
> npx ts-jest config:init
```

> **Alternativa com Vitest**: Para novos projetos, o `vitest` executa TypeScript nativamente em altíssima velocidade sem necessitar de transpilers.

---

# MEU PRIMEIRO TESTE COM JEST

```javascript
test('dois mais dois é quatro', () => {
  expect(2 + 2).toBe(4);
});
// https://jestjs.io/pt-BR/docs/using-matchers
```

---

# PARTE 3
## CONTINUOUS INTEGRATION (CI/CD)

---

# INTRODUÇÃO À
# CONTINUOUS INTEGRATION (CI)

> Prática de desenvolvimento onde alterações de código são integradas frequentemente no repositório principal e validadas por uma suíte automatizada de testes.

---

# FERRAMENTAS DE CI/CD

- **GitHub Actions**: Integrado nativamente ao GitHub, baseado em workflows YAML.
- **GitLab CI/CD**: Integrado ao ecossistema GitLab com suporte avançado a pipelines.
- **CircleCI**: Foco em velocidade de execução e paralelismo de jobs.
- **Bitbucket Pipelines**: Integrado ao Jira e Bitbucket da Atlassian.

---

# POR QUE RODAR TESTES NO CI?

- **Quality Gate**: Bloqueia PRs automaticamente se algum teste quebrar.
- **Ambiente Neutro**: Roda em um container limpo (sem vício da máquina local).
- **Feedback Rápido**: Notifica o time sobre regressões antes do deploy.

---

# GITHUB ACTIONS: CHECAGEM DE LINT

`.github/workflows/lint.yml`
```yaml
name: CI - Lint

on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      - run: npm ci
      - run: npm run lint
```

---

# GITHUB ACTIONS: TESTES COM JEST

`.github/workflows/test.yml`
```yaml
name: CI - Testes

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      - run: npm ci
      - run: npm test
```

---

# GITHUB ACTIONS: STEPS NO MESMO JOB

Combinando Lint e Testes em steps sequenciais (mostrando apenas o que muda nos `steps`):

```yaml
    # ... mesmo setup inicial do job ...
    steps:
      - ...
      - run: npm ci
      - run: npm run lint  # Step 1: Checagem de Lint
      - run: npm test      # Step 2: Suíte de Testes
```

---

# GITHUB ACTIONS: JOBS DIFERENTES

Rodando Lint e Testes em jobs paralelos separados (mostrando a estrutura dos `jobs:`):

```yaml
jobs:
  lint:
    # ... mesmo setup do runner/node ...
    steps:
      - ...
      - run: npm run lint

  test:
    # needs: lint  <-- Opcional: só roda após o lint passar
    steps:
      - ...
      - run: npm test
```

---

# MESMO JOB VS JOBS DIFERENTES

- **Mesmo Job (Steps Sequenciais)**:
  - *Quando usar*: Projetos menores e pipelines enxutos.
  - *Vantagens*: Reaproveita o contexto; não repete o setup (`checkout`/`npm ci`), economizando minutos do CI.

- **Jobs Diferentes (Paralelismo)**:
  - *Quando usar*: Suítes grandes, monorepos ou projetos de média/alta complexidade.
  - *Vantagens*: Execução simultânea em múltiplos runners (menor tempo total de PR) e controle flexível com `needs`.

---

# TALK IS CHEAP,
# SHOW ME THE CODE...

---

# PARTE 4
## TESTES DE CONTRATO (PACT)

---

# O QUE É UM TESTE DE CONTRATO?

> Valida a comunicação e o contrato de API entre dois sistemas (**Consumidor** e **Provedor**) sem precisar subir ambas as aplicações juntas em um ambiente de testes integrado.

- Garante que mudanças no Provedor (Backend) não quebrem as expectativas do Consumidor (Frontend / Microserviço).
- Evita quebras acidentais de API (*breaking changes*) em produção.

---

# CONSUMER-DRIVEN CONTRACT TESTING (CDC)

No padrão **CDC**, quem dita as regras é o **Consumidor**:

1. **Consumidor**: Escreve o teste declarando suas expectativas (rotas, parâmetros e respostas esperadas).
2. **Contrato (Pact)**: O arquivo `.json` de contrato é gerado automaticamente.
3. **Provedor**: Executa a verificação contra o contrato gerado para garantir conformidade.

---

# FERRAMENTAS DE TESTE DE CONTRATO

- **Pact**: Padrão de mercado para CDC (suporte a JS/TS, Java, Go, Python, C#, PHP).
- **Pact Broker**: Servidor central para compartilhar, versionar e validar contratos entre times.
- **Spring Cloud Contract**: Alternativa focada no ecossistema Java / Spring.

---

# EXEMPLO COM PACT: CONSUMIDOR (1/2)

```typescript
// consumer.spec.ts (Definindo expectativas no Consumidor)
import { PactV3, MatchersV3 } from '@pact-foundation/pact';

const provider = new PactV3({ consumer: 'Frontend', provider: 'UserService' });

describe('Contrato com UserService', () => {
  it('deve retornar dados do usuário', async () => {
    provider
      .given('Usuário 123 existe')
      .uponReceiving('GET /users/123')
      .withRequest({ method: 'GET', path: '/users/123' })
      .willRespondWith({
        status: 200,
        body: { id: MatchersV3.like('123'), name: MatchersV3.like('Diego') }
      });
  });
});
```

---

# EXEMPLO COM PACT: PROVEDOR (2/2)

```typescript
// provider.spec.ts (Validação no Backend / Provedor)
import { Verifier } from '@pact-foundation/pact';

describe('Validação do Provedor', () => {
  it('deve validar todos os contratos no Pact Broker', () => {
    return new Verifier({
      providerBaseUrl: 'http://localhost:3000',
      pactBrokerUrl: 'https://nosso-pact-broker.com',
      pactBrokerToken: process.env.PACT_BROKER_TOKEN
    }).verifyProvider();
  });
});
```

---

# BENEFÍCIOS DOS TESTES DE CONTRATO

- **Desacoplamento de Ambientes**: Teste o consumidor e provedor de forma 100% independente no CI/CD.
- **Feedback Rápido**: Detecte quebras de contrato em segundos no Pull Request.
- **Documentação Viva**: O Pact Broker mantém um mapa sempre atualizado das integrações entre serviços.

---

# PARTE 5
## TESTES DE MUTAÇÃO

---

# Testes de mutação
## Como garantir a qualidade da minha cobertura?

---

# Cobertura de código

```text
File                                    | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
----------------------------------------|---------|----------|---------|---------|-------------------
All files                               |   54.17 |       50 |   43.24 |    55.4 |
 src/domain/services/book.service.ts    |     100 |      100 |     100 |     100 |
 src/domain/services/user.service.ts    |     100 |      100 |     100 |     100 |
 src/infrastructure/entrypoint/api.ts   |   96.43 |      100 |     100 |    96.3 | 13
```

---

> "Já tenho 100% de cobertura… Agora não preciso mais me preocupar porque meu código está completamente protegido de mudanças."

---

# Será???

---

# Exemplo de Cobertura Vazia

```javascript
const isAdult = age => {
  return age >= 18
}

it('Test isAdult function', () => {
  expect(isAdult(27)).toBe(true)
  expect(isAdult(10)).toBe(false)
})
```

---

# Essa função está completamente protegida de mudanças???

---

# Mutante 1 (Regra Alterada)

```javascript
const isAdult = age => {
  return age >= 12 // ⚠️ Mutante!
}

it('Test isAdult function', () => {
  expect(isAdult(27)).toBe(true)  // Passa!
  expect(isAdult(10)).toBe(false) // Passa!
})
```

---

# Mutante 2 (Regra Alterada)

```javascript
const isAdult = age => {
  return age >= 21 // ⚠️ Mutante!
}

it('Test isAdult function', () => {
  expect(isAdult(27)).toBe(true)  // Passa!
  expect(isAdult(10)).toBe(false) // Passa!
})
```

---

# Quem guardará os guardas?

---

# E os mutantes surgem para salvar o dia 🦸

---

# Como assim?

Cada ciclo de um teste de mutação que é executado, cria uma variante do nosso código e executa a suíte de testes.

---

# Variantes de Código

As variantes do código não podem passar no nosso teste. Se elas passarem, significa que sua cobertura não está protegendo seu código de mudanças.

---

# Problemas do teste de mutação

1. **É lento**
2. **É caro**
3. **É muito difícil de ser implementado sem a ajuda de bibliotecas**

---

# O Stryker

https://stryker-mutator.io/

`node version min 18+`

---

# Instalando o Stryker

```bash
> npm i --save-dev @stryker-mutator/core @stryker-mutator/jest-runner
```

---

# Inicializando o Stryker

```bash
> npx stryker init
```

---

# Configuração (`stryker.conf.json`)

```json
{
  "$schema": "./node_modules/@stryker-mutator/core/schema/stryker-schema.json",
  "packageManager": "npm",
  "reporters": [
    "html",
    "clear-text",
    "progress"
  ],
  "testRunner": "jest",
  "coverageAnalysis": "perTest"
}
```

---

# Executando o Stryker

```bash
> npx stryker run
```

---

# Hands on...

---

# PARTE 6
## TESTES END TO END COM CYPRESS

---

# USANDO
# CYPRESS
### PARA TESTES END TO END

---

# O QUE É UM TESTE END TO END?

---

# PORQUE FAZER UM TESTE END TO END?

---

# COMO FUNCIONA UM TESTE END TO END?

---

# QUANDO USAR UM TESTE END TO END?

---

# QUEM FAZ UM TESTE END TO END?

---

# O QUE É BDD?

---

# BDD - Cenário 1

### Cenário 1: Cliente com dados corretos
- **Dado que** senhor Joaquim deseja abrir uma conta
- **E** informou “CPF”
- **E** informou “RG”
- **E** informou “seu endereço”
- **Quando** entrar com essas informações no cadastro
- **Então** uma nova conta deve ser criada

---

# BDD - Cenário 2

### Cenário 2: Cliente já cadastrado
- **Dado que** senhor Joaquim deseja abrir uma conta
- **E** informou “CPF” já existente na base de cliente
- **E** informou “RG”
- **E** informou “seu endereço”
- **Quando** entrar com essas informações no cadastro
- **Então** não será possível abrir uma nova conta

---

# BIBLIOTECAS PARA TESTES END TO END

- **cypress.io**
- **pact**
- **appium**
- **capybara**
- **selenium**

---

# O QUE É O CYPRESS?

---

# O CYPRESS UNE TUDO O QUE É NECESSÁRIO PARA FAZER TESTES END TO END NA SUA APLICAÇÃO WEB.

---

# Antes do Cypress vs Com Cypress

### Antes do Cypress:
- Escolha um quadro (Mocha, Jasmine, QUnit, Karma)
- Escolha uma biblioteca de asserções (Chai, Expect.js)
- Instalar Selênio & invólucro (Webdriver, Nightwatch, Protractor)
- Adicionar bibliotecas adicionais (Sinon, TestDouble)

### Com Cypress:
- Quadro de testes tudo em um, biblioteca de asserções, com mocking e stub, **tudo sem selênio**.

---

# CARACTERÍSTICAS DO CYPRESS (1/2)

- **Sem Selenium**: Executa nativamente no navegador, dispensando WebDrivers lentos.
- **Foco em End-to-End**: Criado especificamente para simular a jornada completa do usuário real.
- **Compatível com Web Moderna**: Suporte total a React, Vue, Angular e aplicações SPA/SSR.
- **Linguagem Base é JavaScript/TypeScript**: Escreva testes na mesma linguagem da aplicação.

---

# CARACTERÍSTICAS DO CYPRESS (2/2)

- **Tudo em um Só Lugar**: Runner visual, asserções, spies e stubs integrados na ferramenta.
- **Rápido com Auto-Waiting**: Aguarda automaticamente elementos DOM sem sleeps manuais.
- **CI/CD Friendly**: Modo headless otimizado para pipelines no GitHub Actions e Docker.

---

# INSTALANDO O CYPRESS

```bash
> npm install cypress --save-dev
```

---

# Executando o Cypress

```bash
> npx cypress open
```

---

# Rodando no Terminal (CI)

```bash
> npx cypress run
```

---

# ESTRUTURA (CYPRESS V10+)

```text
[./cypress]
  [./e2e] Especificações e casos de testes E2E (*.cy.ts).
  [./fixtures] Arquivos de dados estáticos e mocks.
  [./support] Comandos customizados e setup (e2e.ts).
[./cypress.config.js] Arquivo central de configuração.
[./package.json] Controle de dependências do projeto.
```

---

# SELETORES E PRIORIDADES

1. **data-cy** (Recomendado)
2. **data-test**
3. **data-testid**
4. **id**
5. **class**
6. **tag**
7. **attributes**
8. **nth-child**

---

# PRIMEIRO TESTE COM CYPRESS

```typescript
// cypress/e2e/cadastro.cy.ts
describe('Fluxo de Cadastro de Cliente', () => {
  it('deve cadastrar um novo cliente com sucesso', () => {
    cy.visit('/cadastro');

    cy.get('[data-cy="input-nome"]').type('Joaquim Silva');
    cy.get('[data-cy="input-cpf"]').type('123.456.789-00');
    cy.get('[data-cy="btn-submeter"]').click();

    cy.get('[data-cy="mensagem-sucesso"]')
      .should('contain', 'Conta criada com sucesso');
  });
});
```

---

# MOCKANDO RESPOSTAS DE API (CY.INTERCEPT)

```typescript
// Interceptação e Mock de API HTTP no Cypress
describe('Fluxo com Mock de API', () => {
  it('deve exibir mensagem de erro se o cliente já for cadastrado', () => {
    cy.intercept('POST', '/api/clientes', {
      statusCode: 400,
      body: { error: 'Cliente já cadastrado na base' }
    }).as('postCliente');

    cy.visit('/cadastro');
    cy.get('[data-cy="input-cpf"]').type('123.456.789-00');
    cy.get('[data-cy="btn-submeter"]').click();

    cy.wait('@postCliente');
    cy.get('[data-cy="mensagem-erro"]')
      .should('contain', 'Não foi possível abrir uma nova conta');
  });
});
```

---

# CONFIGURAÇÕES E VARIÁVEIS DE AMBIENTE

---

# CONTINUOUS INTEGRATION (CYPRESS)

`.github/workflows/e2e.yml`
```yaml
name: E2E - Cypress Tests

on: [push, pull_request]

jobs:
  cypress-run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: cypress-io/github-action@v6
        with:
          build: npm run build
          start: npm start
          wait-on: 'http://localhost:3000'
```

---

# PARTE 7
## TESTES DE CARGA E ESTRESSE

---

# O QUE SÃO TESTES DE CARGA E ESTRESSE?

- **Teste de Carga (Load Test)**: Avalia o comportamento do sistema sob volumes normais e picos esperados de usuários simultâneos (VUs).
- **Teste de Estresse (Stress Test)**: Submete a aplicação além dos seus limites normais até encontrar o ponto de ruptura (*breaking point*).

---

# POR QUE REALIZAR TESTES DE CARGA?

- **Identificar Gargalos**: CPU, memória, concorrência no banco e esgotamento do *connection pool*.
- **Validar Autoscaling**: Garantir que novos contêineres/instâncias sobem antes que o serviço caia.
- **Prevenir Outages**: Evitar indisponibilidades em eventos de alto tráfego (ex: Black Friday, lançamentos).

---

# FERRAMENTAS POPULARES

- **Artillery**: Ferramenta moderna baseada em Node.js com cenários declarativos em YAML.
- **k6**: Baseado em JavaScript/Go orientado a scripts.
- **JMeter**: Tradicional, baseado em Java e interface gráfica XML.
- **Locust**: Baseado em Python com scripts orientados a código.

---

# ARTILLERY: CONFIGURAÇÃO DE CARGA (1/2)

`load-test.yml` (Fases de tráfego e regras de SLA):

```yaml
config:
  target: "https://api.minhaaplicacao.com"
  phases:
    - duration: 30
      arrivalRate: 5
      rampTo: 50
      name: "Ramp-up de Carga"
    - duration: 60
      arrivalRate: 50
      name: "Carga Sustentada"
  ensure:
    p95: 500
    maxErrorRate: 1
```

---

# ARTILLERY: CENÁRIOS E FLUXO (2/2)

`load-test.yml` (Fluxo de execução e validação de HTTP):

```yaml
scenarios:
  - name: "Buscar Produtos"
    flow:
      - get:
          url: "/produtos"
          expect:
            - statusCode: 200
```

---

# MÉTRICAS-CHAVE A MONITORAR

- **RPS (Requests Per Second)**: Taxa total de vazão de requisições por segundo.
- **Latência p95 / p99**: Tempo de resposta garantido para 95% e 99% dos usuários.
- **Taxa de Erro**: Frequência de respostas 5xx ou timeouts.
- **Recursos de Infra**: Uso de CPU, memória, IOPS de disco e conexões ativas do banco.

---

# TALK IS CHEAP,
# SHOW ME THE CODE...

---

# OBRIGADO!
### PODEM PERGUNTAR :)

ferreirabdiego@gmail.com - @eudiegoborgs
