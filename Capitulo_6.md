<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 6:</strong> FERRAMENTAS </h2>

## Babel

Babel é uma ferramenta incrível e existe há algum tempo, mas hoje em dia quase todos os desenvolvedores de JavaScript confiam nela. Isso continuará, porque Babel agora é indispensável e resolveu um grande problema para todos.

Qual problema?

O problema que todo desenvolvedor da Web certamente já enfrentou: um recurso de JavaScript está disponível na versão mais recente de um navegador, mas não nas versões mais antigas. Ou talvez o Chrome ou o Firefox o implementem, mas o Safari iOS e o Edge não.

Por exemplo, o ES6 introduziu as arrows functions:

```
[1, 2, 3].map((n) => n + 1)
```

Então, como você deve lidar com esse problema? Você deve seguir em frente e ignorar esses clientes com navegadores mais antigos/incompatíveis ou deve escrever um código JavaScript mais antigo para deixar todos os usuários felizes?

Aí que entra o Babel. Babel é um compilador: pega o código escrito em uma versão e transpila para código escrito em outra versão.

Você pode configurar o Babel para transpilar o JavaScript do ES2017 para a sintaxe do JavaScript ES5:

```
[1, 2, 3].map(function(n) {
  return n + 1
})
```

### Instalando o Babel

O Babel pode ser facilmente instalado usando o npm:

```
npm install --save-dev @babel/core @babel/cli
```

Como o npm agora vem com o npx, os pacotes CLI instalados localmente podem ser executados digitando o comando na pasta do projeto:

Então podemos executar o Babel executando apenas

```
npx babel script.js
```

### Um exemplo de configuração do Babel

O Babel instalado ainda não faz nada de útil, então você precisa configurá-lo e adicionar alguns plugins.

> [Aqui está uma lista de plugins Babel](https://babeljs.io/docs/en/plugins)

Para resolver o problema de que falamos na introdução (usar as arrow functions em todos os navegadores), podemos executar

```
npm install --save-dev \
    @babel/plugin-transform-es2015-arrow-functions
```

para baixar o pacote no <kbg>node_modules</kbg> do seu app, nós precisamos adicionar
```
{
  "plugins": ["transform-es2015-arrow-functions"]
}
```

para o arquivo <kbg>.babelrc</kbg> presente na pasta raiz do aplicativo. Se você ainda não possui esse arquivo, basta criar um arquivo em branco e colocar esse conteúdo nele.

Agora, só nós tivermos um arquivo <kbg>script.js</kbg> com esse código: 
```
var a = () => {};
var a = (b) => b;

const double = [1,2,3].map((num) => num * 2);
console.log(double); // [2,4,6]

var bob = {
  _name: "Bob",
  _friends: ["Sally", "Tom"],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
};
console.log(bob.printFriends());
```
executando <kbg>babel script.js</kbg> nós retornaremos o seguinte código:
```
var a = function () {};var a = function (b) {
  return b;
};

const double = [1, 2, 3].map(function (num) {
  return num * 2;
});
console.log(double); // [2,4,6]

var bob = {
  _name: "Bob",
  _friends: ["Sally", "Tom"],
  printFriends() {
    var _this = this;
    
    this._friends.forEach(function (f) {
      return console.log(_this._name + " knows " + f);
    });
  }
};
console.log(bob.printFriends());
```

Como você pode ver, as arrow functions foram convertidas em funções do ES5.

### Babel presets

Acabamos de ver no artigo anterior como o Babel pode ser configurado para transpilar recursos específicos de JavaScript.

Você pode adicionar muito mais plugins, mas não pode adicionar aos recursos de configuração um por um, não é nada prático.

É por isso que Babel oferece <kbg>presets</kbg> (predefinições em pt-br hehe).

Os <kbg>presets</kbg> mais populares são o <kbg>env</kbg> e o <kbg>react</kbg>.

### <kbg>env</kbg> preset

O <kbg>env</kbg> é muito útil: você diz quais ambientes deseja suportar e ele faz tudo por você, aceitando todos os recursos modernos do JavaScript.

Por exemplo: "Suporte as duas últimas versões de todos os navegadores, mas, para o Safari, suporte todas as versões desde o Safari 7"

```
{
  "presets": [
    ["env", {
      "targets": {
        "browsers": ["last 2 versions", "safari >= 7"]
      }
    }]
  ]
}
```

ou "Não preciso de suporte do navegador, apenas deixe-me trabalhar com o Node.js. 6.10"

```
{
  "presets": [
    ["env", {
      "targets": {
        "node": "6.10"
      }
    }]
  ]
}
```

### <kbg>react</kbg> preset

O preset <kbg>react</kbg> é muito útil ao escrever aplicativos com React: adicionando <kbg>preset-flow</kbg>, <kbg>syntax-jsx</kbg>, <kbg>transform-react-jsx</kbg>, <kbg>transform-react-display-name</kbg>.

Ao incluí-lo, você estará pronto para desenvolver aplicativos React, com transformações JSX e suporte ao Flow.

### Mais informações sobre os presets

[https://babeljs.io/docs/plugins/](https://babeljs.io/docs/plugins/)

### Usando Babel com Webpack

Se você deseja executar o JavaScript moderno no navegador, o Babel por si só não é suficiente, também é necessário agrupar o código. O Webpack é a ferramenta perfeita para isso.

O JS moderno precisa de dois estágios diferentes: um estágio de compilação e um estágio de runtime. Isso ocorre porque alguns recursos do ES6+ precisam de um polyfill ou de um runtime helper.

Para instalar a funcionalidade de runtime no polyfill do Babel, execute:

```
npm install @babel/polyfill \
            @babel/runtime \
            @babel/plugin-transform-runtime
```

Agora, no seu arquivo <kbg>webpack.config.js</kbg> adicione:
```
entry: [
  'babel-polyfill',
  // your app scripts should be here
],

module: {
  loaders: [
    // Babel loader compiles ES2015 into ES5 for
    // complete cross-browser support
    {
      loader: 'babel-loader',
      test: /\.js$/,
      // only include files present in the `src` subdirectory
      include: [path.resolve(__dirname, "src")],
      // exclude node_modules, equivalent to the above line
      exclude: /node_modules/,
      query: {
        // Use the default ES2015 preset
        // to include all ES2015 features
        presets: ['es2015'],
        plugins: ['transform-runtime']
      }
    }
  ]
```
Mantendo os <kbg>presets</kbg> e os <kbg>plugins</kbg> dentro do arquivo <kbg>webpack.config.js</kbg>, podemos evitar um arquivo <kbg>.babelrc</kbg>.

## Webpack
