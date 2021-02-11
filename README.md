# gatsby-source-strapi

Source plugin for pulling documents into Gatsby from a Strapi API.

## Info

Published version of this fork: https://github.com/unagigd/gatsby-source-strapi (forked to with minor changes: https://github.com/OddBlueDog/gatsby-source-strapi)

More info here: https://github.com/strapi/gatsby-source-strapi/pull/122#issuecomment-765175178

## Install

`npm install --save @oddbluedog/gatsby-source-strapi-support-markdown-images`

## How to use

See more here: https://github.com/strapi/gatsby-source-strapi/pull/122#issuecomment-612969087

```javascript
// In your gatsby-config.js
plugins: [
  {
    resolve: `gatsby-source-strapi`,
    options: {
      apiURL: `http://localhost:1337`,
      queryLimit: 1000, // Default to 100
      contentTypes: [`article`, `user`],
      //If using single types place them in this array.
      singleTypes: [`home-page`, `contact`],
      // Possibility to login with a strapi user, when content types are not publically available (optional).
      loginData: {
        identifier: '',
        password: '',
      },
      markdownImages: {
        typesToParse: {
          article: ['content'],
        },
      },
    },
  },
]
```

## How to query

You can query Document nodes created from your Strapi API like the following:

```graphql
{
  allStrapiArticle {
    edges {
      node {
        id
        title
        content
      }
    }
  }
}
```

To query images you can do the following:

```graphql
{
  allStrapiArticle {
    edges {
      node {
        id
        singleImage {
          publicURL
        }
        multipleImages {
          localFile {
            publicURL
          }
        }
      }
    }
  }
}
```
