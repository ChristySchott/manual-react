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




