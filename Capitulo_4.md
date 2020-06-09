<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 4:</strong> EXERCÍCIOS PRÁTICOS </h2>

2 aplicações bem simples para explicar alguns dos conceitos introduzidos até aqui.

## Construindo um contador simples

Neste pequeno exemplo, criaremos um exemplo muito simples de contador no React, aplicando muitos dos conceitos e teoria descritos anteriormente.

Vamos usar o Codepen para isso. Começamos dando um fork no [React template pen](https://codepen.io/flaviocopes/pen/VqeaxB).

> No Codepen, não precisamos importar o React e o ReactDOM, pois eles já foram adicionados ao escopo.

Mostramos a contagem em uma div e adicionamos alguns botões para incrementar essa contagem:

```
const Button = ({ increment }) => {
  return <button>+{increment}</button>
}

const App = () => {
  let count = 0
  
  return (
    <div>
      <Button increment={1} />
      <Button increment={10} />
      <Button increment={100} />
      <Button increment={1000} />
      <span>{count}</span>
    </div>
  )
}

ReactDOM.render(<App />, document.getElementById('app'))
```

Vamos adicionar a funcionalidade que nos permite alterar a contagem clicando nos botões, adicionando uma props <kbg>onClickFunction</kbg>:

```
const Button = ({ increment, onClickFunction }) => {
  const handleClick = () => {
    onClickFunction(increment)
  }
  return <button onClick={handleClick}>+{increment}</button>
}

const App = () => {
  let count = 0
  
  const incrementCount = increment => {
    //TODO
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

ReactDOM.render(<App />, document.getElementById('app'))
```

Aqui, todo elemento <kbg>Button</kbg> possui 2 objetos: <kbg>increment</kbg> e <kbg>onClickFunction</kbg>. Criamos 4 botões diferentes, com 4 valores de incremento: 1, 10, 100, 1000.

Quando o botão no componente <kbg>Button</kbg> é clicado, a função <kbg>incrementCount</kbg> é chamada.

Esta função deve incrementar a contagem local. Como podemos fazer isso? Podemos usar hooks:

```
const { useState } = React

const Button = ({ increment, onClickFunction }) => {
  const handleClick = () => {
    onClickFunction(increment)
  }
  return <button onClick={handleClick}>+{increment}</button>
}

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

ReactDOM.render(<App />, document.getElementById('app'))
```

<kbg>useState()</kbg> inicializa a variável <kbg>count</kbg> em 0 e fornece o método <kbg>setCount()</kbg> para atualizar seu valor.

Utilizamos ambos na implementação do método <kbg>incrementCount()</kbg>, que chama <kbg>setCount()</kbg> atualizando o valor para o valor existente de <kbg>count</kbg>, mais o incremento passado por cada componente <kbg>Button</kbg>.

## Buscar e exibir informações de usuários do GitHub via API

Exemplo muito simples de um formulário que aceita um nome de usuário do GitHub e, após receber um evento de envio, solicita as informações do usuário à API do GitHub e as imprime.

Este código cria um componente Card, que é reutilizável. Quando você insere um nome no campo de entrada gerenciado pelo componente Formulário, esse nome é vinculado ao seu state.

Quando o Adicionar cartão é pressionado, o formulário de entrada é limpo, deixando o state do userName vazio.

O exemplo usa, além de React, a biblioteca <kbg>Axios</kbg>. É uma biblioteca que, além de muito útil, é leve para lidar com solicitações de rede. Instale localmente usando o <kbg>npm install axios</kbg>.

Começamos criando o componente Card, que exibirá nossa imagem e detalhes conforme coletados no GitHub. Ele obtém seus dados por meio de props, usando

- <kbg>props.avatar_url</kbg> o avatar do usuário
- <kbg>props.name</kbg> o nome do usuário
- <kbg>props.blog</kbg> a url do website do usuário

```
const Card = props => {
  return (
    <div style={{ margin: '1em' }}>
      <img alt="avatar" style={{ width: '70px' }} src={props.avatar_url} />
      <div>
        <div style={{ fontWeight: 'bold' }}>{props.name}</div>
        <div>{props.blog}</div>
      </div>
    </div>
  )
}
```

Criamos uma lista desses componentes, que serão passados por um componente pai para CardList, que simplesmente itera usando map() e gera uma lista de cartões:

```
const CardList = props => (
  <div>
    {props.cards.map(card => (
      <Card {...card} />
    ))}
  </div>
)
```

O componente pai é o App, que armazena a matriz de cartões em seu próprio state e a gerencia usando o <kbg>useState()</kbg>:
```
const App = () => {
  const [cards, setCards] = useState([])
  
  return (
    <div>
      <CardList cards={cards} />
    </div>
  )
}
```
Legal! Agora precisamos ter uma maneira de solicitar ao GitHub os detalhes de um único nome de usuário. Faremos isso usando um componente de formulário, onde gerenciamos nosso próprio state(username) e solicitamos ao GitHub informações sobre um usuário usando suas APIs públicas, via Axios:

```
const Form = props => {
  const [username, setUsername] = useState('')
  
  handleSubmit = event => {
    event.preventDefault()
    
    axios.get(`https://api.github.com/users/${username}`).then(resp => {
      props.onSubmit(resp.data)
      setUsername('')
    })
  }
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={username}
        onChange={event => setUsername(event.target.value)}
        placeholder="GitHub username"
        required
      />
      <button type="submit">Add card</button>
    </form>
  )
}
```
Quando o formulário é enviado, chamamos o evento <kbg>handleSubmit</kbg> e, após a chamada de rede, chamamos <kbg>props.onSubmit</kbg> passando para o pai (<kbg>App</kbg>) os dados que obtivemos do GitHub.

Nós o adicionamos ao <kbg>App</kbg>, passando um método para adicionar um novo cartão à lista de cartões, o <kbg>addNewCard</kbg>, como uma props chamada <kbg>onSubmit</kbg>:

```
const App = () => {
  const [cards, setCards] = useState([])
  
  addNewCard = cardInfo => {
    setCards(cards.concat(cardInfo))
  }
  
  return (
    <div>
      <Form onSubmit={addNewCard} />
      <CardList cards={cards} />
    </div>
  )
}

```

Finalmente nós renderizamos o app:

```
ReactDOM.render(<App />, document.getElementById('app'))
```
Aqui está o código completo do nosso pequeno app em React:

```
const { useState } = React

const Card = props => {
  return (
    <div style={{ margin: '1em' }}>
      <img alt="avatar" style={{ width: '70px' }} src={props.avatar_url} />
      <div>
        <div style={{ fontWeight: 'bold' }}>{props.name}</div>
        <div>{props.blog}</div>
      </div>
    </div>
  )
}

const CardList = props => <div>{props.cards.map(card => <Card {...card} />)}</div>

const Form = props => {
  const [username, setUsername] = useState('')
  
  handleSubmit = event => {
    event.preventDefault()
    
    axios
      .get(`https://api.github.com/users/${username}`)
      .then(resp => {
        props.onSubmit(resp.data)
        setUsername('')
      })
  }
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={username}
        onChange={event => setUsername(event.target.value)}
        placeholder="GitHub username"
        required
      />
      <button type="submit">Add card</button>
    </form>
  )
}

const App = () => {
  const [cards, setCards] = useState([])
  
  addNewCard = cardInfo => {
    setCards(cards.concat(cardInfo))
  }
  
  return (
    <div>
      <Form onSubmit={addNewCard} />
      <CardList cards={cards} />
    </div>
  )
}

ReactDOM.render(<App />, document.getElementById('app'))
```

Esse é o resultado final:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/cZoqPqmbwvuUaIiWJ16fTj6VOhTIquXDECnP" alt="Final Result" /> </h1>











