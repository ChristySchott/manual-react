<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h3 align="center"> O Manual do React segue a regra 80/20: aprenda 80% do tópico em 20% do tempo. </h3>

### Book Index

<strong>SEÇÃO 1:</strong> PRINCIPAIS CONCEITOS DO JAVASCRIPT MODERNO QUE VOCÊ PRECISA SABER PARA USAR O REACT

- Variables
- Arrow functions
- Operador rest e spread
- Objetos e desestruturação de arrays (arrays destructuring)
- Template literals
- Classes
- Callbacks
- Promises
- Async/Await
- ES Modules

<strong>SEÇÃO 2:</strong> CONCEITOS DO REACT

- Single Page Applications
- Declarativo
- Imutabilidade
- Pureza
- Composição
- Virtual DOM
- Fluxo de dados unidirecional

<strong>SEÇÃO 3:</strong> PROFUNDO NO REACT

- JSX
- Componentes
- State (estado)
- Props
- Componentes de apresentação versus contêiner
- State vs props
- PropTypes
- React Fragment
- Eventos
- Lifecycle Events (ciclo de vida dos eventos)
- Formulários no React
- Referenciando um elemento da DOM
- Renderização no lado do servidor (Server side rendering)
- Context API
- Componentes de ordem superior (Higher order components)
- Renderizando as Props
- Hooks
- Divisão de código

<strong>SEÇÃO 4:</strong> EXEMPLOS PRÁTICOS

- Construindo um contador simples
- Buscar e exibir informações de usuários do GitHub via API

<strong>SEÇÃO 5:</strong> ESTILIZANDO

- CSS no React
- SASS no React
- Styled Components

<strong>SEÇÃO 6:</strong> FERRAMENTAS

- Babel
- Webpack

<strong>SEÇÃO 7:</strong> TESTES

- Jest
- Testando componentes do React

<strong>SEÇÃO 8:</strong> O ECOSSISTEMA DO REACT

- React Router
- Redux
- Next.js
- Gatsby

- Empacotando

<h2 align="center"><strong>SEÇÃO 1:</strong> PRINCIPAIS CONCEITOS DO JAVASCRIPT MODERNO QUE VOCÊ PRECISA SABER PARA USAR O REACT</h2>

<h3>Descubra se você precisa aprender alguma coisa antes de se aprofundar no React.</h3>


Se você deseja aprender React, primeiro precisa de algumas coisas na bagagem.

Existem algumas tecnologias de pré-requisito com as quais você precisa se familiarizar, principalmente relacionadas a alguns dos recursos mais recentes do JavaScript que você usará repetidamente no React.

Às vezes, as pessoas pensam que um recurso específico é fornecido pelo React, mas, em vez disso, é apenas a sintaxe moderna do JavaScript.

Não há nenhum ponto em ser especialista nesses tópicos imediatamente, mas quanto mais você se aprofunda no React, mais precisará dominá-los.

Vou mencionar uma lista de coisas para você se atualizar rapidamente.

## Variáveis
           
Uma variável é um literal atribuído a um identificador, para que você possa fazer referência e usá-la posteriormente no programa.

Variáveis em JavaScript não têm nenhum tipo anexado. Depois de atribuir um tipo literal específico a uma variável, você poderá posteriormente reatribuir a variável para hospedar qualquer outro tipo, sem erros de tipagem ou qualquer problema.

É por isso que o JavaScript às vezes é chamado de "fracamente tipada".

Uma variável deve ser declarada antes que você possa usá-la. Existem três maneiras de fazer isso, usando var, let ou const, e essas três maneiras diferem em como você pode interagir com a variável posteriormente.

### Using <kbg>var</kbg>

Até o ES2015, var era o único construto disponível para definir variáveis.
```
var a = 0;
```

Se você esquecer de adicionar var, atribuirá um valor a uma variável não declarada, e os resultados poderão variar.

Em ambientes modernos, com o modo estrito ativado, você receberá um erro. Em ambientes mais antigos (ou com o modo estrito desativado), isso simplesmente inicializa a variável e a atribui ao objeto global.

Se você não inicializar a variável quando a declarar, ela terá o valor <kbg>undefined</kbg> até você atribuir um valor a ela.

```
var a //typeof a === 'undefined'
```

Você pode redeclarar a variável várias vezes, substituindo-a:

```
var a = 1
var a = 2
```

O escopo é a parte do código em que a variável é visível.

Uma variável inicializada com var fora de qualquer função é atribuída ao objeto global, possui um escopo global e é visível em qualquer lugar. Uma variável inicializada com var dentro de uma função é atribuída a essa função, é local e é visível apenas dentro dela, como um parâmetro de função.

Qualquer variável definida em uma função com o mesmo nome que uma variável global tem precedência sobre a variável global, sombreando-a

É importante entender que um bloco (identificado por um par de chaves) não define um novo escopo. Um novo escopo é criado apenas quando uma função é criada, porque var não possui escopo de bloco, mas escopo de função.

Dentro de uma função, qual
quer variável definida nele é visível em todo o código da função, mesmo que a variável seja declarada no final da função, ela ainda pode ser referenciada no início, porque o JavaScript antes de executar o código realmente move todas as variáveis no topo (algo que é chamado de içamento). Para evitar confusão, sempre declare variáveis no início de uma função.

### Using <kbg>let</kbg>

let é um novo recurso introduzido no ES2015 e é essencialmente uma versão do var com escopo em bloco. Seu escopo é limitado ao bloco, instrução ou expressão onde é definido, e todos os blocos internos contidos.

Os desenvolvedores modernos de JavaScript podem optar por usar apenas let e descartar completamente o uso de var.

Definindo let fora de qualquer função - ao contrário de var - não cria-se uma variável global.

### Using <kbg>const</kbg>

As variáveis declaradas com var ou let podem ser alteradas posteriormente no programa e reatribuídas. Depois que uma const é inicializada, seu valor nunca pode ser alterado novamente e não pode ser reatribuído para um valor diferente.

```
const a = 'test'
```

const não fornece imutabilidade, apenas garante que a referência não possa ser alterada.

const tem escopo de bloco, o mesmo que let.

Os desenvolvedores modernos de JavaScript podem optar por sempre usar const para variáveis que não precisam ser reatribuídas posteriormente no programa.

Por quê? Porque sempre devemos usar a construção mais simples disponível para evitar erros no caminho.

## Arrow Functions

Arrow Functions foram introduzidas no ES6 / ECMAScript 2015 e, desde a sua introdução, mudaram para sempre a aparência (e o funcionamento) do código JavaScript.

Na minha opinião, essa alteração foi tão acolhedora que agora você raramente vê o uso da palavra-chave function nas bases de código modernas.

Visualmente, é uma alteração simples e bem-vinda, que permite escrever funções com uma sintaxe mais curta, de:

```
const myFunction = function() {
  //...
}
```

para

```
const myFunction = () => {
  //...
}
```
Se o corpo da função contiver apenas uma única instrução, você poderá omitir os colchetes e escrever tudo em uma única linha:
```
const myFunction = () => doSomething()
```

### Retorno implícito

AS Arrow Functions permitem um retorno implícito: os valores são retornados sem a necessidade de usar a palavra-chave return.

Funciona quando há uma instrução de uma linha no corpo da função:

```
const myFunction = () => 'teste'

myFunction() //'teste'
```

Outro exemplo, ao retornar um objeto, lembre-se de colocar os colchetes entre parênteses para evitar que sejam considerados os colchetes da função de quebra:

```
const myFunction = () => ({ value: 'test' })

myFunction() //{value: 'test'}
```

## Operador Rest e spread

Você pode expandir uma matriz, um objeto ou uma string usando o operador spread ....

Vamos começar com um exemplo de matriz. Dado
```
const a = [1, 2, 3]
```

você pode criar um novo array usando
```
const b = [...a, 4, 5, 6]
```

você também pode criar uma cópia do array
```
You can also create a copy of an array using
```

Usando strings o operador rest cria um array com cada caracter da string 
```
const hey = 'hey'
const arrayized = [...hey] // ['h', 'e', 'y']
```
The rest element is useful when working with array destructuring:
O rest é util quando trabalha-se com desestruturação de um array (array destruct
```
const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
```
e o spread:
```
const numbers = [1, 2, 3, 4, 5]
const sum = (a, b, c, d, e) => a + b + c + d + e
const sumOfNumbers = sum(...numbers)
```
## Objetos e desestruturação de arrays (arrays destructuring)

Dado um objeto, usando a sintaxe de desestruturação, você pode extrair apenas alguns valores e colocá-los em variáveis nomeadas:

```
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54 //made up
}

const { firstName: name, age } = person //name: Tom, age: 54
```

name e age contem os valores designados.

A sintaxe também funciona em arrays:

```
const a = [1, 2, 3, 4, 5]
const [first, second] = a
```

## Template Literals

Os template literals são um novo recurso do ES2015 / ES6 que permite trabalhar com seqüências de caracteres de uma maneira nova em comparação ao ES5 e abaixo.

A sintaxe à primeira vista é muito simples, basta usar backticks em vez de aspas simples ou duplas:
```
const a_string = `something`
```

Eles são únicos porque fornecem muitos recursos que Strings normais construídas com aspas não fornecem, em particular:

- eles oferecem uma ótima sintaxe para definir cadeias de caracteres multilinhas
- eles fornecem uma maneira fácil de interpolar variáveis e expressões em strings
- eles permitem que você crie DSLs com tags de modelo (DSL significa linguagem específica do domínio e é usada, por exemplo, em  React by Styled Components, para definir CSS para um componente)

## Classes 


Em 2015, o padrão ECMAScript 6 (ES6) introduziu classes.

O JavaScript tem uma maneira bastante incomum de implementar herança: herança prototípica. A herança prototípica, embora seja ótima na minha opinião, é diferente da maioria das implementações de herança de outras linguagens de programação populares, que são baseadas em classes.

Pessoas provenientes de Java ou Python ou outras linguagens tiveram dificuldade em entender os meandros da herança prototípica; portanto, o comitê do ECMAScript decidiu borrifar o Syntactic Sugar sobre a herança prototípica, para que se assemelhe ao modo como a herança baseada em classe funciona em outras implementações populares.

Isso é importante: o JavaScript ainda é o mesmo e você pode acessar um protótipo de objeto da maneira usual.

### A definição de uma classes

É assim que uma classe se parece: 
```
class Person {
  constructor(name) {
    this.name = name
  }
  
  hello() {
    return 'Hello, I am ' + this.name + '.'
  }
}
```
Uma classe possui um identificador, que podemos usar para criar novos objetos usando o novo ClassIdentifier ().

Quando o objeto é inicializado, o método construtor é chamado, com todos os parâmetros passados.

Uma classe também possui quantos métodos forem necessários. Nesse caso, o hello é um método e pode ser chamado em todos os objetos derivados dessa classe:

```
const flavio = new Person('Flavio')
flavio.hello()
```

### Herança de classes

Uma classe pode estender outra classe e os objetos inicializados usando essa classe herdam todos os métodos de ambas as classes.

Se a classe herdada tiver um método com o mesmo nome de uma das classes mais altas na hierarquia, o método mais próximo terá precedência:

```
class Programmer extends Person {
  hello() {
    return super.hello() + ' I am a programmer.'
  }
}

const flavio = new Programmer('Flavio')
flavio.hello()
```

o programa acima devolve “Hello, I am Flavio. I am a programmer.”

As classes não possuem declarações explícitas de variáveis de classe, mas você deve inicializar qualquer variável no construtor.

Dentro de uma classe, você pode fazer referência à classe pai chamando super ().

### Getters and setters

Você pode adicionar métodos prefixados com get ou set para criar um getter e setter, que são duas partes diferentes de código que são executadas com base no que você está fazendo: acessando a variável ou modificando seu valor.

```
class Person {
  constructor(name) {
    this.name = name
  }
  
  set name(value) {
    this.name = value
  }
  
  get name() {
    return this.name
  }
}
```

## Callbacks

Os computadores são assíncronos por design.

Assíncrono significa que as coisas podem acontecer independentemente do fluxo do programa principal.

Nos computadores consumidores atuais, todo programa é executado por um intervalo de tempo específico e, em seguida, interrompe sua execução para permitir que outro programa continue sua execução. Essa coisa roda em um ciclo tão rápido que é impossível perceber, e achamos que nossos computadores executam muitos programas simultaneamente, mas isso é uma ilusão (exceto em máquinas com multiprocessadores).

Os programas usam internamente interrupções, um sinal emitido para o processador para ganhar a atenção do sistema.

Não vou falar sobre isso, mas lembre-se de que é normal que os programas sejam assíncronos e interrompam sua execução até que precisem de atenção, e o computador pode executar outras coisas nesse meio tempo. Quando um programa está aguardando uma resposta da rede, ele não pode parar o processador até que a solicitação seja concluída.

Normalmente, as linguagens de programação são síncronas e algumas fornecem uma maneira de gerenciar a assincronicidade, na linguagem ou através de bibliotecas. C, Java, C #, PHP, Go, Ruby, Swift, Python, são todos síncronos por padrão. Alguns deles lidam com async usando threads, gerando um novo processo.

O JavaScript é síncrono por padrão e é de thread único. Isso significa que o código não pode criar novos threads e executar em paralelo.

Linhas de código são executadas em série, uma após a outra, por exemplo:
```
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```
Mas o JavaScript nasceu dentro do navegador, e sua principal tarefa, no início, era responder a ações do usuário, como onClick, onMouseOver, onChange, onSubmit e assim por diante. Como isso poderia ser feito com um modelo de programação síncrona?

A resposta estava em seu ambiente. O navegador fornece uma maneira de fazer isso, fornecendo um conjunto de APIs que podem lidar com esse tipo de funcionalidade.

Mais recentemente, o Node.js introduziu um ambiente de E / S sem bloqueio para estender esse conceito ao acesso a arquivos, chamadas de rede e assim por diante.

Você não sabe quando um usuário clicará em um botão; portanto, o que você faz é definir um manipulador de eventos para o evento click. Este manipulador de eventos aceita uma função, que será chamada quando o evento for disparado:

```
document.getElementById ('button'). addEventListener ('click', () => {
  // item clicado
})

```
Esta é o callback.

Uma callback é uma função simples que é passada como um valor para outra função e só será executada quando o evento acontecer. Podemos fazer isso porque o JavaScript possui funções de primeira classe, que podem ser atribuídas a variáveis e transmitidas para outras funções (chamadas funções de ordem superior)

É comum agrupar todo o seu código de cliente em um eventListener de carregamento no windowobject, que executa a callback somente quando a página estiver pronta:

```
window.addEventListener ('load', () => {
  // janela carregada
  //faça o que você quiser
})

```

Callbacks são usadas em todo o lugar, não apenas em eventos da DOM.

Um exemplo comum é usando os temporizadores:
```
setTimeout(() => {
  // runs after 2 seconds
}, 2000)
```

### Tratamento de erros em callbacks

Como você lida com erros em callbacks? Uma estratégia muito comum é usar o que o Node.js adotou: o primeiro parâmetro em qualquer callback é o objeto de erro.

Se não houver erro, o objeto é <kbg>null</kbg>. Se houver um erro, ele conterá uma descrição do erro e outras informações
```
fs.readFile('/file.json', (err, data) => {
  if (err !== null) {
    //handle error
    console.log(err)
    return
  }
  
  //no errors, process data
  console.log(data)
})
```

### O problema com as callbacks

Callbacks são ótimas para casos simples!

No entanto, toda callback adiciona um nível de aninhamento e, quando você tem muitas callbacks, o código começa a se complicar muito rapidamente:

```
window.addEventListener('load', () => {
  document.getElementById('button').addEventListener('click', () => {
    setTimeout(() => {
      items.forEach(item => {
        //your code here
      })
    }, 2000)
  })
})
```

Este é apenas um código simples de quatro níveis, mas vi muito mais níveis de aninhamento e não é divertido.

Como solucionamos isso?

### Alternatives to callbacks

A partir do ES6, o JavaScript introduziu vários recursos que nos ajudam com código assíncrono que não envolve o uso de callbacks: 

- Promises (ES6)
- Async/Await (ES8)



