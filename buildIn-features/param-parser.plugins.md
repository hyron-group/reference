# Plugins param-parser

Param-parser is a default fontware plugins supported by Hyron. That help pass params from request into handler function

## Features

-   **Pass params from request** to main-handler function. Turn a processing logic function into a router
-   Support **fully method**, include : get, head, post, put, patch
-   **Pass often used request field** into main-handler
-   **Dynamic data type** in request, include : string, number, boolean, array, object
-   High performance passing

# Details

## 1. Pass params from request

With the traditional way (using express), to access a variable from the request, you often use the syntax as :

```js
// ExpressJS
app.get("/api/demo/:a",(req, res)=>{
    var a = req.params.a;
    var b = req.query.b;
    ...
    // do something useful
    res.end(`hello ${a}, i'm ${b}`);
})
```

even more complicated if you want to get a file from the request, or multipart data from the body, etc

Repeating the same syntax
In many of your different routers, it is indeed an extremely annoying problem. it's not just a boring, time-consuming task, but it makes your code odd and heavy when you have to spend part of the space just declaring the variable from the request.

Imagine you are working with an application with hundreds, thousands of different routers, and your job is to edit and optimize them. like renaming a variable, putting a variable from the header into a cookie, or adding some logic. It is scary. When you are in the hands of an extremely confusing mixture

And that is why this plugins came into being. It helps you to automate the separation of variables from requests. 

With param-parser, now you can not only shorten the application development time by having the main function variable contain processing logic into a function, it also helps your source code become cleaner, and easier to change, upgrade if new requirements are available

```js
export class api {
    static requestConfig(){
        return {
            demo : {
                method : "get",
                params : "/:a"
            }
        }
    }

    ...
    demo(a, b){
        // do something useful
        return `hello ${a}, i'm ${b}`;
    }
}
```

As you can see, it's extremely easy, isn't it? This is one of the features supported by the hyron, so you don't need to declare any more syntax

In addition, param-parser also supports some other interesting features such as bellow

## 2. Support fully method

param-parser supports separating variables from requests through :
- **Query in Request** : for GET, HEAD method
- **Body in Request** : for POST, PUT, PATCH
- **Params in Path** : need to be declared in the params attribute in requestConfig according to the syntax : /:param_name

## 3. Pass often used request field
In addition to passing data from the query, body, params, you can also pass the commonly used parameters in request as input parameters, such as:

- **$req** : as [http.IncomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage)
- **$res** : as [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse)
- **$headers** : as [req.headers](https://nodejs.org/api/http.html#http_message_headers)
- **$socket** : as [req.socket](https://nodejs.org/api/http.html#http_message_socket)
- **$trailers** : as [req.trailers](https://nodejs.org/api/http.html#http_message_trailers)
- **$events** : as req.on
- **$cookie** : as object parser from req.headers.cookie
- **$body** : as raw body type for method POST, PUT, PATCH

To used special variables ( start with '$' character ) mentioned above, you need to include it in main-handler method arguments

```js
demo($cookie, b){
    ...
}
```

## 4. Dynamic data type

what if you want to use a complex data type like array, or object for some reason like :

```http
GET http://localhost/search/audi?filter={color:yellow,location:usa,cost:{from:10000,to:300000}}&sort=[name,date]
```

The good news is that Hyron supports this 😆

Hyron supports the included parser to analyze a string into  javascript native types with high-performance, including: **number**, **string**, **boolean**, **array**, **object**

You can find it in : [hyron/lib/objectParser](https://github.com/hyron-group/hyron/blob/master/lib/objectParser.js)

And in server. That it !
```js
// in server
search(name, filter, sort){
    // do something useful
}
```

param-parser also supports uploading files by default if content-type = multipart by [Busboy](https://www.npmjs.com/package/busboy) engine
