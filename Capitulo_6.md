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

O Webpack é uma ferramenta que permite compilar módulos JavaScript, também conhecidos como empacotadores de módulos (module bundlers). Dado um grande número de arquivos, ele gera um único arquivo (ou alguns arquivos) que executa seu aplicativo.

Ele pode executar muitas operações:

- ajuda a agrupar seus recursos.
- procura alterações e executa novamente as tarefas.
- pode executar a transpilação Babel para o ES5, permitindo que você use os recursos mais recentes do JavaScript sem se preocupar com o suporte que o navegador oferece.
- pode transpilar CoffeeScript para JavaScript
- pode converter imagens embutidas em URIs de dados.
- permite usar require() para arquivos CSS.
- pode dividir os arquivos de saída em vários arquivos, para evitar que um arquivo js enorme seja carregado na primeira página.

O uso do Webpack não é limitado a frontend, pois ele também é útil no desenvolvimento backend com o <kbg>Node.js</kbg>.

Os antecessores do webpack e ferramentas ainda amplamente usadas incluem:

- Grunt
- Broccoli
- Gulp

Existem muitas semelhanças no que seus antecessores e o Webpack pode fazer, mas a principal diferença é que eles são conhecidos como executores de tarefas (task runners), enquanto o Webpack surgiu como um empacotador de módulos (module bundles).

Webpack é uma ferramenta mais focada: você especifica um ponto de entrada para seu aplicativo (pode até ser um arquivo HTML com tags de script) e o Webpack analisa os arquivos e agrupa tudo o que você precisa para executar o aplicativo em um único arquivo de saída JavaScript (ou em mais arquivos se você usar a divisão de código).

### Instalando o Webpack

O Webpack pode ser instalando globalmente ou localmente para cada projeto.

### Instalando globalmente

Com o Yarn:

```
yarn global add webpack webpack-cli
with npm:
```
com o npm:
```
npm i -g webpack webpack-cli
```

uma vez que isso é feito, você pode executar 
```
webpack-cli
```

### Instalando localmente

O Webpack também pode ser instalado localmente. É a configuração recomendada, porque ele pode ser atualizado em cada projeto e você tem menos resistência ao uso dos recursos mais recentes.

Com yarn:
```
yarn add webpack webpack-cli -D
```

com npm:
```
npm i webpack webpack-cli --save-dev
```

uma vez que isso é feito, adicione isso ao seu <kbg>package.json</kbg>
```
{
  //...
  "scripts": {
    "build": "webpack"
  }
}
```

e agora você pode executá-lo digitando
```
npm run build
```

na pasta do projeto.

### Configuração do Webpack

Por padrão, o Webpack (a partir da versão 4) não requer nenhuma configuração se você respeitar estas convenções: 

- o <kbg>entry point</kbg> do seu app é <kbg>./src/index.js</kbg>
- o <kbg>output</kbg> está em <kbg>./dist/main.js</kbg>
- Webpack funciona em modo de produção

Você pode personalizar o Webpack, caso precise. A configuração do Webpack é armazenada no arquivo <kbg>webpack.config.js</kbg>, na pasta raiz do projeto.

### O <kbg> entry point </kbg> (ponto de entrada)

Por padrão, o ponto de entrada é <kbg>./src/index.js</kbg>. Este exemplo simples usa o <kbg>arquivo ./index.js</kbg> como ponto de entrada:
```
module.exports = {
  /*...*/
  entry: './index.js'
  /*...*/
}
```

### O <kbg>output</kbg> (ponto de saída)

Por padrão, a saída é gerada em <kbg>./dist/main.js</kbg>. Este exemplo coloca o pacote de saída sendo o <kbg>app.js</kbg>:
```
module.exports = {
  /*...*/
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'app.js'
  }
  /*...*/
}
```

### Loaders

O uso do webpack permite que você use <kbg>import</kbg> ou <kbg>require</kbg> no seu código JavaScript não apenas para incluir outro arquivo JavaScript, mas qualquer tipo de arquivo, como por exemplo, o CSS.

O Webpack tem como objetivo lidar com todas as nossas dependências, não apenas JavaScript, e os <kbg>loaders</kbg> são uma maneira de fazer isso.

Por exemplo, no seu código, você pode usar:

```
import 'style.css'
```

usando essa configuração de <kbg>loader</kbg>:
```
module.exports = {
  /*...*/
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
    }]
  }
  /*...*/
}
```

um <kbg>loader</kbg> pode ter <kbg>options</kbg>:

```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
  /*...*/
}
```

Você pode exigir vários loaders para cada regra:
```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.css$/,
        use:
          [
            'style-loader',
            'css-loader',
          ]
      }
    ]
  }
  /*...*/
}
```

Neste exemplo, o <kbg>css-loader</kbg> interpreta o <kbg>import 'style.css'</kbg> no CSS. O <kbg>style-loader</kbg> é responsável por injetar esse CSS no DOM, usando uma tag `<style>`.

A ordem importa, e é reversa (a última é executada primeiro).

Quais tipo de loaders existem? Muitos! [Você pode encontrar a lista completa aqui](https://webpack.js.org/loaders/).

Um carregador comumente usado é o <kbg>Babel</kbg>, usado para transpilar o JavaScript moderno para o código ES5:
```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
          }
        }
      }
    ]
  }
  /*...*/
}
```

Este exemplo faz com que o Babel pré-processe todos os nossos arquivos React/JSX:

```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  },
  resolve: {
    extensions: [
      '.js',
      '.jsx'
    ]
  }
  /*...*/
}
```
### Plugins

<kbg>Plugins</kbg> são como <kbg>loaders</kbg>, mas com esteróides. Eles podem fazer coisas que os <kbg>loaders</kbg> não podem fazer e são o principal componente do Webpack.

Veja este exemplo:
```
module.exports = {
  /*...*/
  plugins: [
    new HTMLWebpackPlugin()
  ]
  /*...*/
}
```

O plug-in HTMLWebpackPlugin tem a tarefa de criar automaticamente um arquivo HTML, incluindo o caminho do pacote JS de saída, para que o JavaScript esteja pronto para ser veiculado.

Existem muitos plugins disponíveis.

Um outro plugin útil, o CleanWebpackPlugin, pode ser usado para limpar a pasta dist/ antes de criar qualquer saída, assim você não esquece os esquecer por aí quando alterar o nome do arquivo de saída:
```
module.exports = {
  /*...*/
  plugins: [
    new CleanWebpackPlugin(['dist']),
  ]
  /*...*/
}
```

### O modo Webpack

Este modo (introduzido no webpack 4) define o ambiente no qual o Webpack funciona. Ele pode ser definido como desenvolvimento ou produção (o padrão é produção, portanto, você só o define ao passar para o desenvolvimento).

```
module.exports = {
  entry: './index.js',
  mode: 'development',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'app.js'
  }
}
```
Modo de desenvolvimento:

- constrói muito rápido
- é menos otimizado que a produção
- não remove comentários
- fornece mensagens de erro e sugestões mais detalhadas
- fornece uma melhor experiência de debbuging

A construção do modo de produção é mais lenta, pois precisa gerar um pacote mais otimizado. O arquivo JavaScript resultante é menor em tamanho, pois remove muitas coisas que não são necessárias na produção.

Eu fiz um aplicativo de exemplo que apenas imprime um console.log.

Aqui está o pacote de produção:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/kbXOiSFaO06VSDxcLC29Nh4a8ycSoaL9LDup" alt="pacote de produção"/> </h1>

Aqui está o pacote de desenvolvimento:

<h1 align="center"> <img src="https://cdn-media-1.freecodecamp.org/images/W-1sAge4rvYL0aH00e7FuyJ5NLv7PJYpves0" alt="pacote de desenvolvimento"/> </h1>

### Executando o Webpack

Se instalado globalmente, o Webpack pode ser executado manualmente a partir da linha de comando, mas geralmente você escreve um script dentro do arquivo <kbg>package.json</kbg>, que é executado usando <kbg>npm</kbg> ou <kbg>yarn</kbg>.

Por exemplo, esta definição de script package.json que usamos anteriormente:

```
"scripts": {
  "build": "webpack"
}
```

agora é só rodar um 

```
npm run build
```

ou

```
yarn build
```
### Observando mudanças

O Webpack pode reconstruir automaticamente o pacote quando ocorrer uma alteração no seu aplicativo e continuar ouvindo a próxima alteração.

Basta adicionar este script:
```
"scripts": {
  "watch": "webpack --watch"
}
```

e rodar 
```
npm run watch
```

Um recurso interessante do modo de exibição é que o pacote configurável é alterado apenas se a construção não apresentar erros. Se houver erros, o <kbg>watch</kbg> continuará ouvindo as alterações e tentará reconstruir o pacote, mas o pacote em funcionamento não será afetado por essas construções problemáticas.

### Manipulando imagens

O Webpack nos permite usar imagens de uma maneira muito conveniente, usando o <kbg>file-loader</kbg>;

Esta configuração simples:

```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader'
        ]
      }
    ]
  }
  /*...*/
}
```

Permite a você importar imagens no seu JavaScript:
```
import Icon from './icon.png'

const img = new Image()
img.src = Icon
element.appendChild(img)
```

O <kbg>file-loader</kbg> também pode lidar com outros tipos de assets, como fontes, arquivos CSV, xml e muito mais.

Outra ferramenta interessante para trabalhar com imagens é o <kbg>url-loader</kbg>.

Este exemplo carrega qualquer arquivo PNG menor que 8 KB como um URL de dados.

```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.png$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
  /*...*/
}
```

### Processando seu código em Sass e transformando em CSS

Usando <kbg>sass-loader</kbg>, <kbg>css-loader</kbg> e <kbg>style-loader</kbg>:
```
module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      }
    ]
  }
  /*...*/
}
```

### Gerando Source Maps (mapas de origem)

Como o webpack agrupa o código, os source maps são obrigatórios para obter uma referência ao arquivo que gerou um erro, por exemplo.

Você diz ao Webpack para gerar source maps usando a propriedade <kbg>devtool</kbg>:
```
module.exports = {
  /*...*/
  devtool: 'inline-source-map',
  /*...*/
}
```

<kbg>devtool</kbg> possui muitos valores, os mais usados são:

<kbg>none</kbg>: não adiciona nenhum source map
<kbg>source-map</kbg>: ideal para produção, fornece um mapa de origem separado que pode ser minimizado e adiciona uma referência ao pacote, para que as ferramentas de desenvolvimento saibam que o mapa de origem está disponível. Obviamente, você deve configurar o servidor para evitar o envio e usá-lo apenas para fins de depuração.
<kbg>inline-source-map</kbg>: ideal para desenvolvimento, alinha o mapa de origem como uma URL de dados
