<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 1) What is GraphQL? ?</div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => GraphQL is a new API standard designed and developed by Facebook. It is an open-source server-side technology that is now maintained by a large community of companies and individuals worldwide. It is also an execution engine that works as a data query language and used to fetch declarative data.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 2) What was the reason behind the development of GraphQL?
 ?</div>

 <div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => GraphQL was initially developed by Facebook as an internal solution for their mobile apps. It was designed to optimize RESTful API calls and provide a flexible, robust, and efficient alternative to REST. It is not a replacement for REST. It is an alternative to writing APIs using REST.

After its release, it has become prevalent among developers and is also a popular solution for building web services along with REST.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 3) What are the top companies that use GraphQL?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => There are many big organizations such as Facebook, Github, Pinterest, Intuit, coursera, shopify, dailymotion, yelp etc. that uses GraphQL. Actually GraphQL was designed and developed by Facebook itself.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 4) What are the most significant advantages of using GraphQL over REST?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => A list of the most significant advantages of using GraphQL over REST:

There is only one endpoint in GraphQL, but REST has multiple endpoints. That's why GraphQL is more cost-effective than REST. You don't have to use your resources for various endpoints.
In REST API, you have to use multiple requests to retrieve a complex data-set, but in GraphQL, you can execute a complex query easily in just a single request.
You can change the request data format in GraphQL, but it is not possible to do the same in REST.
The development speed in GraphQL is faster than REST.
GraphQL provides high consistency across all platforms, while In REST, it is hard to get consistency across all platforms.
GraphQL doesn't support an automatic caching system, while REST uses caching automatically.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.5 What is the use of resolver in GraphQL?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => In GraphQL, a resolver is used to handle queries and produce a response to the GraphQL query.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 🔹 6. What is GraphQL schema?</div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Every GraphQL server has two core parts that determine how it works: a schema and resolve functions.

The schema is a model of the data that can be fetched through the GraphQL server. It defines what queries clients are allowed to make, what types of data can be fetched from the server, and what the relationships between these types are.

```json

type Author {
  id: Int
  name: String
  posts: [Post]
}
type Post {
  id: Int
  title: String
  text: String
  author: Author
}
type Query {
  getAuthor(id: Int): Author
  getPostsByTitle(titleContains: String): [Post]
}
schema {
  query: Query
}
```

</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.7  What is Query? </div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => A query is used to read data. Similar to the GET request of REST APIs, we can fetch data from a GraphQL server using a query.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 8. What do you mean by over-fetching in the GraphQL language?
</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. =>

Over fetching is basically a condition in GraphQL where the requested client gets more data than what was requested. This will result in an increase in the payload size.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua. 9. What do you mean by under-fetching in the GraphQL language?
</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Under fetching is basically the exact opposite of over-fetching. It happens when the requested client does not get enough data and you are forced to send multiple calls to get the desired data. 
</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.10 What is mutation?</div>

<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Mutation is used for the write operation. A mutation is used for operations like add, delete and edit data.</div>

<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.11 How can you use variables in a query  ?</div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Instead of writing arguments in a query string, we can use variables and pass any arguments to these queries directly. For example :

```json
{
student(id: "100")
{
name
age
}
}
```

.</div>


<div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.12 How can you use variables in a query  ?</div>
<div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Instead of writing arguments in a query string, we can use variables and pass any arguments to these queries directly. For example :

```json
query studentQuery($id : Int)
{
student(id : $id){
name
}
}
```
</div>

 <div style="color:green;font-size:14px;text-transform: Capitalize;">Qua.13  What is a resolver ?</div>

 <div style="color:white;font-size:12px;text-transform: Capitalize;">Ans. => Resolver is used to produce a response to a GraphQL query. Resolver is used to handle queries.</div>