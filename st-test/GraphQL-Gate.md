[GraphQL入门：非常简单](https://www.jianshu.com/p/9c1a2cd30993)
node index.js 
 ``` 
 
const graphqlHTTP = require('express-graphql').graphqlHTTP;
``` 

npm run cli-client http://localhost:4000/graphql
在 package.json 中有以下的记述
``` 

"scripts": {
		"start": "babel-node src/server.js",
		"cli-client": "node index2.js"
	},
```
```
// index.js
const express = require('express');
const app = express();

const graphqlHTTP = require('express-graphql');
const { buildSchema } = require('graphql');

app.get('/', function(req, res) {
  res.send('Express is working!')
});


let schema = buildSchema(`
  type Query {
    hello: String
  }
`);


let root = {
  hello: function() {
    return 'Hello world!';
  },
  test: function() {
    return 'test!';
  },
}


app.use('/graphql', graphqlHTTP({
  schema: schema,
  rootValue: root,
  graphiql: true,
}));

app.listen(4000, function() {
  console.log('Listening on port 4000')
});

```

GraphQL第2个例子
```
var express = require('express');
var graphqlHTTP = require('express-graphql');
var { buildSchema } = require('graphql');
 
//定义schema
var schema = buildSchema(`
    type User{
        name: String
        sex: String
        intro: String
    }
    type Query {
        user:User
    }
`);
 
//定义服务端数据
var root= {
    user: {
        name: 'username',
        sex: '男',
        intro: '资深码农'
    }
};
 
var app = express();
app.use('/graphql', graphqlHTTP({
    schema: schema,
    rootValue: root,
    graphiql: true, //启用GraphiQL
}));
app.listen(4000, () => console.log('请在浏览器中打开地址：http://localhost:4000/graphql'));

```
测试
```
{
  user  
}
```