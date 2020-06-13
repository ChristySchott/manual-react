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

## Next.js

Trabalhar em um aplicativo JavaScript desenvolvido pelo React é incrível, mas ainda assim existem alguns problemas relacionados à renderização de todo o conteúdo no lado do cliente.

Primeiro, a página leva mais tempo para se tornar visível para o usuário, porque antes do carregamento do conteúdo, todo o JavaScript deve ser carregado e seu aplicativo precisa ser executado para determinar o que mostrar na página.

Segundo, se você estiver criando um site disponível publicamente, terá um problema de SEO de conteúdo. Os mecanismos de pesquisa estão melhorando a execução e a indexação de aplicativos JavaScript, mas é muito melhor podermos enviar conteúdo a eles, em vez de deixá-los descobrir.

A solução para esses dois problemas é a renderização do servidor(server rendering), também chamada de pré-renderização estática.

O Next.js é um framework do React para fazer tudo isso de uma maneira muito simples, mas não se limita a isso. Ele é anunciado por seus criadores como uma cadeia de ferramentas de comando único e configuração zero para aplicativos React.

Ele fornece uma estrutura comum que permite a fácil criação do frontend de um aplicativo React e o processamento transparente do lado do servidor para você.

Aqui está uma lista dos principais recursos do Next.js.

- `Hot Code Reloading`: Next.js recarrega a página quando detecta qualquer alteração salva no disco.
- `Automatic Routing`: qualquer URL é mapeado para o sistema de arquivos e você não precisa de nenhuma configuração (é claro que você tem opções de personalização).
- `Single File Components`: usando o styled-jsx, completamente integrado, é trivial adicionar estilos com escopo ao componente.
- `Server Rendering`: você pode (opcionalmente) renderizar os componentes do React no lado do servidor, antes de enviar o HTML para o cliente.
- `Ecosystem Compatibility`: Next.js roda bem com o restante do ecossistema JavaScript, Node e React.
- `Automatic Code Splitting`: as páginas são renderizadas apenas com as bibliotecas e JavaScript de que precisam, e não mais.
- `Dynamic Components`: você pode importar módulos JavaScript e React Components dinamicamente.
- `Static Exports`: usando o comando `next export`, o Next.js permite exportar um site totalmente estático do seu aplicativo.


### Instalação

O Next.js suporta todas as principais plataformas: Linux, macOS, Windows.

Um projeto Next.js é iniciado facilmente com o npm:
```
npm install next react react-dom
```

ou com o yarn:
```
yarn add next react react-dom
```

### Iniciando 

Crie um `package.json` com este conteúdo:
```
{
  "scripts": {
    "dev": "next"
  }
}
```

Agora, se você executar esse comando:
```
npm run dev
```

o script gerará um erro reclamando por não encontrar o arquivo `pages`. Essa é a única coisa que o Next.js requer para executar.

Crie um arquivo `pages` vazio e execute o comando novamente, e o Next.js iniciará um servidor no localhost: 3000.

Se você acessar esse URL agora, será recebido por uma página 404 amigável, com um design bom e limpo

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/wBBqzsveZC9evvtqiPb6yrFav9V5UjExd0HE" alt="404 not found page" /> </h1>

O Next.js também lida com outros tipos de erro, como o erro `500`, por exemplo.

### Criando uma página

Na pasta `pages`, crie um arquivo `index.js` com um simples componente funcional do React:
```
export default () => (
  <div>
    <p>Hello World!</p>
  </div>
)
```

Se você visitar localhost: 3000, esse componente será renderizado automaticamente.

Por que isso é tão simples?

O Next.js usa uma estrutura de páginas declarativa, baseada na estrutura do sistema de arquivos.

Simplificando, as páginas estão dentro de uma pasta de páginas e o URL da página é determinado pelo nome do arquivo da página. O sistema de arquivos é a API das páginas.

### Renderização no lado do servidor

Abra a fonte da página, `View -> Developer -> View Source` com o Chrome.

Como você pode ver, o HTML gerado pelo componente é enviado diretamente na fonte da página. Não é renderizado no lado do cliente, mas é renderizado no servidor.

A equipe do Next.js. queria criar uma experiência de desenvolvedor para páginas renderizadas pelo servidor semelhantes à que você obtém ao criar um projeto PHP básico, onde você simplesmente solta arquivos PHP e os chama, e eles aparecem como páginas. Internamente, é claro que tudo é muito diferente, mas a facilidade de uso é clara.

### Adicionando uma segunda página

Vamos criar outra página, em `pages/contact.js`
```
export default () => (
  <div>
    <p>
      <a href="mailto:my@email.com">Contact us!</a>
    </p>
  </div>
)
```

Se você direcionar o navegador para `localhost:3000/contact`, esta página será renderizada, novamente, pelo servidor.

### Renderização no lado do cliente

A renderização do servidor é muito conveniente no carregamento da primeira página, por todos os motivos citados acima, mas quando se trata de navegar no site, a renderização do lado do cliente é essencial para acelerar o carregamento da página e melhorar a experiência do usuário.

O Next.js fornece um componente `Link` que você pode usar para criar links. Tente vincular as duas páginas acima.

Altere `index.js` para este código:

```
import Link from 'next/link'

export default () => (
  <div>
    <p>Hello World!</p>
    <Link href="/contact">
      <a>Contact me!</a>
    </Link>
  </div>
)
```
Agora volte ao navegador e tente este link. Como você pode ver, a página Contato é carregada imediatamente, sem uma atualização da página.

Essa navegação do lado do cliente está funcionando corretamente, com suporte completo à History API, o que significa que o botão voltar dos usuários não será interrompido.

Se você clicar com o botão direito do mouse no link, a mesma página de Contato será aberta em uma nova guia, agora renderizada pelo servidor.

### Páginas dinâmicas

Um bom caso de uso para o Next.js. é um blog, pois é algo que todos os desenvolvedores sabem como funciona e é um bom exemplo de como lidar com páginas dinâmicas.

Uma página dinâmica é uma página que não possui conteúdo fixo, mas exibe alguns dados com base em alguns parâmetros.

Altere `index.js` para

```
import Link from 'next/link'

const Post = props => (
  <li>
    <Link href={`/post?title=${props.title}`}>
      <a>{props.title}</a>
    </Link>
  </li>
)

export default () => (
  <div>
    <h2>My blog</h2>
    <ul>
      <li>
        <Post title="Yet another post" />
        <Post title="Second post" />
        <Post title="Hello, world!" />
      </li>
    </ul>
  </div>
)
```

Isso criará uma série de postagens e preencherá o parâmetro de consulta de título com o título da postagem:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/nEBXVSebNz6KzUWgNg62w-clo2vL7tnLIYpl"/> </h1>

Agora crie um arquivo `post.js` na pasta `pages` e adicione:

```
export default props => <h1>{props.url.query.title}</h1>
```

Agora, clicar em uma única postagem renderizará o título da postagem em uma tag `h1`:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/urgIpOydqbjE4i9nyELblMonOjrK0Plrn3OJ"/> </h1>

Você pode usar URLs limpos sem parâmetros de consulta. O componente de link Next.js nos ajuda ao aceitar um atributo `as`, que você pode usar para passar um slug:

```
import Link from 'next/link'

const Post = props => (
  <li>
    <Link as={`/${props.slug}`} href={`/post?title=${props.title}`}>
      <a>{props.title}</a>
    </Link>
  </li>
)

export default () => (
  <div>
    <h2>My blog</h2>
    <ul>
      <li>
        <Post slug="yet-another-post" title="Yet another post" />
        <Post slug="second-post" title="Second post" />
        <Post slug="hello-world" title="Hello, world!" />
      </li>
    </ul>
  </div>
)
```


### CSS-in-JS


O Next.js por padrão fornece suporte para styled-jsx, que é uma solução CSS-in-JS fornecida pela mesma equipe de desenvolvimento, mas você pode usar a biblioteca que preferir, como Styled Components.

Exemplo:

```
export default () => (
  <div>
    <p>
      <a href="mailto:my@email.com">Contact us!</a>
    </p>
    <style jsx>{`
      p {
        font-family: 'Courier New';
      }
      a {
        text-decoration: none;
        color: black;
      }
      a:hover {
        opacity: 0.8;
      }
    `}</style>
  </div>
)
```

Os estilos são 'escopados' ao componente, mas você também pode editar estilos globalmente, adicionando `global` ao estilo do elemento:

```
export default () => (
  <div>
    <p>
      <a href="mailto:my@email.com">Contact us!</a>
    </p>
    <style jsx global>{`
      body {
        font-family: 'Benton Sans', 'Helvetica Neue';
        margin: 2em;
      }
      h2 {
        font-style: italic;
        color: #373fff;
      }
    `}</style>
  </div>
)
```

### Exportando um site estático

Uma aplicação com Next.js pode ser facilmente exportada como um site estático, que pode receber um deploy em um dos sites de hosts mais rápidos, como `Netlify` ou `Firebase Hosting`, sem a necessidade de configurar um ambiente no Node.

O processo requer que você declare as URLs que compõem o site, mas é um processo simples.

### Deploy 

É fácil criar uma cópia pronta para produção do aplicativo, sem mapas de origem ou outras ferramentas de desenvolvimento que não são necessárias na compilação final.

No início deste tutorial, você criou um arquivo `package.json` com este conteúdo:

```
{
  "scripts": {
    "dev": "next"
  }
}
```
which was the way to start up a development server using npm run dev.

que é a maneira de startar um servidor de desenvolvimento usando `npm run dev`.

Agora basta adicionar o seguinte conteúdo ao `package.json`:

```
{
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start"
  }
}
```

e prepare seu app rodando `npm run build` e `npm run start`.

### Now

A companhia por trás do Next.js provém um serviço muito bom de hosting para aplicação em Node.js, chamado `Now`.

É claro que eles integram os dois produtos para que você possa implantar aplicativos `Next.js` sem muitos problemas, depois de instalar o `Now`, executando o comando `now` na pasta do aplicativo.

Nos bastidores do `Now`, configure um servidor para você e você não precisará se preocupar com nada, apenas aguardar o URL do aplicativo estar pronto.

### Zones

Você pode configurar várias instâncias do Next.js. para ouvir diferentes URLs. No entanto, o aplicativo para um usuário externo parecerá estar sendo desenvolvido por um único servidor:

https://github.com/zeit/next.js/#multi-zones

### Plugins 

Next.js tem uma lista de plugins em https://github.com/zeit/next-plugins

## Gatsby

Gatsby é uma plataforma para a criação de aplicativos e sites usando o React.

É uma das ferramentas que permitem a criação de um conjunto de tecnologias e práticas conhecidas coletivamente como JAMstack.

Gatsby é uma das coisas mais legais na área do Desenvolvimento Frontend no momento. Por quê? Eu acho que as razões são:

- a explosão da abordagem JAMstack na criação de aplicativos e sites
- a rápida adoção da tecnologia Progressive Web Apps no setor, que é um dos principais recursos do Gatsby
- é construído no React e no GraphQL, que são duas tecnologias muito populares e em ascensão
- é realmente poderoso
- é rápido
- a documentação é ótima
- o efeito de rede (as pessoas o usam, criam sites, fazem tutoriais, as pessoas sabem mais sobre isso, criando um ciclo)
- tudo é JavaScript (não é necessário aprender uma nova linguagem de modelos)
- esconde a complexidade, no começo, mas nos permite acessar todas as etapas para personalizar

Todos esses são ótimos pontos, e Gatsby definitivamente vale a pena dar uma olhada.

### Como o Gatsby funciona?

Com o Gatsby, seus aplicativos são criados usando componentes React.

O conteúdo que você renderiza em um site geralmente é escrito usando o Markdown, mas você pode usar qualquer tipo de fonte de dados, como um headless CMS ou um serviço da Web como o Contentful.

O Gatsby cria o site e é compilado em HTML estático, que pode ser implantado em qualquer servidor da Web que você desejar, como Netlify, AWS S3, GitHub Pages, provedores de hospedagem regulares, PAAS e muito mais. Tudo o que você precisa é de um local que sirva páginas HTTP simples e seus ativos ao cliente.

Mencionei Progressive Web Apps na lista. O Gatsby gera automaticamente seu site como um PWA, com um service worker que acelera o carregamento da página e o cache de recursos.

Você pode aprimorar a funcionalidade do Gatsby através de plugins.
