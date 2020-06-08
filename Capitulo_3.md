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
