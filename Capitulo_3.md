<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 3:</strong> PROFUNDO NO REACT</h2>

## JSX

JSX é uma tecnologia que foi introduzida pelo React.

Embora o React possa funcionar completamente sem o uso do JSX, é uma tecnologia ideal para trabalhar com componentes, portanto, o React se beneficia muito com o JSX.

No começo, você pode pensar que usar JSX é como misturar HTML e JavaScript (e como você verá, CSS).

Mas isso não é verdade, porque o que você realmente está fazendo ao usar a sintaxe JSX é escrever uma sintaxe declarativa do que um componente da UI deve ser.

E você não está descrevendo essa interface do usuário usando seqüências de caracteres, e sim usando JavaScript, o que permite fazer muitas coisas legais.

### Um iniciador JSX

Aqui está como você define uma tag h1 que contém uma string:
```
const element = <h1> Olá, mundo! </h1>
```
Parece uma estranha mistura de JavaScript e HTML, mas, na realidade, é tudo JavaScript.

O que parece HTML, na verdade, é um 'açúcar sintático' para definir componentes e seu posicionamento dentro da marcação.

Dentro de uma expressão JSX, os atributos podem ser inseridos com muita facilidade:
```
const myId = 'test'
const element = <h1 id={myId}>Hello, world!</h1>
```

Você só precisa prestar atenção quando um atributo tem um traço (-) que é convertido na sintaxe camelCase, e nesses 2 casos especiais:

- class vira className
- for vira htmlFor

porque eles são palavras reservadas do JavaScript

Aqui está um snippet JSX que agrupa dois componentes em uma div:

```
<div>
  <BlogPostsList />
  <Sidebar />
</div>
```

Uma tag sempre precisa ser fechada, porque isso é mais XML que HTML (se você se lembrar dos dias XHTML, isso será familiar, mas desde então a sintaxe mínima do HTML5 ganhou). Nesse caso, uma tag de fechamento automático é usada.

Observe como eu agrupei os 2 componentes em uma div. Por quê? Como a função render() pode retornar apenas um único nó, portanto, caso você queira retornar 2 irmãos, basta adicionar um pai. Pode ser qualquer tag, não apenas div.

### Transpilando JSX

Um navegador não pode executar arquivos JavaScript que contêm código JSX. Eles devem ser primeiro transformados em JS regular.

Como? Ao fazer um processo chamado transpiling (algo como transpilação).

Já dissemos que o JSX é opcional, porque para cada linha JSX, uma alternativa JavaScript simples correspondente está disponível, e é para isso que o JSX é transpilado.

Por exemplo, as duas construções a seguir são equivalentes

> Plain JS
```
ReactDOM.render(
  React.DOM.div(
    { id: 'test' },
    React.DOM.h1(null, 'A title'),
    React.DOM.p(null, 'A paragraph')
  ),
  document.getElementById('myapp')
```

> JSX 
```
ReactDOM.render(
  <div id="test">
    <h1>A title</h1>
    <p>A paragraph</p>
  </div>,
  document.getElementById('myapp')
)
```
Este exemplo é apenas o ponto de partida, mas você já pode ver quão mais complicada é a sintaxe do JavaScript comparada ao uso do JSX.

No momento da digitação, a maneira mais popular de realizar a transpilação é usar o Babel, que é a opção padrão ao executar o create-react-app. Portanto, se você o usar, não precisará se preocupar, tudo acontece por baixo dos panos.

Se você não usa o app create-react, precisa configurar o Babel por conta própria.

### JS no JSX

O JSX aceita misturar qualquer tipo de JavaScript.

Sempre que você precisar adicionar algum JS, basta colocá-lo dentro de chaves {}. Por exemplo, veja como usar um valor definido em outro lugar:

```
const paragraph = 'A paragraph'
ReactDOM.render(
  <div id="test">
    <h1>A title</h1>
    <p>{paragraph}</p>
  </div>,
  document.getElementById('myapp')
)
```

Esse é um exemplo simples. As chaves aceitam qualquer tipo de JS.
```
const paragraph = 'A paragraph'
ReactDOM.render(
  <table>
    {rows.map((row, i) => {
      return <tr>{row.text}</tr>
    })}
  </table>,
  document.getElementById('myapp')
)
```
Como você pode ver, nós colocamos JS dentro de um JSX definido dentro de um JS aninhado em um JS (hehe aqui o autor se passou). Você pode ir tão 'fundo' quanto precisa.

### HTML no JSX

JSX lembra HTML um monte, mas na verdade é uma sintaxe XML.

No final, você renderiza HTML, portanto, é necessário conhecer algumas diferenças entre como você definiria algumas coisas em HTML e como você as define em JSX.

### Você precisar fechar todas as tags

Como no XHTML, se você ja utilizou ele alguma vez, você precisa fechar todas as tagas: sem mais `<br>`, ao  invés disso use a self-closing tag: `<br />`. O mesmo vale para outras tags.

### camelCase é o novo padrão

Em HTML, você encontrará atributos sem nenhum 'case' (por exemplo, onchange). No JSX, eles são renomeados para o equivalente em camelCase:

- onchange => onChange
- onclick => onClick
- onsubmit => onSubmit

### <kbg>class</kbg> vira <kbg>className</kbg>

Devido ao fato de JSX ser JavaScript, e classe ser uma palavra reservada do JS, você não pode escrever:

```
<p class="description">

```

você precisa usar:

```
<p className="description">
```

O mesmo se aplica para o <kbg>for</kbg>, que é transformado em <kbg>htmlFor</kbg>.

### CSS no React

JSX fornece uma maneira muito legal de definir o CSS.

Se você tem um pouco de experiência com estilos inline de HTML, à primeira vista, você volta 10 ou 15 anos para um mundo em que o inline CSS era completamente normal (hoje em dia é demonizado e geralmente é apenas uma “solução rápida”).

O styles do não é a mesma coisa: primeiro, em vez de aceitar uma sequência contendo propriedades CSS, o atributo <kbg>style</kbg> do JSX aceita apenas um objeto. Isso significa que você define propriedades em um objeto:

```
var divStyle = {
  color: 'white'
}

ReactDOM.render(<div style={divStyle}>Hello World!</div>, mountNode)
```

ou 

```
ReactDOM.render(<div style={{ color: 'white' }}>Hello World!</div>, mountNode)
```

Os valores CSS que você escreve em JSX são ligeiramente diferentes do CSS comun:

- o nome da propriedade é escrito em camelCase
- os valores são apenas strings
- você separa cada propriedade com uma vírgula

### Por que isso é preferível ao CSS / SASS / LESS?

CSS é um problema não resolvido. Desde a sua criação, dezenas de ferramentas ao seu redor ascenderam e caíram. O principal problema com o JS é que não há escopo e é fácil escrever CSS que não é forçado; portanto, uma "solução rápida" pode afetar elementos que não devem ser tocados.

O JSX permite que os componentes (definidos no React, por exemplo) encapsulem completamente seu estilo.

### Essa é a solução ideal?

Inline styles no JSX só são ótimos até que você precise:

1. escrever medias queries
2. fazer animações
3. referenciar pseudo classes (como o :hover)
4. referenciar pseudo elementos (como o ::first-letter)

Em resumo, eles cobrem o básico, mas não são a solução final.

### Formulários em JSX

Com o objetivo de facilitar as coisas para o desenvolvedor, o JSX adiciona algumas mudanças na maneira como os formulários do HTML funcionam.

### <kbg>value</kbg> e <kbg>defaultValue</kbg>

O atributo <kbg>value</kbg> sempre armazena o valor atual de um campo.

O <kbg>defaultValue</kbg> armazena o valor padrão que foi definido quando o campo foi criado.

Isso ajuda a resolver alguns comportamentos estranhos da interação com a DOM ao inspecionar o input.value e o input.getAttribute('value'), retornando um o valor atual e outro o valor padrão original.

O mesmo para <kbg>textarea</kbg>
```
<textarea> Algum texto </textarea>
```

que vira: 
```
<textarea defaultValue={'Algum texto'} />
```

### Para campos do tipo <kbg>select</kbg>

Em vez de usar 

```
<select>
  <option value="x" selected>
    ...
  </option>
</select>
```
use 
```
<select defaultValue="x">
  <option value="x">...</option>
</select>
```
### Um onChage mais consistente

Passando uma function para o atributo <kbg>onChange</kbg>, você pode definir eventos nos campo do formulário.

Isso funciona tranquilamente em outros campos, até no <kbg>radio</kbg>,  <kbg>select</kbg> e  <kbg>checkbox</kbg>.

O onChange também dispara quando um caracter é digitado dentro de um <kbg>textarea</kbg>

### Adicionando comentários JSX

Você pode adicionar comentários ao JSX usando os comentários normais do JavaScript em uma expressão:
```
<p>
  {/* um comentário */}
  {
    //outro comentário
  }
</p>
```

### Atributos Spread

No JSX, uma operação comum está atribuindo valores a atributos.

Em vez de fazê-lo manualmente, por exemplo:
```
<div>
  <BlogPost title={data.title} date={data.date} />
</div>
```

você pode fazer:

```
<div>
  <BlogPost {...data} />
</div>
```

e as propriedades do objeto de dados serão usadas como atributos automaticamente, graças ao operador spread do ES6.

### Como fazer um loop no JSX

Se você tiver um conjunto de elementos em que precisará fazer loop para gerar um JSX parcial, poderá criar um loop e adicionar JSX a uma matriz:

```
const elements = [] //..algum array

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<Element key={index} />)
}
```

Agora, ao renderizar o JSX, você pode incorporar a matriz de itens simplesmente envolvendo-a em chaves:

```
const elements = ['one', 'two', 'three'];

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<li key={index}>{value}</li>)
}

return (
  <div>
    {items}
  </div>
)
```
Você pode fazer o mesmo diretamente no JSX, usando map em vez de um loop for-of (esse eu recomendo muuito):

```
const elements = ['one', 'two', 'three'];
return (
  <ul>
    {elements.map((value, index) => {
      return <li key={index}>{value}</li>
    })}
  </ul>
)
```

## Componentes

Um componente é uma parte isolada da interface. Por exemplo, em uma página inicial típica do blog, você pode encontrar o componente Barra Lateral e o componente Lista de Postagens do Blog. Por sua vez, eles são compostos pelos próprios componentes, para que você possa ter uma lista dos componentes da postagem do blog, cada um para cada postagem do blog e cada um com suas próprias propriedades peculiares.

React torna muito simples: tudo é um componente.

Até as tags HTML simples são componentes por conta própria e são adicionadas por padrão.

As próximas 2 linhas são equivalentes, elas fazem a mesma coisa. Um com JSX, outro sem, injetando `<h1> Hello World! </h1>` em um elemento com o id app.

```
import React from 'react'
import ReactDOM from 'react-dom'

ReactDOM.render(<h1>Hello World!</h1>, document.getElementById('app'))

ReactDOM.render(
  React.DOM.h1(null, 'Hello World!'),
  document.getElementById('app')
)
```
Veja, React.DOM nos expôs um componente h1. Quais outras tags HTML estão disponíveis? Todos eles! Você pode inspecionar o que o React.DOM oferece digitando-o no console do navegador:

(a lista é mais longa)

Os componentes internos são bons, mas você os supera rapidamente. O que o React se destaca é nos permitir compor uma interface do usuário compondo componentes personalizados.

### Componentes customizados

Tem dois modos de definir um componente no React.

A componente funcional:
```
const BlogPostExcerpt = () => {
  return (
    <div>
      <h1>Title</h1>
      <p>Description</p>
    </div>
  )
}
```

Um componente de classe: 
```
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <div>
        <h1>Title</h1>
        <p>Description</p>
      </div>
    )
  }
}
```
Até recentemente, os componentes de classe eram a única maneira de definir um componente que tinha seu próprio state e podia acessar os métodos do ciclo de vida para que você pudesse fazer as coisas quando o componente fosse renderizado, atualizado ou removido pela primeira vez.

O React Hooks mudou isso, então nossos componentes funcionais agora são muito mais poderosos do que nunca e acredito que veremos cada vez menos componentes de classe no futuro, embora ainda seja uma maneira perfeitamente válida de criar componentes.

## State 

### Configurando um state padrão para um componente

No constructor do componente, inicialize this.state. Por exemplo, o componente BlogPostExcerpt pode ter um state chamado <kbg>clicked</kbg>:

```
class BlogPostExcerpt extends Component {
  constructor(props) {
    super(props)
    this.state = { clicked: false }
  }
  
  render() {
    return (
      <div>
        <h1>Title</h1>
        <p>Description</p>
      </div>
    )
  }
}
```

### Acessando o state

O <kbg>clicked</kbg> pode ser acessado referenciando <kbg>this.state.clicked</kbg>

```
class BlogPostExcerpt extends Component {
  constructor(props) {
    super(props)
    this.state = { clicked: false }
  }
  
  render() {
    return (
      <div>
        <h1>Title</h1>
        <p>Description</p>
        <p>Clicked: {this.state.clicked}</p>
      </div>
    )
  }
}
```

### Mutando o state

Um state nunca pode ser mudado usando:

```
this.state.clicked = true
```

Em vez disso, você sempre deve usar o setState()

```
this.setState({ clicked: true })
```

O objeto pode conter um subconjunto ou um superconjunto do state. Somente as propriedades que você passar serão mutadas, as omitidas serão deixadas no estado atual.

### Porque você sempre deve usar o setState()

O motivo é que, usando esse método, o React sabe que o state mudou. Ele iniciará a série de eventos que levarão à renderização do componente, juntamente com qualquer atualização da DOM.

### Fluxo de dados unidirecional

Um state sempre pertence a um componente. Quaisquer dados afetados por esse state podem afetar apenas os componentes abaixo dele: seus filhos.

Alterar o state de um componente nunca afetará seus pais, irmãos ou qualquer outro componente no aplicativo: apenas seus filhos.

Esse é o motivo pelo qual o state é frequentemente movido para cima na árvore de componentes.

### Movendo o state na árvore

Por causa da regra Fluxo de Dados Unidirecional, se dois componentes precisarem compartilhar state, ou o state pode ser movido por um ancestral comum.

Muitas vezes, o ancestral mais próximo é o melhor lugar para gerenciar o state, mas não é uma regra obrigatória.

O state é passado para os componentes que precisam desse valor por meio das props:
```
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.state = { currency: '€' }
  }
  
  render() {
    return (
      <div>
        <Display currency={this.state.currency} />
        <CurrencySwitcher currency={this.state.currency} />
      </div>
    )
  }
}
```

O state pode ser modificado por um componente filho passando uma função de mutação para baixo como uma props:
```
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.state = { currency: '€' }
  }
  
  handleChangeCurrency = event => {
    this.setState({ currency: this.state.currency === '€' ? '$' : '€' })
  }
  
  render() {
    return (
      <div>
        <Display currency={this.state.currency} />
        <CurrencySwitcher
          currency={this.state.currency}
          handleChangeCurrency={this.handleChangeCurrency}
        />
      </div>
    )
  }
}

const CurrencySwitcher = props => {
  return (
    <button onClick={props.handleChangeCurrency}>
      Current currency is {props.currency}. Change it!
    </button>
  )
}

const Display = props => {
  return <p>Current currency is {props.currency}.</p>
}
```

## Props

Props é como os componentes obtêm suas propriedades. A partir do componente superior, cada componente filho recebe seus props do pai. Em um componente funcional, <kbg>props</kbg> é tudo o que é passado, e eles estão disponíveis adicionando props como argumento da função:

```
const BlogPostExcerpt = props => {
  return (
    <div>
      <h1>{props.title}</h1>
      <p>{props.description}</p>
    </div>
  )
}
```

Em um componente baseado em classe, as props são transmitidas por padrão. Não há necessidade de adicionar nada de especial, e eles podem ser acessados como <kbg>this.props</kbg> em uma instância de Component.

```
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </div>
    )
  }
}
```

Passar props para componentes filhos é uma ótima maneira de passar valores em sua aplicação. Um componente retém dados (possui state) ou recebe dados por meio de seus props.

Fica complicado quando:

- você precisa acessar o estado de um componente a partir de uma child que está em vários níveis (todas as childs anteriores precisam agir como uma passagem, mesmo que não precisem conhecer o props, complicando as coisas).
- você precisa acessar o state de um componente a partir de um componente completamente não relacionado.

### Default values (valores padrão) para as props

Se algum valor não for necessário, precisamos especificar um valor padrão para ele se ele estiver ausente quando o componente for inicializado.

```
BlogPostExcerpt.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string
}

BlogPostExcerpt.defaultProps = {
  title: '',
  description: ''
}
```

Algumas ferramentas como ESLint têm a capacidade de impor a definição de defaultProps para um Componente com alguns propTypes não explicitamente necessários.

### Como as props são passadas 

Ao inicializar um componente, passe os adereços de maneira semelhante aos atributos HTML:
```
const desc = 'A description'
//...
<BlogPostExcerpt title="A blog post" description={desc} />
```

Passamos o título como uma string simples (algo que só podemos fazer com strings!) E a descrição como uma variável.

### Children 

Umas props especiais sãos as <kbg>childrens</kbg>(crianças). Que contém o valor de qualquer coisa que seja passada no <kbg>body</kbg> do componente, por exemplo:
```
<BlogPostExcerpt title="A blog post" description="{desc}">
  Something
</BlogPostExcerpt>
```

Neste caso, dentro de <kbg>BlogPostExcerpt</kbg> nós podemos acessar <kbg>Something</kbg> utilizando <kbg>this.props.children</kbg>.

Enquanto Props permitem que um Componente receba propriedades de seu pai, e seja "instruído" a imprimir alguns dados, por exemplo, o state permite que um componente ganhe vida própria e seja independente do ambiente ao redor.

## Componentes de apresentação versus contêiner

No React, componentes são geralmente divididos em 2 pacotes: presentational components versus container components.

Cada um tem suas próprias características.

Presentational components preocupam-se principalmente em gerar alguma marcação a ser produzida.

Eles não gerenciam nenhum tipo de state, exceto o state relacionado à apresentação

Os container components estão preocupados principalmente com as operações de "back-end".

Eles podem lidar com o estado de vários subcomponentes. Eles podem agrupar vários componentes de apresentação. Eles podem interagir com o Redux.

Como uma maneira de simplificar a distinção, podemos dizer que os presentational components estão preocupados com a aparência, os container components estão preocupados em fazer as coisas funcionarem.

Por exemplo, este é um presentational components. Ele obtém dados de seus objetos e se concentra apenas em mostrar um elemento:
```
const Users = props => (
  <ul>
    {props.users.map(user => (
      <li>{user}</li>
    ))}
  </ul>
)
```

Por outro lado, este é um container components. Ele gerencia e armazena seus próprios dados e usa o presentation component para exibi-los.

```
class UsersContainer extends React.Component {
  constructor() {
    this.state = {
      users: []
    }
  }
  
  componentDidMount() {
    axios.get('/users').then(users =>
      this.setState({ users: users }))
    )
  }
  
  render() {
    return <Users users={this.state.users} />
  }
}
```

## State vs Props

Em um componente React, props são variáveis transmitidas a ele por seu componente pai. O state, por outro lado, ainda é variável, mas diretamente inicializado e gerenciado pelo componente.

O state pode ser inicializado por props.

Por exemplo, um componente pai pode incluir um componente filho chamando

```
<ChildComponent />
```

O pai pode passar uma props usando essa sintaxe:
```
<ChildComponent color=green />
```

Dentro do construtor do ChildComponent nós podemos acessar a props:
```
class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
    console.log(props.color)
  }
}
```

e qualquer outro método nesta classe pode fazer referência aos objetos usando this.props.

Props podem ser usados para definir o state interno com base em um valor da props no construtor, assim:
```
class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state.colorName = props.color
  }
}
```

Obviamente, um componente também pode inicializar o state sem olhar para as props.

Nesse caso, não há nada útil acontecendo, mas imagine fazer algo diferente com base no valor das props, provavelmente definir o valor do state é o melhor.

As props nunca devem ser alterados em um componente filho; portanto, se houver algo que altere alguma variável, essa variável deve pertencer ao state do componente.

As props também são usadas para permitir que os componentes filhos acessem os métodos definidos no componente pai. Essa é uma boa maneira de centralizar o gerenciamento do state no componente pai e evitar que os filhos precisem ter seu próprio state.

A maioria dos seus componentes exibe apenas algum tipo de informação com base nas props que eles receberam e permanece sem estado.

## PropTypes

Como o JavaScript é uma linguagem de tipagem dinâmico, não temos realmente uma maneira de impor o tipo de variável em tempo de compilação e, se passarmos tipos inválidos, eles falharão no tempo de execução ou darão resultados estranhos se os tipos forem compatíveis, mas não o que esperamos.

O Flow e o TypeScript ajudam muito, mas o React tem uma maneira de ajudar diretamente com os tipos de props, e mesmo antes de executar o código, nossas ferramentas (editores, linters) podem detectar quando estamos transmitindo os valores errados:

```
import PropTypes from 'prop-types'
import React from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </div>
    )
  }
}

BlogPostExcerpt.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string
}

export default BlogPostExcerpt
```

### Quais tipos nós podemos usar

Existem tipos fundamentais que podemos utilizar:

- PropTypes.array
- PropTypes.bool
- PropTypes.func
- PropTypes.number
- PropTypes.object
- PropTypes.string
- PropTypes.symbol

### Requiring properties (Exigindo propriedades)

Anexar <kbg>isRequired</kbg> a qualquer opção PropTypes fará com que o React retorne um erro se essa propriedade estiver ausente:

```
PropTypes.arrayOf(PropTypes.string).isRequired,
PropTypes.string.isRequired,
```

## React Fragment

Observe como envolvo os valores de retorno em uma <kbg>div</kbg>. Isso ocorre porque um componente pode retornar apenas um único elemento e, se você quiser mais de um, precisará envolvê-lo com outra tag de contêiner.

Isso, no entanto, causa uma divisão desnecessária na saída. Você pode evitar isso usando <kbg>React.Fragment</kbg>:
```
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <React.Fragment>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </React.Fragment>
    )
  }
}
```

que também possui uma sintaxe mais curta `<></>`, suportada nas versões mais recentes 
```
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </>
    )
  }
}
```

## Eventos

O React fornece uma maneira fácil de gerenciar eventos. Prepare-se para dizer adeus ao addEventListener.

No artigo anterior sobre o State, você viu este exemplo:
```
const CurrencySwitcher = props => {
  return (
    <button onClick={props.handleChangeCurrency}>
      Current currency is {props.currency}. Change it!
    </button>
  )
}
```

Se você usa JavaScript há algum tempo, isso é como manipuladores de eventos antigos e simples, exceto que desta vez você está definindo tudo em JavaScript, não em seu HTML, e passando uma função, não uma string.

Os nomes dos eventos reais são um pouco diferentes, porque no React você usa camelCase para tudo, então onclick se torna onClick, o onsubmit se torna onSubmit.

Para referência, este é o HTML 'antigo' com eventos JavaScript misturados:
```
<button onclick="handleChangeCurrency()">...<;/button>
```

## Event Handlers

(Uma tradução literal para event handlers seria 'manipuladores de eventos', porém, optei por utilizar o nome em inglês)


É uma convenção ter event handlers definidos como métodos nos componentes baseados em classe:

```
class Converter extends React.Component {
  handleChangeCurrency = event => {
    this.setState({ currency: this.state.currency === '€' ? '$' : '€' })
  }
}
```

## Bind <kbg>this</kbg> em métodos

Se você usa componentes de classe, não se esqueça de vincular (dar um bind) métodos. Os métodos das classes ES6, por padrão, não são vinculados. O que isso significa é que isso não é definido, a menos que você defina métodos com <kbg>Arrows functions</kbg>:
```
class Converter extends React.Component {
  handleClick = e => {
    /* ... */
  }
  //...
}
```

você também pode configurá-lo manualmente no construtor:
```
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.handleClick = this.handleClick.bind(this)
  }
  handleClick(e) {}
}
```

### A referência de eventos

Existem muitos eventos suportados. Aqui está uma lista resumida.

### Clipboard
- onCopy
- onCut
- onPaste
### Composition
- onCompositionEnd
- onCompositionStart
- onCompositionUpdate
### Keyboard
- onKeyDown
- onKeyPress
- onKeyUp
### Focus
- onFocus
- onBlur
### Form
- onChange
- onInput
- onSubmit
### Mouse
- onClick
- onContextMenu
- onDoubleClick
- onDrag
- onDragEnd
- onDragEnter
- onDragExit
- onDragLeave
- onDragOver
- onDragStart
- onDrop
- onMouseDown
- onMouseEnter
- onMouseLeave
- onMouseMove
- onMouseOut
- onMouseOver
- onMouseUp
### Selection
- onSelect
### Touch
- onTouchCancel
- onTouchEnd
- onTouchMove
- onTouchStart
### UI
- onScroll
### Mouse Wheel
- onWheel
### Media
- onAbort
- onCanPlay
- onCanPlayThrough
- onDurationChange
- onEmptied
- onEncrypted
- onEnded
- onError
- onLoadedData
- onLoadedMetadata
- onLoadStart
- onPause
- onPlay
- onPlaying
- onProgress
- onRateChange
- onSeeked
- onSeeking
- onStalled
- onSuspend
- onTimeUpdate
- onVolumeChange
- onWaiting
### Image
- onLoad
- onError
### Animation
- onAnimationStart
- onAnimationEnd
- onAnimationIteration
### Transition
- onTransitionEnd

## Lifecycle Events (eventos de ciclo de vida)

Os componentes baseados em classe do React podem ter ganchos(hooks) para vários lifecycle events.

> Hooks permite aos componentes funcionais acessá-los também, de uma maneira diferente

Durante a vida útil de um componente, há uma série de eventos chamados e, para cada evento, você pode conectar e fornecer funcionalidades personalizadas.

Qual hook é melhor para cada funcionalidade é algo que veremos aqui.

Primeiro, há 3 fases no ciclo de vida do componente React:

- Mounting 
- Updating 
- Unmounting

Vamos ver essas três fases em detalhes e os métodos chamados para cada uma.

### Mounting

No mounting, você tem 4 métodos de ciclo de vida antes de o componente ser montado no DOM: o constructor, getDerivedStateFromProps, render e componentDidMount.

#### Constructor

O constructor é o primeiro método chamado ao montar um componente.

Você geralmente usa o construtor para configurar o state inicial usando this.state = ....

#### getDerivedStateFromProps()

Quando o state depende das props, getDerivedStateFromProps pode ser usado para atualizar o state com base no valor das props.

Foi adicionado no React 16.3, com o objetivo de substituir o método obsoleto componentWillReceiveProps.

Neste método, você não tem acesso ao <kbg>this</kbg>, pois é um método estático.

É um método puro, portanto, não deve causar efeitos colaterais e deve retornar a mesma saída quando chamado várias vezes com a mesma entrada.

Retorna um objeto com os elementos atualizados do state (ou nulo se o state não for alterado)

#### render()

No método render (), você retorna o JSX que constrói a interface do componente.

É um método puro, portanto, não deve causar efeitos colaterais e deve retornar a mesma saída quando chamado várias vezes com a mesma entrada.

#### componentDidMount ()

Esse método é o que você usará para executar chamadas de API ou processar operações no DOM.
Ele será executado após o render() estar completo.

### Updating

Ao atualizar(updating), você tem 5 métodos de ciclo de vida antes da montagem do componente no DOM: getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate e componentDidUpdate.

#### getDerivedStateFromProps()

Mesma descrição feita acima.

#### shouldComponentUpdate()

Este método retorna um valor booleano, <kbg>true</kbg> ou <kbg>false</kbg>. Você usa esse método para informar ao React se deve continuar com a renderização novamente. O padrão é <kbg>true</kbg>. Você retornará <kbg>false</kbg> quando a renderização for cara e você desejar ter mais controle quando isso acontecer.

### Unmount
Nesta fase temos apenas um método, o componentWillUnmount.

#### componentWillUnmount() 

O método é chamado quando o componente é removido do DOM. Use isso para fazer qualquer tipo de limpeza que você precise executar.

### Legado

Se você estiver trabalhando em um aplicativo que usa componentWillMount, componentWillReceiveProps ou componentWillUpdate, esses itens foram descontinuados no React 16.3 e você deve migrar para outros métodos de ciclo de vida.


## Formulários no React

Os formulários são um dos poucos elementos HTML interativos por padrão.

Eles foram projetados para permitir que o usuário interaja com uma página.

Usos comuns de formulários?

- Pesquisa
- Formulários de contato
- Checkout no carrinho em uma loja virtual
- Login e cadastro

Usando React, podemos tornar nossos formulários muito mais interativos e menos estáticos.

Existem duas maneiras principais de lidar com formulários no React, que diferem em um nível fundamental: como os dados são gerenciados.

- se os dados são manipulados pela DOM, os chamamos de componentes não controlados
- se os dados são tratados pelos componentes, os chamamos de componentes controlados

Como você pode imaginar, um componente controlado é o que você usará na maioria das vezes. O state do componente é a única fonte da verdade, e não o DOM. Alguns campos de formulário são inerentemente não controlados devido ao seu comportamento, como o campo <input type = "file">.

Quando um state do elemento é alterado em um campo de formulário gerenciado por um componente, nós o rastreamos usando o atributo <kbg>onChange</kbg>.

```
class Form extends React.Component {
  constructor(props) {
    super(props)
    this.state = { username: '' }
  }
  
  handleChange(event) {}
  
  render() {
    return (
      <form>
        Username:
        <input
          type="text"
          value={this.state.username}
          onChange={this.handleChange}
        />
      </form>
    )
  }
}
```

Para definir o novo state, devemos vincular (dar um bind) o <kbg>this</kbg> ao método handleChange, caso contrário, o <kbg>this</kbg> não poderá ser acessado nesse método:

```
class Form extends React.Component {
  constructor(props) {
    super(props)
    this.state = { username: '' }
    this.handleChange = this.handleChange.bind(this)
  }
  
  handleChange(event) {
    this.setState({ value: event.target.value })
  }
  
  render() {
    return (
      <form>
        <input
          type="text"
          value={this.state.username}
          onChange={this.handleChange}
        />
      </form>
    )
  }
}
```

## Referenciando um elemento da DOM

O React é excelente em abstrair a DOM para você ao criar aplicativos.

Mas e se você quiser acessar o elemento da DOM que um componente React representa?

Talvez você precise adicionar uma biblioteca que interaja diretamente com a DOM, como uma biblioteca de gráficos. Ou talvez precise chamar alguma API do DOM. Ou adicionar foco a um elemento.

> Seja qual for o motivo, uma boa prática é garantir que não haja outra maneira de fazer isso sem acessar o DOM diretamente.

No JSX do seu componente, você pode atribuir a referência do elemento na DOM a uma propriedade do componente usando este atributo:

```
ref={el => this.someProperty = el}
```

Botando isso em um contexto, por exemplo com o elemento <kbg>button</kbg>

```
<button ref={el => (this.button = el)} />
```

## Renderização no lado do servidor (Server side rendering)

A Server Side Renderign, também chamada SSR, é a capacidade de um aplicativo JavaScript renderizar no servidor e não no navegador.

Por que deveríamos fazer isso?

- permite que seu site tenha um tempo de carregamento de primeira página mais rápido, que é a chave para uma boa experiência do usuário
- é essencial para o SEO: os mecanismos de pesquisa ainda não conseguem indexar de maneira eficiente e correta os aplicativos que processam exclusivamente o cliente. Apesar das melhorias mais recentes na indexação no Google, também existem outros mecanismos de pesquisa, e o Google não é perfeito em nenhum caso. Além disso, o Google favorece sites com tempos de carregamento rápidos, e ter que carregar do lado do cliente não é bom para velocidade
- é ótimo quando as pessoas compartilham uma página do seu site nas mídias sociais, pois podem coletar facilmente os metadados necessários para compartilhar o link de maneira agradável (imagens, título, descrição ..)

Sem a renderização no lado do servidor, todo o servidor é uma página HTML sem corpo, apenas algumas tags de script que são usadas pelo navegador para renderizar o aplicativo.

Os aplicativos renderizados pelo cliente são ótimos em qualquer interação subsequente do usuário após o carregamento da primeira página. A renderização no lado do servidor nos permite obter o ponto ideal entre aplicativos renderizados pelo cliente e aplicativos renderizados no back-end: a página é gerada no lado do servidor, mas todas as interações com a página após o carregamento são tratadas no lado do cliente.

No entanto, a renderização no servidor também tem sua desvantagem:

- é justo dizer que uma simples prova de conceito de SSR é simples, mas a complexidade do SSR pode aumentar com a complexidade do seu aplicativo
- a renderização de um grande aplicativo no lado do servidor pode consumir muitos recursos e, sob carga pesada, pode até proporcionar uma experiência mais lenta que a renderização no lado do cliente, pois você possui um único gargalo

### Um exemplo muito simplista do que é necessário para renderizar um aplicativo React no lado do servidor

As configurações de SSR podem se tornar muito, muito complexas e a maioria dos tutoriais serão focados no Redux, React Router e muitos outros conceitos desde o início.

Para entender como o SSR funciona, vamos começar do básico para implementar uma prova de conceito.

> Sinta-se à vontade para pular este parágrafo se quiser apenas olhar para as bibliotecas que fornecem SSR e não se preocupar com o trabalho de base

Para implementar o SSR básico, usaremos o Express.

> Se você é novo no Express, ou precisa de alguma atualização, consulte meu Manual Express gratuito aqui: https://flaviocopes.com/page/ebooks/.

Aviso: a complexidade do SSR pode aumentar com a complexidade do seu aplicativo. Esta é a configuração mínima para renderizar um aplicativo React básico. Para necessidades mais complexas, talvez você precise fazer um pouco mais de trabalho ou também consulte as bibliotecas SSR do React.

Suponho que você iniciou um aplicativo React com create-react-app. Se você está apenas tentando, instale um agora usando o npx create-react-app ssr.

Vá para a pasta principal do aplicativo com o terminal e execute:

```
npm install express
```

Você tem um conjunto de pastas no diretório do aplicativo. Crie uma nova pasta chamada server, depois entre nela e crie um arquivo chamado `server.js`.

Seguindo as convenções do create-react-app, o aplicativo fica no arquivo `src / App.js`. Vamos carregar esse componente e renderizá-lo em uma string usando `ReactDOMServer.renderToString()`, fornecido pelo `react-dom`.

Você obtém o conteúdo do arquivo `./build/index.html` e substitui o espaço reservado `<div id = "root"> </div>`, que é a marca na qual o aplicativo é conectado por padrão, por `<div id =" root "> \ $ {ReactDOMServer.renderToString (<App />)} </div>`.

Todo o conteúdo dentro da pasta de compilação será veiculado como está, estaticamente, pelo Express.
```
import path from 'path'
import fs from 'fs'

import express from 'express'
import React from 'react'
import ReactDOMServer from 'react-dom/server'

import App from '../src/App'

const PORT = 8080
const app = express()

const router = express.Router()

const serverRenderer = (req, res, next) => {
  fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
    if (err) {
      console.error(err)
      return res.status(500).send('An error occurred')
    }
    return res.send(
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
      )
    )
  })
}
router.use('^/$', serverRenderer)

router.use(
  express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' })
)

// tell the app to use the above rules
app.use(router)

// app.use(express.static('./build'))
app.listen(PORT, () => {
  console.log(`SSR running on port ${PORT}`)
})
```

Agora, no aplicativo cliente, em seu `src / index.js`, em vez de chamar ReactDOM.render():

```
ReactDOM.render (<App />, document.getElementById('root'))
```

chame `ReactDOM.hydrate()`, que é o mesmo, mas possui a capacidade adicional de anexar event listeners à marcação existente quando o React for carregado:

```
ReactDOM.hydrate (<App />, document.getElementById ('root'))
```

Todo o código Node.js. precisa ser transpilado pelo Babel, pois o código Node.js. do servidor não sabe nada sobre JSX, nem sobre os Módulos ES (que usamos para as instruções de inclusão).

Instale estes 3 pacotes:

```
npm install @ babel / register @ babel / preset-env @ babel / preset-react ignore-styles express
```

`ignore-styles` é um utilitário Babel que o instrui a ignorar arquivos CSS importados usando a sintaxe de importação.

```
require('ignore-styles')
```

Vamos criar um ponto de entrada no server / index.js:
```
require ('@ babel / register') ({
  ignore: [/ (node_modules) /],
  presets: ['@ babel / preset-env', '@ babel / preset-react']
})

require ('./ server')
```

Crie o aplicativo React, para que a compilação / pasta seja preenchida:
```
npm run build
```

e vamos executar isso:
```
node server / index.js
```


Eu disse que essa é uma abordagem simplista e é:

- não processa a renderização de imagens corretamente ao usar importações, que precisam do Webpack para funcionar (e que complica muito o processo)
- não trata os metadados do cabeçalho da página, o que é essencial para fins de compartilhamento social e de SEO (entre outras coisas)

Portanto, embora este seja um bom exemplo do uso de ReactDOMServer.renderToString() e ReactDOM.hydrate para obter essa renderização básica do lado do servidor, não é suficiente para o uso no mundo real.

### Server Side Rendering usando bibliotecas

É difícil fazer o SSR corretamente, e o React não tem como de fato implementá-lo.

Ainda é muito discutível se vale a pena o esforço, a complicação e a sobrecarga para obter os benefícios, em vez de usar uma tecnologia diferente para servir essas páginas. Esta discussão no Reddit tem muitas opiniões a esse respeito.

Quando a renderização no servidor é um assunto importante, minha sugestão é confiar em bibliotecas e ferramentas pré-fabricadas que tenham esse objetivo em mente desde o início.

Em particular, sugiro o Next.js e o Gatsby, dois projetos que veremos mais adiante.

## Context API

É uma maneira elegante de passar o state pelo aplicativo sem precisar usar props. Foi introduzido para permitir a passagem do state (e a atualização do state) pelo aplicativo, sem a necessidade de usar props.

A equipe do React sugere manter os props se você tiver apenas alguns níveis de filhos para passar, porque ainda é uma API muito menos complicada do que a Context API.

Em muitos casos, ela evita o uso do Redux, simplifica bastante os aplicativos e também aprende a usar o React.

Como funciona?

Você cria um contexto usando <kbg>React.createContext()</kbg>, que retorna um objeto Context:
```
const { Provider, Consumer } = React.createContext()
```
Em seguida, você cria um componente wrapper(container/embrulho) que retorna um componente Provider e adiciona como filhos todos os componentes dos quais você deseja acessar o contexto:

```
class Container extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      something: 'hey'
    }
  }
  
  render() {
    return (
      <Provider value={{ state: this.state }}>{this.props.children}</Provider>
    )
  }
}

class HelloWorld extends React.Component {
  render() {
    return (
      <Container>
        <Button />
      </Container>
    )
  }
}
```
Eu usei Container como o nome desse componente porque este será um Provider global. Você também pode criar contextos menores.

Dentro de um componente envolvido em um <kbg>Provider</kbg>, você usa um componente <kbg>Consumer</kbg> para fazer uso do contexto:

```
class Button extends React.Component {
  render() {
    return (
      <Consumer>
        {context => <button>{context.state.something}</button>}
      </Consumer>
    )
  }
}
```

Você também pode passar funções para um valor de Provider, e essas funções serão usadas pelo Consumer para atualizar o estado do contexto:
```
<Provider value={{
  state: this.state,
  updateSomething: () => this.setState({something: 'ho!'})
  {this.props.children}
</Provider>

/* ... */
<Consumer>
  {(context) => (
    <button onClick={context.updateSomething}>{context.state.something}</button>
  )}
</Consumer>
```

Você pode criar vários contextos, para distribuir seu estado entre componentes, mas expô-lo e alcançá-lo por qualquer componente que desejar.

Ao usar vários arquivos, você cria o conteúdo em um arquivo e importa-o em todos os locais em que o usa:

```
//context.js
import React from 'react'
export default React.createContext()

//component1.js
import Context from './context'
//... use Context.Provider

//component2.js
import Context from './context'
//... use Context.Consumer
```

## Componentes de ordem superior (Higher order components)

Você pode estar familiarizado com as Funções de ordem superior em JavaScript. Essas são funções que aceitam funções como argumentos e/ou retornam funções.

Dois exemplos dessas funções são `Array.map()` ou `Array.filter()`.

No React, estendemos esse conceito aos componentes e, portanto, temos um HOC (High Order Order Component) quando o componente aceita um componente como entrada e retorna um componente como saída.

Em geral, os componentes de ordem superior permitem criar código que pode ser composto, reutilizado e encapsulado.

Podemos usar um HOC para adicionar métodos ou propriedades ao state de um componente ou a um Redux store, por exemplo.

Você pode usar componentes de ordem superior quando desejar aprimorar um componente existente, operar no state e objetos ou aprimorar sua marcação renderizada.

Existe uma convenção de anexar um componente de ordem superior à string <kbg>with</kbg> (é uma convenção, portanto não é obrigatória); portanto, se você tiver um componente <kbg>Button</kbg>, seu equivalente HOC deverá ser chamado <kbg>Button</kbg>.

Vamos criar um.

O exemplo mais simples de um HOC é aquele que simplesmente retorna o componente inalterado:
```
const withElement = Element => () => &lt;Element />
```

Vamos tornar isso um pouco mais útil e adicionar uma propriedade a esse botão, além de todas as props que já acompanham ele, a cor:

```
const withColor = Element => props => <Element {...props} color="red" />
```

Nós usamos esse HOC em um JSX

```
const Button = () => {
  return <button>test</button>
}

const ColoredButton = withColor(Button)
```

e nós finalmente podemos renderizar o <kbg>ColoredButton</kbg> em nossa tela:
```
function App() {
  return (
    <div className="App">
      <h1>Hello</h1>
      <ColoredButton />
    </div>
  )
}
```
## Renderizando as props

Um padrão comum usado para compartilhar state entre componentes é usar o `props.children`.

Dentro de um componente JSX, você pode renderizar `{this.props.children}` que injeta automaticamente qualquer JSX passado no componente pai como `children`:

```
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      /*...*/
    }
  }
  
  render() {
    return <div>{this.props.children}</div>
  }
}

const Children1 = () => {}

const Children2 = () => {}

const App = () => (
  <Parent>
    <Children1 />
    <Children2 />
  </Parent>
)
```

No entanto, há um problema aqui: o state do componente pai não pode ser acessado pelos filhos.

Para poder compartilhar o state, você precisa usar um render prop component, em vez de passar componentes como filhos do componente pai, passa uma função que você executa em `{this.props.children ()}`. A função pode aceitar argumentos:

```
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: 'Flavio' }
  }
  
  render() {
    return <div>{this.props.children(this.state.name)}</div>
  }
}

const Children1 = props => {
  return <p>{props.name}</p>
}

const App = () => <Parent>{name => <Children1 name={name} />}</Parent>
```
Em vez de usar a props do filho, que tem um valor muito específico, você pode usar qualquer props e, portanto, pode usar esse padrão várias vezes no mesmo componente:

```
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: 'Flavio', age: 35 }
  }
  
  render() {
    return (
      <div>
        <p>Test</p>
        {this.props.someprop1(this.state.name)}
        {this.props.someprop2(this.state.age)}
      </div>
    )
  }
}

const Children1 = props => {
  return <p>{props.name}</p>
}

const Children2 = props => {
  return <p>{props.age}</p>
}

const App = () => (
  <Parent
    someprop1={name => <Children1 name={name} />}
    someprop2={age => <Children2 age={age} />}
  />
)

ReactDOM.render(<App />, document.getElementById('app'))
```

## Hooks

Hooks é um recurso que será introduzido no React 16.7 e mudará a forma como escrevemos aplicativos do React no futuro.

Antes da aparição de Hooks, algumas coisas importantes nos componentes eram possíveis apenas usando componentes de classe: ter seu próprio state e usar lifecycle events. Os componentes funcionais, mais leves e mais flexíveis, eram limitados em funcionalidade.

Os Hooks permitem que os componentes funcionais tenham state e também respondam aos lifecycle events, e meio que tornam os componentes da classe obsoletos. Eles também permitem que os componentes funcionais tenham uma boa maneira de lidar com eventos.

### Acessando o state

Usando a API <kbg>useState()</kbg>, você pode criar uma nova variável de estado e ter uma maneira de alterá-la. <kbg>useState()</kbg> aceita o valor inicial do item de state e retorna uma matriz que contém a variável de state e a função que você chama para alterar o state. Como ele retorna uma matriz, usamos a desestruturação da matriz para acessar cada item individual, assim: `const [count, setCount] = useState(0)`

Aqui está um exemplo prático:

```
import { useState } from 'react'

const Counter = () => {
  const [count, setCount] = useState(0)
  
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}

ReactDOM.render(<Counter />, document.getElementById('app'))
```

Você pode adicionar quantas chamadas useState() quiser, para criar quantas variáveis de state desejar. Apenas certifique-se de chamá-lo no nível superior de um componente (não em um if ou em qualquer outro bloco).

### Acessando o lifecycle(ciclo de vida) hooks

Outro recurso muito importante do Hooks é permitir que os componentes de função tenham acesso aos lifecycle hooks.

Usando componentes de classe, você pode registrar uma função nos eventos componentDidMount, componentWillUnmount e componentDidUpdate, e esses servirão a muitos casos de uso, da inicialização de variáveis às chamadas de API.

Ganchos fornecem a API `useEffect()`. A chamada aceita uma função como argumento.

A função é executada quando o componente é renderizado pela primeira vez e em cada nova renderização/atualização subsequente. O React atualiza primeiro a DOM e depois chama qualquer função passada para o `useEffect()`. Tudo isso sem bloquear a renderização da interface do usuário, ao contrário do antigo componentDidMount e componentDidUpdate, que faz com que nossos aplicativos pareçam mais rápidos.

Exemplo: 

```
const { useEffect, useState } = React

const CounterWithNameAndSideEffect = () => {
  const [count, setCount] = useState(0)
  const [name, setName] = useState('Flavio')
  
  useEffect(() => {
    console.log(`Hi ${name} you clicked ${count} times`)
  })
  
  return (
    <div>
      <p>
        Hi {name} you clicked {count} times
      </p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
      <button onClick={() => setName(name === 'Flavio' ? 'Roger' : 'Flavio')}>
        Change name
      </button>
    </div>
  )
}

ReactDOM.render(
  <CounterWithNameAndSideEffect />,
  document.getElementById('app')
)
```
O mesmo trabalho do `componentWillUnmount` pode ser alcançado retornando opcionalmente uma função do nosso parâmetro do <kbg>useEffect()</kbg>:

```
useEffect(() => {
  console.log(`Hi ${name} you clicked ${count} times`)
  return () => {
    console.log(`Unmounted`)
  }
})
```


`useEffect()` pode ser chamado várias vezes, o que é bom para separar a lógica não relacionada (algo que afeta o lifecycle do componente de classe).

Como as funções `useEffect()` são executadas em cada re-renderização/atualização subsequente, podemos dizer ao React para pular uma execução ao adicionarmos um segundo parâmetro, que é uma matriz que contém uma lista de variáveis de state a serem observadas. React só executará novamente o efeito colateral se um dos itens desta matriz for alterado.
```
useEffect(
  () => {
    console.log(`Hi ${name} you clicked ${count} times`)
  },
  [name, count]
)
```
Da mesma forma, você pode dizer ao React para executar apenas o efeito colateral uma vez (no tempo de montagem), passando uma matriz vazia:

```
useEffect(() => {
  console.log(`Component mounted`)
}, [])
```

### Manipulando eventos em componentes funcionais

Antes do Hooks, você usou componentes de classe ou passou um manipulador de eventos usando props.

Agora nós podemos usar a API <kbg>useCallback()</kbg>:
```
const Button = () => {
  const handleClick = useCallback(() => {
    //...do something
  })
  return <button onClick={handleClick} />
}
```

Qualquer parâmetro usado dentro da função deve ser passado por um segundo parâmetro da `useCallback()`, em uma matriz:

```
const Button = () => {
  let name = '' //... add logic
  const handleClick = useCallback(
    () => {
      //...do something
    },
    [name]
  )
  return <button onClick={handleClick} />
}
```

### Ative a comunicação entre componentes usando hooks personalizados

A capacidade de escrever seus próprios hooks é o recurso que altera significativamente a maneira como você escreve os aplicativos React no futuro.

Usando hooks personalizados, você tem mais uma maneira de compartilhar state e lógica entre componentes, adicionando uma melhoria significativa nos padrões de renderização das props e componentes de ordem superior. O que ainda é ótimo, mas agora com hooks personalizados têm menos relevância em muitos casos de uso.

Como você cria um hook personalizado?

Um hook é apenas uma função que começa convencionalmente com o <kbg>use</kbg>. Ele pode aceitar um número arbitrário de argumentos e retornar o que quiser.

Exemplos:
```
const useGetData() {
  //...
  return data
}
```
ou

```
const useGetUser(username) {
  //...const user = fetch(...)
  //...const userData = ...
  return [user, userData]
}
```

Nos seus próprios componentes, você pode usar o hooks assim:
```
const MyComponent = () => {
  const data = useGetData()
  const [user, userData] = useGetUser('flavio')
  //...
}
```

Quando exatamente adicionar hooks em vez de funções regulares deve ser determinado com base em cada caso, e somente a experiência informa.


## Divisão de código (code splitting)

Os aplicativos JavaScript modernos podem ser bastante grandes em termos de tamanho de pacote. Você não deseja que seus usuários tenham que baixar um pacote JavaScript de 1MB (seu código e as bibliotecas que você usa) apenas para carregar a primeira página, certo? Mas é o que acontece por padrão quando você envia um Web App moderno construído com o bundle Webpack.

Esse bundle contém um código que talvez nunca seja executado porque o usuário para na página de login e nunca vê o restante do seu aplicativo.

A divisão de código é a prática de carregar apenas o JavaScript necessário no momento em que você precisar.

Isso melhora:

- a performance do seu app
- o impacto na memório, e também a bateria usada em dispositivos móveis
- o tamanho do download em KB

O React 16.6.0, lançado em outubro de 2018, introduziu uma maneira de executar a divisão de código que deve substituir todas as ferramentas ou bibliotecas usadas anteriormente: <kbg>React.lazy</kbg> e <kbg>Suspense</kbg>.

<kbg>React.lazy</kbg> e <kbg>Suspense</kbg> formam a maneira perfeita de carregar 'preguiçosamente' uma dependência e carregá-la apenas quando necessário.

Vamos começar com React.lazy. Você o usa para importar qualquer componente:
```
import React from 'react'

const TodoList = React.lazy(() => import('./TodoList'))

export default () => {
  return (
    <div>
      <TodoList />
    </div>
  )
}
```
o componente <kbg>TodoList</kbg> será adicionado dinamicamente à saída assim que estiver disponível. O Webpack criará um pacote separado para ele e cuidará de carregá-lo quando necessário.

<kbg>Suspense</kbg> é um componente que você pode usar para quebrar qualquer componente carregado lentamente (que utilizou o React.lazy):

```
import React from 'react'

const TodoList = React.lazy(() => import('./TodoList'))

export default () => {
  return (
    <div>
      <React.Suspense>
        <TodoList />
      </React.Suspense>
    </div>
  )
}
```
Ele cuida da manipulação da saída enquanto o lazy component é buscado e renderizado.

Use a props fallback para gerar um saída de JSX ou componente:

```
...
      <React.Suspense fallback={<p>Please wait</p>}>
        <TodoList />
      </React.Suspense>
...
```

Tudo isso funciona muito bem com o React Router

```
import React from 'react'
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom'

const TodoList = React.lazy(() => import('./routes/TodoList'))
const NewTodo = React.lazy(() => import('./routes/NewTodo'))

const App = () => (
  <Router>
    <React.Suspense fallback={<p>Please wait</p>}>
      <Switch>
        <Route exact path="/" component={TodoList} />
        <Route path="/new" component={NewTodo} />
      </Switch>
    </React.Suspense>
  </Router>
)
```
