# Prismic preview

Enable previews of your prismic documents by looking for graphql query data and patch in data from prismic previews.

> **Note**
>
> Checkout gatsby-source-prismic-graphql for updated version that works with Prismic's GraphQL API https://github.com/birkir/gatsby-source-prismic-graphql
>
> It has more features and much better stability

## Installing

Install module

```bash
npm install --save gatsby-plugin-prismic-preview
```

Add plugin to `gatsby-config.js`:

```js
{
  resolve: 'gatsby-plugin-prismic-preview',
  options: {
    repositoryName: 'gatsby-source-prismic-test-site',
    linkResolver: require('./src/linkResolver'),
    path: '/preview',
  }
}
```

## Configuration

### `repositoryName`

Should be the same as the one in gatsby-source-prismic plugin

### `linkResolver`

Inline function

```js
options: {
  linkResolver(doc) {
    if (doc.type === 'BlogPost') {
      return `/blog/${doc.uid}`;
    }
    return `${doc.type}`;
  },
},
```

or a require to a specific file (must be ES5 `module.exports` format)

```js
options: {
  linkResolver: require('./src/utils/linkResolver'),
},
```

### path

Where the preview page should live.

Defaults to `/preview`.

## Usage

```jsx
import { withPrismicPreview } from 'gatsby-plugin-prismic-preview';

const AboutPage = ({ data }) => (
  <h1>
    About
    {console.log('This will now include preview data:', data.prismicAboutPage.title)}
  </h1>
);

export default withPrismicPreview({ data })(AboutPage);
```

## Staging environment

Only allow previews on staging? In `gatsby-config.js` do a conditional operation:

```js
const plugins = [
  'plugin-1',
  'plugin-2',
];

if (process.env.NODE_ENV === 'staging') {
  plugins.push({
    resolve: 'gatsby-plugin-prismic-preview',
    options: {}
  });
}

module.exports = {
  siteMetadata: {
    title: 'Gatsby Default Starter',
  },
  plugins,
};
```

## Troubleshooting

Report issues on GitHub
