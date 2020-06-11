<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 8:</strong> O ECOSSISTEMA DO REACT </h2>

O ecossistema ao redor do React é enorme. Aqui, apresento quatro dos projetos mais populares baseados em React: React Router, Redux, Next.js, Gatsby.

## React Router

O React Router é a biblioteca de roteamento do React e é um dos projetos mais populares criados no React.

O React em sua essência é uma biblioteca muito simples e não determina nada sobre o roteamento.

O roteamento em um Single Page Aplication é a maneira de introduzir alguns recursos para navegar no aplicativo por meio de links, que são esperados em aplicativos Web normais:

- O navegador deve alterar a URL quando você navega para uma tela diferente
- A vinculação profunda deve funcionar: se você apontar o navegador para uma URL, o aplicativo deverá reconstruir a mesma exibição que foi apresentada quando a URL foi gerada.
- O botão voltar (e avançar) do navegador deve funcionar como o esperado.

O roteamento vincula a navegação do aplicativo aos recursos de navegação oferecidos pelo navegador: a barra de endereço e os botões de navegação.

O React Router oferece uma maneira de escrever seu código, de modo que ele mostre determinados componentes do seu aplicativo somente se a rota corresponder ao que você definir.

### Instalação

Com npm:

```
npm install react-router-dom
```

Com yarn:
```
yarn add react-router-dom
```

### Tipos de rotas

React Router fornece dois tipos de routas:

- `BrowserRouter`
- `HashRouter`

Um cria URLs clássicos, o outro cria URLs com o hash:

```
https://application.com/dashboard   /* BrowserRouter */
https://application.com/#/dashboard /*  HashRouter  */
```

Qual deles usar é ditado principalmente pelos navegadores que você precisa oferecer suporte. O `BrowserRouter` usa a `History API`, que é relativamente recente e não é suportada no IE9 e abaixo. Se você não precisa se preocupar com navegadores antigos, é a escolha recomendada.

### Componentes

Os 3 componentes que você mais irá interagir quando trabalhar com o React Router são:

- `BrowserRouter`, referenciado como `Router`
- `Link`
- `Route`

`BrowserRouter` envolve todos os seus componentes do Router

`Link` é - como você pode imaginar - usada para gerar links para suas rotas

`Route` é responsável por mostrar - ou esconder - os componentes que ele contém

### Browser Router

Aqui está um exemplo simples do componente `BrowserRouter`. Você o importa do `react-router-dom` e o usa para envolver todo o seu aplicativo:
```
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router } from 'react-router-dom'

ReactDOM.render(
  <Router>
      <div>
        <!-- -->
      </div>
  </Router>,
  document.getElementById('app')
)
```

Um componente BrowserRouter pode ter apenas um elemento filho, portanto, agrupamos tudo o que vamos adicionar em uma `div`.

### Link

O componente Link é usado para acionar novas rotas. Você o importa do react-router-dom e pode adicionar os componentes `Link` para apontar para rotas diferentes, usando o atributo `to`:
```
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router, Link } from 'react-router-dom'

ReactDOM.render(
  <Router>
      <div>
        <aside>
          <Link to={`/dashboard`}>Dashboard</Link>
          <Link to={`/about`}>About</Link>
        </aside>
        <!-- -->
      </div>
  </Router>,
  document.getElementById('app')
)
```

### Route

Agora, vamos adicionar o componente Route no snippet acima para fazer com que as coisas funcionem como queremos:

```
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router, Link, Route } from 'react-router-dom'

const Dashboard = () => (
  <div>
    <h2>Dashboard</h2>
    ...
  </div>
)

const About = () => (
  <div>
    <h2>About</h2>
    ...
  </div>
)

ReactDOM.render(
  <Router>
    <div>
      <aside>
        <Link to={`/`}>Dashboard</Link>
        <Link to={`/about`}>About</Link>
      </aside>
      
      <main>
        <Route exact path="/" component={Dashboard} />
        <Route path="/about" component={About} />
      </main>
    </div>
  </Router>,
  document.getElementById('app')
)
```

Quando a rota corresponde a `/`, o aplicativo mostra o componente `Dashboard`.

Quando a rota é alterada, clicando no link "Sobre" para `/about`, o componente `Dashboard` é removido e o componente `About` é inserido na DOM.

Observe o atributo `exact`. Sem isso, `path = "/"` também corresponderia a `/ about`, já que `/` está contido na rota.

### Definindo vários caminhos

Você pode fazer com que uma rota responda a vários caminhos simplesmente usando uma expressão regular, porque o caminho pode ser uma sequência de expressões regulares:

```
<Route path="/(about|who)/" component={Dashboard} />
```

### Inline Rendering (Renderização em linha)

Em vez de especificar uma propriedade `component` no Route, você pode usar o `render`

```
<Route
  path="/(about|who)/"
  render={() => (
    <div>
      <h2>About</h2>
      ...
    </div>
  )}
/>
```

### Definindo parâmetros dinâmicos para as rotas

Você já aprendeu a usar rotas estáticas como

```
const Posts = () => (
  <div>
    <h2>Posts</h2>
    ...
  </div>
)

//...

<Route exact path="/posts" component={Posts} />
```

Veja como lidar com rotas dinâmicas:

```
const Post = ({match}) => (
  <div>
    <h2>Post #{match.params.id}</h2>
    ...
  </div>
)

//...

<Route exact path="/post/:id" component={Post} />
```

No seu componente Route, você pode encontrar os parâmetros dinâmicos em `match.params`.

`match` também está disponível em rotas renderizadas em linha, e isso é especialmente útil nesse caso, porque podemos usar o parâmetro id para pesquisar os dados de postagem em nossa fonte de dados antes de renderizar `Post`:

```
const posts = [
  { id: 1, title: 'First', content: 'Hello world!' },
  { id: 2, title: 'Second', content: 'Hello again!' }
]

const Post = ({post}) => (
  <div>
    <h2>{post.title}</h2>
    {post.content}
  </div>
)

//...

<Route exact path="/post/:id" render={({match}) => (
  <Post post={posts.find(p => p.id === match.params.id)} />
)} />
```

## Redux

> (Dica do tradutor(hehe): se não entenderem muito bem o Redux a partir desse livro, recomendo o blog da Rocketseat, só clicar [aqui](https://blog.rocketseat.com.br/redux-o-passo-a-passo/))

O Redux é um gerenciador de estado que geralmente é usado junto com o React, mas não está vinculado a essa biblioteca - ele também pode ser usado com outras tecnologias.

O Redux é uma maneira de gerenciar o estado de um aplicativo e movê-lo para um armazenamento global externo.

Existem alguns conceitos a serem compreendidos, mas uma vez que você o faça, o Redux é uma abordagem muito simples para o problema.

O Redux é muito popular nas aplicações React, mas não é exclusivo do React: existem ligações para praticamente qualquer estrutura popular. Dito isso, darei alguns exemplos usando o React, pois é seu principal caso de uso.

### Quando você deve usar o Redux?

O Redux é ideal para aplicativos de médio a grande porte, e você deve usá-lo apenas quando tiver problemas para gerenciar o estado com o gerenciamento padrão do React ou com a outra biblioteca usada.

Aplicativos simples não devem precisar dele (e não há nada de errado com aplicativos simples).

### Immutable State Tree (algo como Árvore de estado imutável)

No Redux, todo o estado do aplicativo é representado por um objeto JavaScript, chamado State ou State Tree.

Chamamos de Árvore de Estado Imutável porque é somente leitura: não pode ser alterada diretamente.

Só pode ser alterado enviando uma `Action`.

### Actions

Uma `Action` é um objeto JavaScript que descreve uma alteração de maneira mínima (com apenas as informações necessárias):

```
{
  type: 'CLICKED_SIDEBAR'
}

// exemplos com mais dados
{
  type: 'SELECTED_USER',
  userId: 232
}
```

O único requisito de uma `action` é ter uma propriedade `type`, cujo valor geralmente é uma string.

### `Types` devem ser constantes

Em uma aplicação simples o `type` pode ser definido como uma string, como eu fiz no exemplo anterior.

Quando a aplicação cresce, é melhor usar constantes:
```
const ADD_ITEM = 'ADD_ITEM'
const action = { type: ADD_ITEM, title: 'Third item' }
```

e separar ações em seus próprios arquivos e importá-los

```
import { ADD_ITEM, REMOVE_ITEM } from './actions'
```

### Actions Creators

As `Actions Creators` são funções que criam `actions`.

```
function addItem(t) {
  return {
    type: ADD_ITEM,
    title: t
  }
}
```

Você normalmente executa `actions creators` em combinação com o acionamento do `dispatcher`:
```
dispatch(addItem('Milk'))
```
ou definindo uma função `action dispatcher`:

```
const dispatchAddItem = i => dispatch(addItem(i))
dispatchAddItem('Milk')
```

### Reducers

Quando uma `action` é acionada, algo deve acontecer, o estado do aplicativo deve mudar.

Este é o trabalho dos `reducers`.

Um `reducer` é uma função pura que calcula a próxima Árvore de Estado com base na Árvore de Estado anterior e na `action dispatch()`.

```
;(currentState, action) => newState
```

Uma função pura recebe uma entrada e retorna uma saída, tudo isso sem alterar a entrada ou qualquer outra coisa. Assim, um `reducer` retorna um objeto de árvore de estado completamente novo que substitui o anterior.

### O que um reducer não deve fazer

Um `reducer` deve ser uma função pura, portanto deve:

- nunca mudar seus argumentos
- nunca mudar o estado, mas sim criar um novo com `Object.assign({}, ...)`
- nunca gerar efeitos colaterais (nenhuma chamada de API muda nada)
- nunca chamar funções não puras, funções que alteram sua saída com base em outros fatores além da entrada (por exemplo, `Date.now()` ou `Math.random()`)

### Multiplos Reducers

Como o estado de um aplicativo complexo pode ser realmente amplo, não há um único `reducer`, mas muitos `reducers` para qualquer tipo de ação.

### Uma simulação de um reducer

Em essência, o Redux pode ser simplificado com este modelo simples:

#### O state (estado)

```
{
  list: [
    { title: "Primeiro item" },
    { title: "Segundo item" },
  ],
  title: 'lista de compras'
}
```

#### Uma lista de `actions`

```
{ type: 'ADD_ITEM', title: 'Terceiro items' }
{ type: 'REMOVE_ITEM', index: 1 }
{ type: 'CHANGE_LIST_TITLE', title: 'Lista de viagens' }
```

#### Um reducer para cada parte do state
```
const title = (state = '', action) => {
    if (action.type === 'CHANGE_LIST_TITLE') {
      return action.title
    } else {
      return state
    }
}

const list = (state = [], action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      return state.concat([{ title: action.title }])
    case 'REMOVE_ITEM':
      return state.map((item, index) =>
        action.index === index
          ? { title: item.title }
          : item
    default:
      return state
  }
}
```

#### Um reducer para todo o state

```
const listManager = (state = {}, action) => {
  return {
    title: title(state.title, action),
    list: list(state.list, action)
  }
}
```

### O Store

O `store` é um objeto que:

- armazena o state do seu app
- expõe o state via getState()
- nos permite atualizar o state via dispatch()

Um `store` é único no seu aplicativo.

Aqui está como um `store` para o aplicativo listManager é criado:

```
import { createStore } from 'redux'
import listManager from './reducers'
let store = createStore(listManager)
```

### Posso inicializar o `store` com dados do servidor?

Claro, apenas passe um state inicial:

```
let store = createStore(listManager, preexistingState)
```

### Pegando o state

```
store.getState()
```

### Atualize o state
```
store.dispatch(addItem('Something'))
```

### 'Ouça' mudanças no state

```
const unsubscribe = store.subscribe(() =>
  const newState = store.getState()
)

unsubscribe()
```

### Fluxo de dados

O fluxo de dados no Redux é sempre unidirecional.

Você chama o `dispatch()` no `Store`, passando uma `Action`.

O `store` se encarrega de enviar a `action` ao Reducer, gerando o proximo `state`.

O `store` atualiza o state e avisa todos os `listeners`.
