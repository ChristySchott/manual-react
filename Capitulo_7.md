<h1 align="center">Manual do React</h1>

<h1 align="center"><img src="https://cdn-media-1.freecodecamp.org/images/1*m5aPLXkrWJs7xKsfYViJEg.png" /></h1>

<h2 align="center"><strong>SEÇÃO 7:</strong> TESTES </h2>

## Jest

Jest é uma biblioteca para testar o código JavaScript.

É um projeto open source mantido pelo Facebook e é especialmente adequado para testar códigos no React, embora não se limite a isso: ele pode testar qualquer código JavaScript. Seus pontos fortes são:

- é rápido
- ele pode executar testes instantâneos (snapshot testing)
- é opinativo e fornece tudo pronto para uso, sem exigir que você faça escolhas

O Jest é uma ferramenta muito semelhante ao Mocha, embora eles tenham diferenças:

- Mocha é menos opinativo, enquanto Jest tem um certo conjunto de convenções
- O Mocha requer mais configuração, enquanto o Jest, por ser opinativo, geralmente funciona imediatamente
- O Mocha é mais antigo e estabelecido, com mais integrações de ferramentas

Na minha opinião, o maior recurso do Jest é ser uma solução pronta para uso que funciona sem ter que interagir com outras bibliotecas de teste.

### Instalação

O Jest é instalado automaticamente com o <kbg>create-react-app</kbg>. Portanto, se você usar isso, não precisará instalar o Jest.

O Jest pode ser instalado em qualquer outro projeto usando o Yarn:

```
yarn add --dev jest
```

ou o npm

```
npm install --save-dev jest
```

observe como instruímos ambos a colocar o Jest nas <kbg>devDependencies</kbg> do arquivo <kbg>package.json</kbg>, para que ele seja instalado apenas no ambiente de desenvolvimento e não na produção.

Inclua esta linha na parte de scripts do seu arquivo <kbg>package.json</kbg>:

```
{
  "scripts": {
    "test": "jest"
  }
}
```
então os testes podem ser executados rodando <kbg> npm run test</kbg> ou <kbg>yarn test</kbg>

### Criando o primeiro teste com o Jest
