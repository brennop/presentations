# Criando um Blog em Gatsby

[[toc]]

## Começando

### Instalando o CLI do Gatsby

```bash
yarn global add gatsby-cli
```

### Iniciando um projeto

Pra iniciar o starter default. Você pode conferir outros
starters disponíveis na [biblioteca de starters do
Gatsby](https://www.gatsbyjs.org/starters/).

```bash
gatsby new blog
```

Vamos utilizar o [stater hello
world](https://github.com/gatsbyjs/gatsby-starter-hello-world)
que contém o mínimo de uma aplicação em Gatsby.

```bash
gatsby new blog https://github.com/gatsbyjs/gatsby-starter-hello-world
```

### Iniciando o projeto

```bash
gatsby develop
```

## Estrutura de pastas

- Raiz:
  Arquivos de API do Gatsby
- src/
  Semelhante ao src do React
- src/pages
  Todas os componentes exportados aqui serão automaticamente
  transformados em rotas
- public
  Build final do Gatsby
- static
  Arquivos que devem estar disponíveis na build

## Configurando

As configurações são um objeto exportado pelo arquivo
`gatsby-config.js`.

### [Plugins](https://www.gatsbyjs.org/plugins/)

#### React-Helmet

Componente helper criado pelos desenvolvedores da NFL para
gerenciar o \<head\> com React.

```bash
yarn add gatsby-plugin-react-helmet react-helmet
```

```javascript
plugins: [`gatsby-plugin-react-helmet`];
```

[React Helmet](https://github.com/nfl/react-helmet)

#### Google Fonts

Plugin para precarregar as fontes do [Google
Fonts](https://fonts.google.com)

```bash
yarn add gatsby-plugin-prefetch-google-fonts
```

```javascript
plugins: [
  {
    resolve: `gatsby-plugin-prefetch-google-fonts`,
    options: {
      fonts: [
        {
          family: `Oswald`,
          subsets: [`latin`],
        },
        {
          family: `Open Sans`,
          variants: [`400`, `700`],
        },
      ],
    },
  },
];
```

Ver também:

- [Typography](https://www.gatsbyjs.org/packages/gatsby-plugin-typography)
- [Typefaces](https://github.com/KyleAMathews/typefaces)

#### styled-components

```bash
yarn add gatsby-plugin-styled-components styled-components babel-plugin-styled-components
```

```javascript
plugins: [`gatsby-plugin-styled-components`];
```

#### [Source Filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem)

Esse plugin cria nós a partir dos sistema de arquivos para
os plugins "transformer" gerarem dados acessíveis pela
camada GraphQL do Gatsby.

Você pode ter múltiplas instâncias desse plugin, uma pra
cada fonte de arquivos.

```bash
yarn add gatsby-source-filesystem
```

```javascript
plugins: [
  {
    resolve: `gatsby-source-filesystem`,
    options: {
      name: `posts`,
      path: `${__dirname}/src/posts/`,
    },
  },
];
```

#### [Markdown](https://www.gatsbyjs.org/packages/gatsby-transformer-remark/)

```bash
yarn add gatsby-transformer-remark
```

```javascript
plugins: [
  {
    resolve: `gatsby-transformer-remark`,
    options: {
      plugins: [],
    },
  },
],
```

#### [Sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp/)

Usa o [Sharp](https://github.com/lovell/sharp) para otimizar
o carregamento de imagens. Vamos utilizar junto com o remark
para otimizar as imagens do nosso markdown.

```bash
yarn add gatsby-remark-images gatsby-plugin-sharp
```

```javascript
plugins: [
  `gatsby-plugin-sharp`,
  {
    resolve: `gatsby-transformer-remark`,
    options: {
      plugins: [
        {
          resolve: `gatsby-remark-images`,
          options: {
            maxWidth: 590,
          },
        },
      ],
    },
  },
];
```

#### Outros:

- [PrismJS](https://www.gatsbyjs.org/packages/gatsby-remark-prismjs/) (Syntax Highlighting)
- [nprogress](https://www.gatsbyjs.org/packages/gatsby-plugin-nprogress) (Barra de Progresso)
- [Google Analytics](https://www.gatsbyjs.org/packages/gatsby-plugin-google-analytics/) (Analytics)
- [manifest](https://www.gatsbyjs.org/packages/gatsby-plugin-manifest/) (PWA)
- [offline](https://www.gatsbyjs.org/packages/gatsby-plugin-offline/) (PWA Offline)

### siteMetadata

Metadados disponíveis para toda a aplicação pela camada de
GraphQL pela query `site`.

```javascript
siteMetadata: {
  title: `BJR`,
  description: `Empresa Júnior de Blogs`,
  lang: `pt-br`,
  author: `@brennop`
}
```

## Criando a página inicial

### Adicionando estilos globais

Assim como podíamos adicionar um `.css` no `index.js` da
nossa aplicação React, se quisermos que um código esteja
disponível em todas as páginas podemos usar a API do
`gatsby-browser.js`

```css
/* src/styles.css */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Roboto, sans-serif;
}
```

```javascript
// gatsby-browser.js
import "./src/styles.css";
```

### Criando um componente de SEO

Podemos usar o ambiente interativo _GraphiQL_ para obter
a query dos metadados.

## Criando um post

### Criando o Markdown

Podemos usar o frontmatter para adicionar metadados ao post.

### Criando as páginas

Usamos as [APIs expostas pelo
Gatsby](https://www.gatsbyjs.org/docs/api-files-gatsby-node/)
no arquivo `gatsby-node.js`.

### Criando um template

```jsx
// src/templates/blog-post.js

export const query = graphql`
  query BlogPostBySlug($slug: String!) {
    markdownRemark(frontmatter: { slug: { eq: $slug } }) {
      html
      frontmatter {
        date(formatString: "DD-MM-YY")
        slug
        title
      }
    }
  }
`;

export default ({ data }) => {
  const { markdownRemark: post } = data;
  return (
    <Layout>
      <SEO title={post.frontmatter.title} />
      <Navbar />
      <Post>
        <h1 className="post-title">{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </Post>
    </Layout>
  );
};
```

## Criando a página de blog

Fazer um map com o resultado da query de posts.

## Criando uma 404

https://www.gatsbyjs.org/docs/add-404-page/

## Benchmark: Lighthouse
