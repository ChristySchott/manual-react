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

Inclua esta linha na parte de scripts do seu arquivo `package.json`:

```
{
  "scripts": {
    "test": "jest"
  }
}
```
então os testes podem ser executados rodando ` npm run test` ou `yarn test`

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

Agora crie um arquivo `math.test.js`, na mesma pasta, e usaremos o Jest para testar as funções definidas em `math.js`:

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

A execução de `npm run test` resulta no Jest sendo executado em todos os arquivos de teste encontrados e retornando o resultado final:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/vGSvRogM-QF8N3EP5j9vUYYrkWvRc89OhE98" alt="Teste" /> </h1>

### Executando o Jest com o VS Code

O Visual Studio Code é um ótimo editor de texto para desenvolver em JavaScript. A extensão [Jest](O Visual Studio Code é um ótimo editor para desenvolvimento de JavaScript. A extensão Jest oferece uma integração de alto nível para nossos testes.

Depois de instalá-lo, ele detectará automaticamente se você instalou o Jest em suas devDependencies e executará os testes. Você também pode chamar os testes manualmente, selecionando o comando `Jest: Start Runner`. Ele executará os testes e permanecerá no modo de exibição para executá-los novamente sempre que você alterar um dos arquivos que possuem um teste (ou um arquivo de teste):) oferece uma integração de alto nível para nossos testes.

Depois de instalá-lo, ele detectará automaticamente se você instalou o Jest em suas devDependencies e executará os testes. Você também pode chamar os testes manualmente, selecionando o comando Jest: Start Runner. Ele executará os testes e permanecerá no modo de exibição para executá-los novamente sempre que você alterar um dos arquivos que possuem um teste (ou um arquivo de teste):

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/WYyCsxacP34Fss8u9jT5lT0u3O--1Uwz9cKW" alt="Teste" /> </h1>

### Matchers

Nos exemplos anterior eu usei o `toBe()` como o único `matcher`:
```
test('Adding 1 + 1 equals 2', () => {
  expect(sum(1, 1)).toBe(2)
})
```

Um `matcher` é um método que permite testar valores.

Os `matchers` mais usados, comparando o valor do resultado de `expect()` com o valor passado como argumento, são:

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

Todos esses matchers podem ser negados usando `.not.` dentro da instrução, por exemplo:

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
<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/8j7LKC8uKE5Tw0X4WN4Gm0rD3NziyPxNwyCn" alt="example" /> </h1>
                                                                                                                            
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

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/F9HWCuZKWwG1RMZdNkDAaGMRsC0zaIsMokia" alt="example" /> </h1>

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
<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/7xWQMgM0PC9AGUBewAzcCgNWvHIjjxerfRxR" alt="example" /> </h1>

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

### Mock em um pacote inteiro

O Jest fornece uma maneira conveniente de dar um mock em um pacote inteiro. Crie uma pasta `__mocks__` na raiz do projeto e, nessa pasta, crie um arquivo JavaScript para cada um dos seus pacotes.

Digamos que você importe mathjs. Crie um arquivo `__mocks __/mathjs.js` na raiz do projeto e adicione este conteúdo:

```
module.exports = {
  log: jest.fn(() => 'test')
}
```

Isso vai dar um `mock` na função `log()` do pacote. Adicione quantas funções você desejar:
```
const mathjs = require('mathjs')

test(`The mathjs log function`, () => {
  const result = mathjs.log(10000, 10)
  expect(result).toBe('test')
  expect(mathjs.log).toHaveBeenCalled()
  expect(mathjs.log).toHaveBeenCalledWith(10000, 10)
})
```

### Mock em uma única função

Mais simples, você pode fazer isso usando `jest.fn()`:
```
const mathjs = require('mathjs')

mathjs.log = jest.fn(() => 'test')
test(`The mathjs log function`, () => {
  const result = mathjs.log(10000, 10)
  expect(result).toBe('test')
  expect(mathjs.log).toHaveBeenCalled()
  expect(mathjs.log).toHaveBeenCalledWith(10000, 10)
})
```

## Testing React Components

A maneira mais fácil de começar com o teste de componentes do React é fazer o teste de instantâneo, uma técnica de teste que permite testar componentes isoladamente.

Suponho que você criou um aplicativo React com o create-react-app, que já vem com o Jest instalado, o pacote de testes que precisamos.

Vamos começar com um teste simples. O CodeSandbox é um ótimo ambiente para experimentar isso. Comece com uma React sandbox, crie um componente `App.js` em uma pasta de componentes e adicione um arquivo `App.test.js`.

```
import React from 'react'

export default function App() {
  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
    </div>
  )
}
```

Nosso primeiro teste é bem simples:

```
test('First test', () => {
  expect(true).toBeTruthy()
})
```

Quando o CodeSandbox detecta arquivos de teste, ele os executa automaticamente e você pode clicar no botão Testes na parte inferior da exibição para mostrar os resultados do teste:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/DKFPyZSWF0O2ldKLAMyz7i0Di9NLqMs-ChQ4" alt="Test"/></h1>

Um arquivo de teste pode conter multiplos testes:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/iWZgjKzyxhyAtvjpsyTTEpzs4pKot938aVjk" alt="Test"/></h1>

Para realmente testar um componente React, vamos fazer algo um pouco mais útil agora. Por enquanto só temos o App, que não está fazendo nada muito útil. Primeiro, vamos configurar o ambiente com um pequeno aplicativo com mais funcionalidades: o aplicativo de contador que criamos anteriormente. Se você pulou, pode voltar e ler como a construímos, mas para uma referência mais fácil, adiciono-a aqui novamente.


São apenas dois componentes: `App` e `Button`. Crie o arquivo `App.js`:

```
import React, { useState } from 'react'
import Button from './Button'

const App = () => {
  const [count, setCount] = useState(0)
  
  const incrementCount = increment => {
    setCount(count + increment)
  }
  
  return (
    <div>
      <Button increment={1} onClickFunction={incrementCount} />
      <Button increment={10} onClickFunction={incrementCount} />
      <Button increment={100} onClickFunction={incrementCount} />
      <Button increment={1000} onClickFunction={incrementCount} />
      <span>{count}</span>
    </div>
  )
}

export default App
```
e o arquivo `Button`:

```
import React from 'react'

const Button = ({ increment, onClickFunction }) => {
  const handleClick = () => {
    onClickFunction(increment)
  }
  return <button onClick={handleClick}>+{increment}</button>
}

export default Button
```

Vamos usar a `react-testing-library`, que é uma grande ajuda, pois permite inspecionar a saída de cada componente e aplicar eventos a eles. Você pode ler mais sobre isso em https://github.com/kentcdodds/react-testing-library ou assistir a [este vídeo](https://www.youtube.com/watch?v=JKOwJUM4_RM).

Vamos testar o componente `Button` primeiro.

Começamos importando o `render` e o `fireEvent` da `react-testing-library`, dois `helpers`. O primeiro nos permite renderizar `JSX`. O segundo nos permite emitir eventos em um componente.

Crie um `Button.test.js` e coloque-o na mesma pasta que o `Button.js`.

```"
import React from 'react'
import { render, fireEvent } from 'react-testing-library'
import Button from './Button
```

Os Buttons são usados no aplicativo para aceitar um evento de clique e, em seguida, chamam uma função passada para a props onClickFunction. Adicionamos uma variável count e criamos uma função que a incrementa:

```
let count

const incrementCount = increment => {
  count += increment
}
```

Depois, clicamos no botão e verificamos que a contagem passou de 0 a 1:

```
test('+1 Button works', () => {
  count = 0
  const { container } = render(
    <Button increment={1} onClickFunction={incrementCount} />
  )
  const button = container.firstChild
  expect(button.textContent).toBe('+1')
  expect(count).toBe(0)
  fireEvent.click(button)
  expect(count).toBe(1)
})
```

Vamos testar o componente App agora, que mostra 4 botões e o resultado na página. Podemos inspecionar cada botão e ver se o resultado aumenta quando clicamos neles, clicando também várias vezes:

```
import React from 'react'
import { render, fireEvent } from 'react-testing-library'
import App from './App'

test('App works', () => {
  const { container } = render(<App />)
  console.log(container)
  const buttons = container.querySelectorAll('button')
  
  expect(buttons[0].textContent).toBe('+1')
  expect(buttons[1].textContent).toBe('+10')
  expect(buttons[2].textContent).toBe('+100')
  expect(buttons[3].textContent).toBe('+1000')
  
  const result = container.querySelector('span')
  expect(result.textContent).toBe('0')
  fireEvent.click(buttons[0])
  expect(result.textContent).toBe('1')
  fireEvent.click(buttons[1])
  expect(result.textContent).toBe('11')
  fireEvent.click(buttons[2])
  expect(result.textContent).toBe('111')
  fireEvent.click(buttons[3])
  expect(result.textContent).toBe('1111')
  fireEvent.click(buttons[2])
  expect(result.textContent).toBe('1211')
  fireEvent.click(buttons[1])
  expect(result.textContent).toBe('1221')
  fireEvent.click(buttons[0])
  expect(result.textContent).toBe('1222')
})
```
