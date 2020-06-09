<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 5:</strong> ESTILIZANDO </h2>

## CSS no React

Usando o React, você tem várias maneiras de adicionar estilo aos seus componentes.

### Usando classes e CSS

A primeira, e a mais simples, é usar classes e um arquivo CSS normal para direcionar essas classes:

```
const Button = () => {
  return <button className="button">A button</button>
}

.button {
  background-color: yellow;
}
```

Você pode importar a folha de estilo assim:

```
import './style.css'
```

e o Webpack dará conta de adicionar o CSS ao pacote.

### Usando o atribulo style

Um segundo método é usar o atributo <kbg>style</kbg> anexado a um elemento JSX. Usando essa abordagem, você não precisa de um arquivo CSS separado.

```
const Button = () => {
  return <button style={{ backgroundColor: 'yellow' }}>A button</button>
}
```

CSS é definido de uma maneira um pouco diferente agora. Primeiro, observe os colchetes duplos: é porque o <kbg>style</kbg> aceita um objeto. Passamos um objeto JavaScript, definido em chaves. Também poderíamos fazer isso:

```
const buttonStyle = { backgroundColor: 'yellow' }
const Button = () => {
  return <button style={buttonStyle}>A button</button>
}
```

Além disso, o estilo agora é camelCased em vez de usar traços. Toda vez que uma propriedade CSS tiver um traço, remova-a e inicie a próxima palavra em maiúscula.

<kbg>Styles</kbg> têm o benefício de serem locais para o componente e não poderem vazar para outros componentes em outras partes do aplicativo, algo que o uso de classes e um arquivo CSS externo não pode fornecer.

### Usando CSS Modules

CSS Modules parece ser um opção perfeita entre as duas opções acima: você usa classes, mas o CSS tem escopo definido para o componente, o que significa que qualquer estilo adicionado não pode ser aplicado a outros componentes sem a sua permissão. E, no entanto, seus estilos são definidos em um arquivo CSS separado, mais fácil de manter do que CSS em JavaScript (e você pode usar seus bons e antigos nomes de propriedades CSS).

Comece criando um arquivo CSS que termine com <kbg>.module.css</kbg>, por exemplo, <kbg>Button.module.css</kbg>. Uma ótima opção é atribuir o mesmo nome ao componente que você vai modelar:

Adicione seu CSS aqui e importe-o dentro do arquivo de componente que você deseja estilizar:

```
import style from './Button.module.css'
```

agora você pode usar isso no seu JSX: 
```
const Button = () => {
  return <button className={style.content}>Um botão</button>
}
```

É isso aí! Na marcação resultante, o React gera uma classe específica e exclusiva para cada componente renderizado e atribui o CSS a essa classe, assim o CSS não afeta outra marcação.

## SASS no React (meu preferido aqui hehe)

Ao criar um aplicativo React usando o <kbg>create-react-app</kbg>, você tem muitas opções à sua disposição quando se trata de estilo.

> Obviamente, se não estiver usando o <kbg>create-react-app</kbg>, você terá todas as opções do mundo, mas limitamos a discussão às opções fornecidas pelo <kbg>create-react-app</kbg>.

Você pode estilizar usando classes simples e arquivos CSS, usando o atributo <kbg>style</kbg> ou o <kbg>CSS Modules</kbg>, por exemplo.

SASS/SCSS é uma opção muito popular e muito amada entre os desenvolvedores.

Você pode usá-lo sem nenhuma configuração, começando com <kbg>create-react-app</kbg>.

Tudo o que você precisa é criar um arquivo <kbg>.sass</kbg> ou <kbg>.scss</kbg> e importá-lo em um componente:

```
import './styles.scss'
```

## Styled Components

Styled Components é uma das novas maneiras de usar o CSS no JavaScript moderno. Ele pretende ser um sucessor dos CSS Modules, e é outra maneira de escrever CSS com escopo definido para um único componente.

### Uma curta história 

Houve uma vez em que a Web era realmente simples e o CSS nem existia. Organizávamos as páginas usando tables e frames. Bons tempos.

Então o CSS ganhou vida e, depois de algum tempo, ficou claro que os frameworks poderiam ajudar bastante, especialmente na criação de grids e layouts, o Bootstrap desempenhou um papel importante nisso.

Pré-processadores como o SASS e outros ajudaram muito a desacelerar a adoção de frameworks e a organizar melhor o código. Convenções como o BEM e o SMACSS cresceram em uso, especialmente em equipes.

As convenções não são uma solução para tudo, e são complexas de serem lembradas; portanto, nos últimos anos, com a crescente adoção do JavaScript e processos de construção em todos os projetos de front-end, o CSS encontrou seu caminho no JavaScript (CSS-in-JS).

Novas ferramentas exploraram novas maneiras de executar CSS-in-JS e algumas tiveram sucesso com crescente popularidade:

- React Style
- jsxstyle
- Radium

e mais.

### Introduzindo Styled Components

Uma das ferramentas mais populares é o Styled Components.

Ele pretende ser um sucessor do CSS Modules, uma maneira de escrever CSS com escopo definido para um único componente.

Styled Components permite que você escreva CSS simples em seus componentes sem se preocupar com colisões de nomes de classes.

#### Instalação

Instale usando <kbg>npm</kbg> ou <kbg>yarn</kbg>:
```
npm install styled-components
yarn add styled-components
```

É isso aí! Agora tudo que você precisa fazer é adicionar este import:
```
import styled from 'styled-components'
```

### Seu primeiro styled component

Com o <kbg>styled</kbg> importado, agora você pode começar a criar Styled Components. Aqui está o primeiro:
```
const Button = styled.button`
  font-size: 1.5em;
  background-color: black;
  color: white;
```
<kbg>Button</kbg> é agora um componente React.

Nós criamos isso usando uma função do <kbg>styled</kbg>, chamando button nesse caso, e passando algumas propriedades do CSS em uma template literal.

Agora esse componenente pode ser renderizado em nosso container usando a sintaxe normal do React:
```
render(<Button />)
```

Styled Components oferece outras funções que você pode usar para criar outros componentes, não apenas botões, mas também <kbg>section</kbg>, <kbg>h1</kbg>, <kbg>input</kbg> e muitos outros.

A sintaxe usada com o backtick pode ser estranha no começo, mas é chamada de <kbg>Tagged templates</kbg> e é uma maneira de passar um argumento para a função.

### Usando props para customizar um component 

Quando você passa alguns objetos para um Styled Component, ele os passa para um nó da DOM.

Por exemplo, aqui está como passamos as props do <kbg>placeholder</kbg> e do <kbg>type</kbg> para um componente de entrada:

```
const Input = styled.input`
  //...
`

render(
  <div>
    <Input placeholder="..." type="text" />
  </div>
)
```

Isso fará exatamente o que você pensa, inserindo esses objetos como atributos HTML.

As props, em vez de apenas serem transmitidas às cegas para a DOM, também podem ser usadas para personalizar um componente com base no seu valor. Aqui está um exemplo:

```
const Button = styled.button`
  background: ${props => (props.primary ? 'black' : 'white')};
  color: ${props => (props.primary ? 'white' : 'black')};
`

render(
  <div>
    <Button>A normal button</Button>
    <Button>A normal button</Button>
    <Button primary>The primary button</Button>
  </div>
)
```

### Extendendo um Styled Component

Se você possui um componente e deseja criar um semelhante, com um estilo um pouco diferente, pode usar o extend:
```
const Button = styled.button`
  color: black;
  //...
`

const WhiteButton = Button.extend`
  color: white;
`

render(
  <div>
    <Button>A black button, like all buttons</Button>
    <WhiteButton>A white button</WhiteButton>
  </div>
)
```

### É CSS simples

Em Styled Components você pode usar o CSS que você já conhece e ama. É só CSS simples. 

Você pode usar media queries, aninhamento e qualquer outra coisa que possa precisar.
