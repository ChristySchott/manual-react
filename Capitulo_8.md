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

### Tipos de routas

React Router fornece dois tipos de routas:

- `BrowserRouter`
- `HashRouter`

Um cria URLs clássicos, o outro cria URLs com o hash:

```
https://application.com/dashboard   /* BrowserRouter */
https://application.com/#/dashboard /*  HashRouter  */
```

Qual deles usar é ditado principalmente pelos navegadores que você precisa oferecer suporte. O `BrowserRouter` usa a `History API`, que é relativamente recente e não é suportada no IE9 e abaixo. Se você não precisa se preocupar com navegadores antigos, é a escolha recomendada.
