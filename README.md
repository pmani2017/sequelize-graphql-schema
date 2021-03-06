# sequelize-graphql-schema

A helper function that automatically generates `GraphQLSchema` from Sequelize models.
Extended Romain Pellerin's https://github.com/rpellerin/graphql-sequelize-schema-generator

## Installation

```bash
npm install sequelize-graphql-schema
```

## Prerequisites

This package assumes you have `graphql` and `sequelize` already installed (both packages are declared as `dependencies` and `peerDependencies`).

## Usage

```javascript
var {generateModelTypes, generateSchema} = require('sequelize-graphql-schema')
var models = require('./models')
var schema = generateSchema(models) // Generates the schema
// OR
var types = generateModelTypes(models)
var schema = generateSchema(models, types) // Generates the schema by reusing the types
```

### Example with Express

```javascript
var { GraphQLSchema } = require('graphql');
const express = require('express');
const graphqlHTTP = require('express-graphql');
const {generateSchema} = require('../src/sequelize-graphql-schema')({
    exclude: [ 'Product2' ],
    includeArguments: {
        scopeId: 'int'
    }
});
const models = require('./models');

var app = express()

app.use(
  '/graphql',
  graphqlHTTP({
    schema: new GraphQLSchema(generateSchema(models)),
    graphiql: true
  })
)

app.listen(8080, function() {
  console.log('RUNNING ON 8080')
})
```
