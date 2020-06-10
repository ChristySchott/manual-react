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
