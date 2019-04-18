---
description: >-
  Param-parser is a default frontware plugins supported by Hyron. That help pass
  params from request into handler function that automatically
---

# param\_parser



### Why ?

* **Save time** by automating
* **Easy to edit**
* H**elp simplify** executer
* Makes **executer reusable**

## Usage

param-parser is a hyron **global frontware** plugins. You **do not need to declare** it. Just use it with the features it supports

1. Auto **pass params** from request
2. **Pass arg list** to this scope

```javascript
export class api {
    static requestConfig(){
        return {
            uploadFile : {
                method : "get",
                params: "/:name",
            }
        }
    }

// 
     uploadFile(name, $raw){
        // POST /api/upload-file/:name
        // with raw body type
        return fs.writeFile("/upload/"+name, $raw);
    }
}
```



## Features

### 1. Auto pass payload data

With `param_parser`, it will be **automatically** loaded as executer input

```javascript
export class api {
    static requestConfig(){
        return {
            demo : {
                method : "get",
                params : "/:a"
            }
        }
    }

    demo(a, b){
        // do something useful
        return `hello ${a}, i'm ${b}`;
    }
}    
```

To use param-parser you need to follow the following rules

* **With query type** \(get, head\) : The data needs to be declared on the query part of the request. Example : `/search?keyword=audi`
* **With body type** \(post, put, patch\) : The data needs to be declared on the body part of the request.
* **With param type** : You need to specify the **dynamic part** of the url to be used as the params section, by declaring the **params** or **path** attribute in `requestConfig`. Example : `/search/:name/age/:age`
* **Use special variables** to pass fields from the request

### 2. Support special field

In addition to passing data from the query, body, params, you can also pass the commonly used parameters in request as input parameters, such as:

| argument | type | description |
| :--- | :--- | :--- |
| $req | [IncomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage) | contains information about client requests |
| $res | [ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse) | contains information about server response |
| $socket | [req.socket](https://nodejs.org/api/http.html#http_message_socket) | socket to connect between client and server |
| $trailers | [req.trailers](https://nodejs.org/api/http.html#http_message_trailers) | contains information about client trailers |
| $events | req.on | used to attach events to requests |
| $cookie | object | as object parser from req.headers.cookie |
| $query | object | parse query from url into a object |
| $urlencoded | object | parse body data as url-encoded data type into a object |
| $multipart | object | parse body data as multi-part data type into a object |
| $raw | Buffer | parse body data as raw data type |

To used special variables \( start with '$' character \) mentioned above, you need to include it in main-handler method arguments

```javascript
demo ($cookie, b) {
    ...
}
```

### 3. Dynamic data type

what if you want to use a complex data type like array, or object for some reason like :

```http
/search/audi?filter={color:yellow,location:usa,cost:{from:10000,to:300000}}&sort=[name,date]
```

The good news is that Hyron supports this 😆

Hyron supports the included parser to analyze a string into javascript native types with high-performance, including: **number**, **string**, **boolean**, **array**, **object**

You can find it in : [Hyron/lib/objectParser](https://github.com/Hyron-group/Hyron/blob/master/lib/objectParser.js)

And in server. That it !

```javascript
// in server
search(name, filter, sort){
    // do something useful
}
```

param-parser also supports uploading files by default if content-type = multipart by [Busboy](https://www.npmjs.com/package/busboy) engine

