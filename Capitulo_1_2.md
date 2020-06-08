<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

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

## Promises

Promises são uma maneira de lidar com o código assíncrono, sem escrever muitos retornos de chamada no seu código.

Embora existam há anos, eles foram padronizados e introduzidos no ES2015 e agora foram substituídos no ES2017 por funções assíncronas (async functions).

As funções assíncronas (async functions) usam a API das promises como seu componente básico, portanto, entendê-las é fundamental, mesmo que no código mais recente você provavelmente use funções assíncronas (async functions) em vez de promises.

### Como as promises funcionam

Uma vez que uma promise tenha sido chamada, ela começará no estado pendente. Isso significa que a função de chamada continua a execução, enquanto aguarda a promise fazer seu próprio processamento e fornece algum feedback à função de chamada.

Nesse ponto, a função de chamada espera que ela retorne a promise em um estado resolvido ou em um estado rejeitado, mas como você sabe que o JavaScript é assíncrono, a função continua sua execução enquanto a promise funciona.

### Qual API do JS usa promises?

Além de seu próprio código e código de biblioteca, as promessas são usadas pelas APIs modernas padrão da Web, como Fetch ou Services Workers.

É improvável que no JavaScript moderno você não use promises, então vamos começar a mergulhar nelas.

### Criando uma promise

A API Promise expõe um construtor Promise, que você inicializa usando <kbg>new Promise()</kbg>:
```
let done = true

const isItDoneYet = new Promise((resolve, reject) => {
  if (done) {
    const workDone = 'Aqui é o que eu construí'
    resolve(workDone)
  } else {
    const why = 'Continua funciocando em outra coisa'
    reject(why)
  }
})
```
Como você pode ver, a promise verifica a constante global realizada e, se isso for verdade, retornamos uma promise resolvida, caso contrário, uma promise rejeitada.

Usando <kbg>resolve</kbg> e <kbg>reject</kbg>, podemos comunicar um valor novamente; no caso acima, retornamos apenas uma string, mas também poderia ser um objeto.

### Consumindo uma promise

Na última seção, nós instroduzimos como uma promise é criada.

Agora vamos ver como uma promise pode ser consumida ou usada.

```
const isItDoneYet = new Promise()
//...

const checkIfItsDone = () => {
  isItDoneYet
    .then(ok => {
      console.log(ok)
    })
    .catch(err => {
      console.error(err)
    })
}
```

## Async / Await

O JavaScript evoluiu em um período muito curto, desde callbacks até promises (ES2015), e desde o ES2017, o JavaScript assíncrono é ainda mais simples com a sintaxe <kbg>async / await</kbg>.

As async functions (funções assíncronas) são uma combinação de promises e geradores e, basicamente, são uma abstração de nível superior às promises. Deixe-me repetir: assíncrono / espera é construído sobre promises.

### Por que o async/await foi introduzido?

Eles reduzem o clichê em torno das promises e a limitação "não quebre a cadeia" do encadeamento de promises.

Quando as promises foram introduzidas no ES2015, elas pretendiam solucionar um problema com código assíncrono, e fizeram isso, mas nos dois anos que separaram o ES2015 e o ES2017, ficou claro que as promises não poderiam ser a solução final.

Promises foram introduzidas para resolver o famoso problema 'callback hell', mas introduziram complexidade por conta própria, além da complexidade de sintaxe.

Eles eram boas primitivas em torno das quais uma sintaxe melhor poderia ser exposta aos desenvolvedores; portanto, quando chegou a hora certa, obtivemos as async functions (funções assíncronas).

Eles fazem o código parecer síncrono, mas é assíncrono e sem bloqueio nos bastidores.

### Como funciona

Uma async function retorna uma promise, como no exemplo: 

```
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 3000)
  })
}
```

Quando você deseja chamar essa função, você acrescenta <kbg>await</kbg>, e o código de chamada será interrompido até que a promise seja resolvida ou rejeitada. Uma ressalva: a função deve ser definida como assíncrona. Aqui está um exemplo:

```
const doSomething = async () => {
  console.log(await doSomethingAsync())
}
```
### Um rápido exemplo

Esse é um exemplo simples de como um async/await roda uma função de forma assíncrona:

```
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('Eu fiz algo'), 3000)
  })
}

const doSomething = async () => {
  console.log(await doSomethingAsync())
}

console.log('Antes')
doSomething()
console.log('Depois')
```

O código acima imprimirá o seguinte no console do navegador:

```
Antes
Depois
Eu fiz algo //depois de 3s
```

<h2 align="center"><strong>SEÇÃO 2:</strong> CONCEITOS DO REACT </h2>

### Single Page Aplication (SPA)

Aplicações em React também são chamadas de Single Page Aplications. Mas o que isso significa?

No passado, quando os navegadores eram muito menos capazes do que hoje, e o desempenho do JavaScript era ruim, todas as páginas vinham de um servidor. Sempre que você clicava em algo, uma nova solicitação era feita ao servidor e o navegador carregava a nova página posteriormente.

Somente produtos muito inovadores funcionaram de maneira diferente e experimentaram novas abordagens.

Hoje, popularizado pelas modernas estruturas de front-end JavaScript, como o React, um aplicativo geralmente é criado como um aplicativo de página (single page aplication): você carrega o código do aplicativo (HTML, CSS, JavaScript) apenas uma vez e, quando você interage com o aplicativo, o que geralmente acontece é que JavaScript intercepta os eventos do navegador e, em vez de fazer uma nova solicitação ao servidor que retorna um novo documento, o cliente solicita algum JSON ou executa uma ação no servidor, mas a página que o usuário vê nunca é completamente apagada e se comporta mais como um aplicativo de desktop.

Single page applications are built in JavaScript (or at least compiled to JavaScript) and work in the browser.

Single page aplication são desenvolvidas em JavaScript (ou pelo menos compiladas para JavaScritp) e funcionam no browser.

A tecnologia é sempre a mesma, mas a filosofia e alguns components chaves de como a aplicação funciona são diferentes.

### Exemplos de Single Page Applications

- Gmail
- Google Maps
- Facebook
- Twitter
- Google Drive

### Prós e constras das SPA'S

Uma SPA é muito mais rápido para o usuário, porque, em vez de esperar a comunicação cliente-servidor, e esperar que o navegador renderize novamente a página, agora você pode obter feedback instantâneo. Isso é de responsabilidade do fabricante do aplicativo, mas você pode ter transições e spinners e qualquer tipo de aprimoramento de UX que seja certamente melhor do que o fluxo de trabalho tradicional.

Além de tornar a experiência mais rápida para o usuário, o servidor consumirá menos recursos, porque você pode se concentrar em fornecer uma API eficiente em vez de criar layouts do lado do servidor.

Isso o torna ideal se você também criar um aplicativo móvel sobre a API, pois poderá reutilizar completamente o código existente do lado do servidor.

As SPAs são fáceis de transformar em Progressive Web Apps, que, por sua vez, permitem fornecer armazenamento em cache local e oferecer suporte a experiências offline para seus serviços (ou simplesmente uma mensagem de erro melhor se seus usuários precisarem estar online).

As SPAs são mais utilizados quando não há necessidade de SEO (otimização de mecanismos de busca). Por exemplo, para aplicativos que funcionam atrás de um login.

Os mecanismos de pesquisa, embora melhorem a cada dia, ainda têm problemas para indexar sites criados com uma abordagem de SPA, em vez das páginas tradicionais renderizadas por servidor. Este é o caso dos blogs. Se você vai contar com os mecanismos de pesquisa, não se preocupe em criar um aplicativo de página única sem que um servidor também seja processado.

Ao codificar um SPA, você escreverá bastante JavaScript. Como o aplicativo pode ser demorado, você precisará prestar muito mais atenção a possíveis vazamentos de memória - se no passado sua página tinha uma vida útil contada em minutos, agora uma SPA pode ficar aberto por horas a fio. 

As SPAs são ótimos quando se trabalha em equipe. Os desenvolvedores de back-end podem se concentrar apenas na API, e os desenvolvedores de front-end podem se concentrar na criação da melhor experiência do usuário, fazendo uso da API criada no back-end.

Por isso, os aplicativos de página única dependem muito do JavaScript. Isso pode tornar o uso de um aplicativo executado em dispositivos de baixa potência uma experiência ruim em termos de velocidade. Além disso, alguns de seus visitantes podem ter o JavaScript desativado e você também precisa considerar a acessibilidade para qualquer coisa que criar.

### Substituindo a navegação

Como você se livra da navegação padrão do navegador, os URLs devem ser gerenciados manualmente.

Essa parte de um aplicativo é chamada de roteador. Algumas estruturas já cuidam delas para você (como o Ember), outras exigem bibliotecas que farão esse trabalho (como o React Router).

Qual é o problema? No começo, isso era uma reflexão tardia para os desenvolvedores que criam SPAs. Isso causou o problema comum de "botão quebrado": ao navegar no aplicativo, o URL não foi alterado (desde que a navegação padrão do navegador foi invadida) e ao pressionar o botão voltar, uma operação comum que os usuários fazem para ir para a tela anterior, pode4iq mudar para um site que você visitou há muito tempo.

Agora, esse problema pode ser resolvido usando a History API, oferecida pelos navegadores, mas na maioria das vezes você usa uma biblioteca que usa internamente essa API, como o React Router.

## Declarativo

O que significa quando você lê que React é declarativo? Você encontrará artigos que descrevem o React como uma abordagem declarativa para criar UIs.

O React tornou sua "abordagem declarativa" bastante popular e aberta, permeando o mundo frontend junto com o React.

Não é realmente um conceito novo, mas o React levou a criação de UIs muito mais declarativamente do que nos modelos HTML:

- você pode criar interfaces Web sem sequer tocar diretamente no DOM
- você pode ter um sistema de eventos sem precisar interagir com os eventos DOM reais.

O oposto de declarativo é imperativo. Um exemplo comum de uma abordagem imperativa é procurar elementos na DOM usando eventos jQuery ou DOM. Você diz ao navegador exatamente o que fazer, em vez de dizer o que precisa.

A abordagem declarativa React abstrai isso para nós. Apenas dizemos ao React que queremos que um componente seja renderizado de uma maneira específica e nunca precisamos interagir com a DOM para fazer referência a ele mais tarde.

## Imutabilidade

Um conceito que você provavelmente encontrará ao programar no React é a imutabilidade (e seu oposto, a mutabilidade).

É um tópico polêmico, mas seja o que for que você pense sobre o conceito de imutabilidade, o React e a maior parte do seu ecossistema o força, então você precisa pelo menos ter uma idéia de por que é tão importante e suas implicações.

Na programação, uma variável é imutável quando seu valor não pode ser alterado após a criação.

Você já está usando variáveis imutáveis sem saber quando manipula uma string. As strings são imutáveis por padrão, quando você as altera na realidade, você cria uma nova string e a atribui ao mesmo nome de variável.

Uma variável imutável nunca pode ser alterada. Para atualizar seu valor, você cria uma nova variável.

O mesmo se aplica a objetos e matrizes.

Em vez de alterar uma matriz, para adicionar um novo item, você cria uma nova matriz concatenando a matriz antiga e o novo item.

Um objeto nunca é atualizado, mas copiado antes de alterá-lo.

Isso se aplica ao React em muitos lugares.

Por exemplo, você nunca deve alterar a propriedade state de um componente diretamente, mas apenas através do método setState().

No Redux, você nunca muda o estado diretamente, mas apenas através de reducers, que são funções.

A questão é, por quê?

Existem várias razões, e as mais importantes são:

- As mutações podem ser centralizadas, como no caso do Redux, o que melhora os recursos de debbuging e reduz as fontes de erros.
- O código parece mais limpo e simples de entender. Você nunca espera que uma função altere algum valor sem que você saiba, o que lhe dá previsibilidade. Quando uma função não modifica objetos, mas apenas retorna um novo objeto, isso é chamado de função pura.
- A biblioteca pode otimizar o código porque, por exemplo, o JavaScript é mais rápido ao trocar uma referência de objeto antigo por um objeto totalmente novo, em vez de alterar um objeto existente. Isso lhe dá desempenho.

## Pureza

No JavaScript, quando uma função não modifica objetos, mas apenas retorna um novo objeto, ela é chamada de função pura.

Uma função ou método, para ser considero puro, não deve causar efeitos colaterais e deve retornar a mesma saída quando chamado várias vezes com a mesma entrada.

Uma função pura recebe uma entrada e retorna uma saída sem alterar a entrada.

Sua saída é determinada apenas pelos argumentos. Você poderia chamar essa função 1M vezes e, dado o mesmo conjunto de argumentos, a saída será sempre a mesma.

React aplica esse conceito aos componentes. Um componente React é um componente puro quando sua saída depende apenas de suas props.

Todos os componentes funcionais são componentes puros:
```
const Button = props => {
  return <button>{props.message}</button>
}
```
Os componentes de classe podem ser puros se sua saída depender apenas das props:

```
class Button extends React.Component {
  render() {
    return <button>{this.props.message}</button>
  }
}
```

## Composição

Na programação, a composição permite criar funcionalidades mais complexas combinando funções pequenas e focadas.

Por exemplo, pense em usar map () para criar uma nova matriz a partir de um conjunto inicial e, em seguida, filtrar o resultado usando filter ():

``
const lista = ['Maçã', 'Laranja', 'Ovo']
lista.map (item => item [0]). filter (item => item === 'A') // 'A'
``
No React, a composição permite que você tenha algumas vantagens interessantes.

Você cria componentes pequenos e os usa para compor mais funcionalidade sobre eles. Como?

### Criando uma versão especializada de um componente

Use um componente externo para expandir e especializar um componente mais genérico>

```
const Button = props => {
  return <button>{props.text}</button>
}

const SubmitButton = () => {
  return <Button text="Submit" />
}

const LoginButton = () => {
  return <Button text="Login" />
}
```

### Passando métodos como props

Um componente pode se concentrar no rastreamento de um evento de clique, por exemplo, e o que realmente acontece quando o evento de clique ocorre depende do componente do contêiner:
```
const Button = props => {
  return <button onClick={props.onClickHandler}>{props.text}</button>
}

const LoginButton = props => {
  return <Button text="Login" onClickHandler={props.onClickHandler} />
}

const Container = () => {
  const onClickHandler = () => {
    alert('clicked')
  }
  
  return <LoginButton onClickHandler={onClickHandler} />
}
```

### Usando Children

A propriedade <kbg>props.children</kbg> permite a você inserir componentes dentro de outros componentes.

O componente precisa enviar props.children no seu JSX:
```
const Sidebar = props => {
  return <aside>{props.children}</aside>
}
```

e você incorpora mais componentes nele de maneira transparente:

```
<Sidebar>
  <Link title="First link" />
  <Link title="Second link" />
</Sidebar>
```

### Componentes de ordem superior (high order components)

Quando um componente recebe um componente como props e retorna um componente, isso é chamado de componente de ordem superior.

Nós os veremos daqui a pouco.

## Virtual DOM

Muitos frameworks existentes, antes que o React aparecesse, manipulavam diretamente a DOM a cada alteração.

Primeiro, o que é a DOM?

A DOM (Document Object Model) é uma representação em árvore da página, iniciando na tag <html>, indo para todos os filhos, chamados de nós.

Ela é mantido na memória do navegador e diretamente vinculada ao que você vê em uma página. A DOM possui uma API que você pode usar para atravessá-la, acessar todos os nós, filtrá-los e modificá-los.

A API é a sintaxe familiar que você provavelmente já viu muitas vezes, se você não estava usando a API abstrata fornecida pelo jQuery e amigos:

```
document.getElementById(id)
document.getElementsByTagName(name)
document.createElement(name)
parentNode.appendChild(node)
element.innerHTML
element.style.left
element.setAttribute()
element.getAttribute()
element.addEventListener()
window.content
window.onload
window.dump()
window.scrollTo()
```

O React mantém uma cópia da representação da DOM, no que diz respeito à renderização do React: a virtual DOM


### A virtual DOM explicada

Sempre que a DOM é alterada, o navegador precisa realizar duas operações intensivas: repaint (alterações visuais ou de conteúdo em um elemento que não afeta o layout e o posicionamento em relação a outros elementos) e reflow (recalcular o layout de uma parte da página - ou o layout da página inteira).

O React usa uma virtual DOM para ajudar o navegador a usar menos recursos quando alterações precisam ser feitas em uma página.

Quando você chama setState() em um componente, especificando um state diferente do anterior, o React marca esse componente como sujo (dirty). Este é o ponto: o React apenas atualiza quando um componente altera o estado explicitamente.

O que acontece a seguir é:

- O React atualiza a virtual DOM em relação aos componentes marcados como sujos (com algumas verificações adicionais, como acionar shouldComponentUpdate ())
- Executa o algoritmo diffing para reconciliar as alterações
- Atualiza a DOM real

## Fluxo de dados unidirecional

Trabalhando com o React, você pode encontrar o termo Fluxo de dados unidirecional. O que isso significa? O fluxo de dados unidirecional não é um conceito exclusivo do React, mas como desenvolvedor JavaScript, pode ser a primeira vez que você o ouve.

Em geral, esse conceito significa que os dados têm uma e apenas uma maneira de serem transferidos para outras partes do aplicativo.

Em React, isso significa que:

- state é passado para a view e para os componentes filhos
- ações são acionadas pela view
- ações podem atualizar o state
- a mudança no state é passada para a view e para os componentes filhos

A view é resultado do state do aplicativo. O state só pode mudar quando ações acontecem. Quando ações acontecem, o state é atualizado.

Graças às ligações unidirecionais, os dados não podem fluir de maneira oposta (como aconteceria com as ligações bidirecionais, por exemplo), e isso tem algumas vantagens principais:

- é menos propenso a erros, pois você tem mais controle sobre seus dados
- é mais fácil de debugar, pois você sabe o que vem e de onde vem
- é mais eficiente, pois a biblioteca já sabe quais são os limites de cada parte do sistema

Um state sempre pertence a um componente. Quaisquer dados afetados por esse state podem afetar apenas os componentes abaixo dele: seus filhos.

A alteração do state em um componente nunca afetará seus pais, irmãos ou qualquer outro componente no aplicativo: apenas seus filhos.

Esse é o motivo pelo qual o state é frequentemente movido para cima na árvore de componentes, para que ele possa ser compartilhado entre os componentes que precisam acessá-lo.

