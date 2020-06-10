<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 7:</strong> TESTES </h2>

## Jest

Jest é uma biblioteca para testar o código JavaScript.

É um projeto open source mantido pelo Facebook e é especialmente adequado para testar códigos no React, embora não se limite a isso: ele pode testar qualquer código JavaScript. Seus pontos fortes são:

- é rápido
- ele pode executar testes instantâneos (snapshot testing)
- é opinativo e fornece tudo pronto para uso, sem exigir que você faça escolhas

O Jest é uma ferramenta muito semelhante ao Mocha, embora eles tenham diferenças:

- Mocha é menos opinativo, enquanto Jest tem um certo conjunto de convenções
- O Mocha requer mais configuração, enquanto o Jest, por ser opinativo, geralmente funciona imediatamente
- O Mocha é mais antigo e estabelecido, com mais integrações de ferramentas

Na minha opinião, o maior recurso do Jest é ser uma solução pronta para uso que funciona sem ter que interagir com outras bibliotecas de teste.

### Instalação

O Jest é instalado automaticamente com o <kbg>create-react-app</kbg>. Portanto, se você usar isso, não precisará instalar o Jest.

O Jest pode ser instalado em qualquer outro projeto usando o Yarn:

```
yarn add --dev jest
```

ou o npm

```
npm install --save-dev jest
```

observe como instruímos ambos a colocar o Jest nas <kbg>devDependencies</kbg> do arquivo <kbg>package.json</kbg>, para que ele seja instalado apenas no ambiente de desenvolvimento e não na produção.

Inclua esta linha na parte de scripts do seu arquivo <kbg>package.json</kbg>:

```
{
  "scripts": {
    "test": "jest"
  }
}
```
então os testes podem ser executados rodando <kbg> npm run test</kbg> ou <kbg>yarn test</kbg>

### Criando o primeiro teste com o Jest

Projetos criados com create-react-app têm o Jest instalado e pré-configurado, mas adicionar o Jest a qualquer projeto é muito fácil, basta digitar:

```
yarn add --dev jest
```

Adicione essa linha ao seu arquivo <kbg>package.json</kbg>:
```
{
  "scripts": {
    "test": "jest"
  }
}
```

então os testes podem ser executados rodando <kbg> npm run test</kbg> ou <kbg>yarn test</kbg>.

Por enquanto você não tem nenhum teste, então nada será executado:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/QJ4lMCN6PhDyBBZ8mPyLmLciew9p9cUE9ug0" alt="Teste" /> </h1>

Vamos criar o primeiro teste. Abra um arquivo <kbg>math.js</kbg> e digite algumas funções que testaremos mais tarde:

```
const sum = (a, b) => a + b
const mul = (a, b) => a * b
const sub = (a, b) => a - b
const div = (a, b) => a / b

export default { sum, mul, sub, div }
```

Agora crie um arquivo <kbg>math.test.js</kbg>, na mesma pasta, e usaremos o Jest para testar as funções definidas em <kbg>math.js</kbg>:

```
const { sum, mul, sub, div } = require('./math')

test('Adding 1 + 1 equals 2', () => {
  expect(sum(1, 1)).toBe(2)
})
test('Multiplying 1 * 1 equals 1', () => {
  expect(mul(1, 1)).toBe(1)
})
test('Subtracting 1 - 1 equals 0', () => {
  expect(sub(1, 1)).toBe(0)
})
test('Dividing 1 / 1 equals 1', () => {
  expect(div(1, 1)).toBe(1)
})
```

A execução de <kbg>npm run test</kbg> resulta no Jest sendo executado em todos os arquivos de teste encontrados e retornando o resultado final:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/vGSvRogM-QF8N3EP5j9vUYYrkWvRc89OhE98" alt="Teste" /> </h1>

### Executando o Jest com o VS Code

O Visual Studio Code é um ótimo editor de texto para desenvolver em JavaScript. A extensão [Jest](O Visual Studio Code é um ótimo editor para desenvolvimento de JavaScript. A extensão Jest oferece uma integração de alto nível para nossos testes.

Depois de instalá-lo, ele detectará automaticamente se você instalou o Jest em suas devDependencies e executará os testes. Você também pode chamar os testes manualmente, selecionando o comando <kbg>Jest: Start Runner</kbg>. Ele executará os testes e permanecerá no modo de exibição para executá-los novamente sempre que você alterar um dos arquivos que possuem um teste (ou um arquivo de teste):) oferece uma integração de alto nível para nossos testes.

Depois de instalá-lo, ele detectará automaticamente se você instalou o Jest em suas devDependencies e executará os testes. Você também pode chamar os testes manualmente, selecionando o comando Jest: Start Runner. Ele executará os testes e permanecerá no modo de exibição para executá-los novamente sempre que você alterar um dos arquivos que possuem um teste (ou um arquivo de teste):

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/WYyCsxacP34Fss8u9jT5lT0u3O--1Uwz9cKW" alt="Teste" /> </h1>

### Matchers

Nos exemplos anterior eu usei o <kbg>toBe()</kbg> como o único <kbg>matcher</kbg>:
```
test('Adding 1 + 1 equals 2', () => {
  expect(sum(1, 1)).toBe(2)
})
```

Um <kbg>matcher</kbg> é um método que permite testar valores.

Os <kbg>matchers</kbg> mais usados, comparando o valor do resultado de <kbg>expect()</kbg> com o valor passado como argumento, são:

- <kbg>toBe</kbg> compara a igualdade estrita, usando ===
- <kbg>toEqual</kbg> compara os valores de duas variáveis. Se for um objeto ou matriz, verifica a igualdade de todas as propriedades ou elementos
- <kbg>toBeNull</kbg> é verdadeiro ao passar um valor nulo
- <kbg>toBeDefined</kbg> é verdadeiro ao passar um valor definido (oposto ao exemplo acima)
- <kbg>toBeUndefined</kbg> é verdadeiro ao transmitir um valor indefinido
- <kbg>toBeCloseTo</kbg> é usado para comparar valores float, evitando erros de arredondamento
- <kbg>toBeTruthy</kbg> é verdadeiro se o valor for considerado true (como um if faz)
- <kbg>toBeFalsy</kbg> é verdadeira se o valor for considerado false (como um if faz)
- <kbg>toBeGintenanceThan</kbg> é verdadeiro  se o resultado de expect() for maior que o argumento
- <kbg>toBeGintenanceThanOrEqual</kbg> é verdadeiro  se o resultado de expect () for igual ao argumento ou maior que o argumento
- <kbg>toBeLessThan</kbg> é verdadeiro Se o resultado de expect() for menor que o argumento
- <kbg>toBeLessThanOrEqual</kbg> é verdadeiro  se o resultado de expect() for igual ao argumento ou menor que o argumento
- <kbg>toMatch</kbg> é usado para comparar cadeias com correspondência de padrão de expressão regular
- <kbg>toContain</kbg> é usado em matrizes, true se a matriz esperada contiver o argumento em seu conjunto de elementos
- <kbg>toHaveLength</kbg>(number): verifica o comprimento de uma matriz
- <kbg>toHaveProperty</kbg>(chave, valor): verifica se um objeto tem uma propriedade e, opcionalmente, verifica seu valor
- <kbg>toThrow</kbg> verifica se uma função aprovada gera uma exceção (em geral) ou uma exceção específica
- <kbg>toBeInstanceOf()</kbg>: verifica se um objeto é uma instância de uma classe

Todos esses matchers podem ser negados usando <kbg>.not.</kbg> dentro da instrução, por exemplo:

```
test('Adding 1 + 1 does not equal 3', () => {
  expect(sum(1, 1)).not.toBe(3)
})
```

Para uso com promises, você pode usar `.resolve` e `.rejects`:

```
expect(Promise.resolve('lemon')).resolves.toBe('lemon')

expect(Promise.reject(new Error('octopus'))).rejects.toThrow('octopus')
```

### Setup

Antes de executar seus testes, você desejará executar alguma inicialização.

Para fazer algo uma vez antes de todos os testes serem executados, use a função `beforeAll()`:
```
beforeAll(() => {
  //faço algo
})
```

Para executar algo antes de cada teste, use `beforeEach()`:
```
beforeEach(() => {
  //faço algo
})
```

### Teardown

Assim como você pode fazer no setup, você também pode executar algo após a execução de cada teste:
```
afterEach (() => {
  //faça alguma coisa
})
```

e depois que todos os testes terminam:
```
afterAll (() => {
  //faça alguma coisa
})
```

### Agrupe testes usando o `describe()`:

Descrição ()
Você pode criar grupos de testes, em um único arquivo, que isolam as funções de setup e teardown:

```
describe('first set', () => {
  beforeEach(() => {
    //faça algo
  })
  afterAll(() => {
    //faça algo
  })
  test(/*...*/)
  test(/*...*/)
})

describe('second set', () => {
  beforeEach(() => {
    //faça algo
  })
  beforeAll(() => {
    //faça algo
  })
  test(/*...*/)
  test(/*...*/)
}) 
```

### Testando código assíncrono

O código assíncrono no JavaScript moderno pode ter basicamente duas formas: `callbacks` e `promises`. Além das `promises`, podemos usar `async/await`.

#### Callbacks

Você não pode fazer um teste em uma callback, porque o Jest não o executa - a execução do arquivo de teste termina antes que a callback seja executada. Para corrigir isso, basta passar um parâmetro para a função de teste, que você pode chamar de `done`. O Jest esperará até você executar o `done()` antes de terminar o teste:
```
//uppercase.js
function uppercase(str, callback) {
  callback(str.toUpperCase())
}
module.exports = uppercase

//uppercase.test.js
const uppercase = require('./src/uppercase')

test(`uppercase 'test' to equal 'TEST'`, (done) => {
  uppercase('test', (str) => {
    expect(str).toBe('TEST')
    done()
  }
})
```

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/wsyP30ZeaXYM6LTu4UOiTIg4cFjUOo4GtutV" alt="Example" /> </h1>

#### Promises

Com funções que retornam `promises`, simplesmente retornamos uma `promises` do teste:

```
//uppercase.js
const uppercase = str => {
  return new Promise((resolve, reject) => {
    if (!str) {
      reject('Empty string')
      return
    }
    resolve(str.toUpperCase())
  })
}
module.exports = uppercase

//uppercase.test.js
const uppercase = require('./uppercase')
test(`uppercase 'test' to equal 'TEST'`, () => {
  return uppercase('test').then(str => {
    expect(str).toBe('TEST')
  })
})
```
<h1 align="center> <img src="https://cdn-media-1.freecodecamp.org/images/8j7LKC8uKE5Tw0X4WN4Gm0rD3NziyPxNwyCn" alt="example" /> </h1>
                                                                                                                            
Promises que são rejeitadas podem ser testadas usando `catch()`:

```
//uppercase.js
const uppercase = str => {
  return new Promise((resolve, reject) => {
    if (!str) {
      reject('Empty string')
      return
    }
    resolve(str.toUpperCase())
  })
}

module.exports = uppercase

//uppercase.test.js
const uppercase = require('./uppercase')

test(`uppercase 'test' to equal 'TEST'`, () => {
  return uppercase('').catch(e => {
    expect(e).toMatch('Empty string')
  })
})
```

<h1 align="center> <img src="https://cdn-media-1.freecodecamp.org/images/F9HWCuZKWwG1RMZdNkDAaGMRsC0zaIsMokia" alt="example" /> </h1>

#### Async/Await

Para testar funções que retornam `promises` não também podemos usar `async/await`, o que torna a sintaxe mais direta e simples:
```
//uppercase.test.js
const uppercase = require('./uppercase')
test(`uppercase 'test' to equal 'TEST'`, async () => {
  const str = await uppercase('test')
  expect(str).toBe('TEST')
})
```
<h1 align="center> <img src="https://cdn-media-1.freecodecamp.org/images/7xWQMgM0PC9AGUBewAzcCgNWvHIjjxerfRxR" alt="example" /> </h1>

### Mocking

Nos testes, um `mocking` permite testar funcionalidades que dependem de:

- banco de dados
- solicitações de rede
- acesso a arquivos
- qualquer sistema externo

então:

- seus testes são executados mais rapidamente, proporcionando um tempo de resposta mais rápido durante o desenvolvimento
- seus testes são independentes das condições da rede ou do estado do banco de dados
- seus testes não poluem nenhum armazenamento de dados porque não tocam no banco de dados
- qualquer alteração feita em um teste não altera o estado dos testes subsequentes e a nova execução do conjunto de testes deve começar a partir de um ponto de partida conhecido e reproduzível
- você não precisa se preocupar com a limitação de taxa em chamadas de API e solicitações de rede

`Mocking` é útil quando você deseja evitar efeitos colaterais (por exemplo, gravar em um banco de dados) ou ignorar partes lentas do código (como acesso à rede), além disso, evita implicações na execução de seus testes várias vezes (por exemplo, imagine uma função que envie uma e-mail ou chama uma API com taxa de acesso limitada).

Ainda mais importante, se você estiver escrevendo um Teste de unidade, deve testar a funcionalidade de uma função isoladamente, não com toda a bagagem de coisas que ela abrange.

Usando `mockings`, você pode inspecionar se uma função do módulo foi chamada e quais parâmetros foram usados, com:

- `expect().toHaveBeenCalled()`: verifica se uma função "espionada" foi chamada
- `expect().toHaveBeenCalledTimes()`: conta quantas vezes uma função "espionada" foi chamada
- `expect().toHaveBeenCalledWith()`: checa se a função foi chamada com um número específico de parâmetros
- `expect().toHaveBeenLastCalledWith()`: checa os parâmetros da última função invocada

### Pacotes espiões (spy packages) sem afetar o código de funções

Ao importar um pacote, você pode dizer ao Jest para "espionar" a execução de uma função específica, usando `spyOn()`, sem afetar o funcionamento desse método.

Exemplo:

```
const mathjs = require('mathjs')

test(`The mathjs log function`, () => {
  const spy = jest.spyOn(mathjs, 'log')
  const result = mathjs.log(10000, 10)
  
  expect(mathjs.log).toHaveBeenCalled()
  expect(mathjs.log).toHaveBeenCalledWith(10000, 10)
})
```
