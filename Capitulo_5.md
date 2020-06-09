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
