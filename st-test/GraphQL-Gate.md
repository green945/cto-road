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

const graphqlHTTP = require('express-graphql').graphqlHTTP;
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
var graphqlHTTP = require('express-graphql').graphqlHTTP;
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


GraphQL第3个例子

data.json
 ```
{
  "1": {
    "id": "1",
    "name": "Dan"
  },
  "2": {
    "id": "2",
    "name": "Marie"
  },
  "3": {
    "id": "3",
    "name": "Jessie"
  }
}
```

index3.js

 ```
// Import the required libraries
var graphql = require('graphql');
var graphqlHTTP = require('express-graphql').graphqlHTTP;
var express = require('express');
var data = require('./data.json');
 
 
var userType = new graphql.GraphQLObjectType({
  name: 'User',
  fields: {
    id: { type: graphql.GraphQLString },
    name: { type: graphql.GraphQLString },
  }
});
 
var schema = new graphql.GraphQLSchema({
  query: new graphql.GraphQLObjectType({
    name: 'Query',
    fields: {
      user: {
        type: userType,
        // `args` describes the arguments that the `user` query accepts
        args: {
          id: { type: graphql.GraphQLString }
        }, 
        resolve: function (_, args) {
          return data[args.id];
        }
      }
    }
  })
});
 
express()
  .use('/graphql', graphqlHTTP({ schema: schema, pretty: true }))
  .listen(4000); 
console.log('GraphQL server running on http://localhost:4000/graphql');
``` 
test 
```
{user(id:"1"){name}}

[test](http://192.168.1.9:4000/graphql?query={user(id:"1"){name}}
```


Setup an HTTP Server:构建一个HTTP服务器
[构建一个HTTP服务器](https://blog.csdn.net/hxpjava1/article/details/78263911?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-7)

 待完成

 [GraphQL 中文文档](http://www.mianshigee.com/tutorial/graphql-zh/ec2f2575c49a7954.md)
 待理解
