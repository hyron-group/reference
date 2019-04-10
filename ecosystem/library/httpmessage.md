# HTTPMessage

HTTPMessage is an inherited Error class, which allows to break the processing thread with a throwable

### Features

* Allow break processing thread with a 'throw' / reject
* Loaded as a global var, so you can call anywhere
* Human readable status code from 1XX - 5XX
* Support custom status message

## Details

### 1. Break processing with 'thow'

This is a interested feature of Hyron buildin lib, that allow you break the flow of hyron processing using a throw, or a Promise reject. Such as throw a normal Error

It could be used at every where. But, you need to remember that you need to require 'hyron' first.

Example :

```javascript
// main-handler
class User {
    ...
    async findUser(name) {
        // mongoose
        var userData = await UserModel.findOne(name).exec();
        if(userData==null) {
            // That it
            throw new HTTPMessage(
                StatusCode.NOT_FOUND, 
                "not found user with name : "+name);
        }

        return userData;
    }
}
```

### 2. Human readable status code

With StatusCode - a class mapping http code with a readable name, you can easy to choise a code fit you case. Bellow is a code mapping for http

| code | represent name | description |
| :---: | :--- | :--- |
| 100 | CONTINUE | Server has received the request headers and client should proceed to send the request body |
| 101 | SWITCHING\_PROTOCOL | Server agreed to switch protocol by client |
| 102 | PROCESSING | Server has received and is processing the request, but no response is available yet |
| 103 | EARLY\_HINTS | Return some response headers before final HTTP message |
| 200 | OK | Standard response for successful HTTP requests |
| 201 | CREATED | Resulting in the creation of a new resource |
| 202 | ACCEPTED | Request has been accepted for processing, but the processing has not been completed |
| 203 | NON\_AUTHORIZED \_INFORMATION | Transforming proxy server notify that missing auth info |
| 204 | NO\_CONTENT | Server success with no response content |
| 205 | RESET\_CONTENT | Response has no content and request client to reset view |
| 206 | PARTIAL\_CONTENT | The server is delivering only part of the resource because interrupted download |
| 207 | MULTI\_STATUS | Body contain a number of separate response codes |
| 208 | ALREADY\_REPORTED | The members of a DAV binding have already been enumerated in a preceding part |
| 226 | IM\_USED | Response is a representation of the result of one or more instance-manipulations applied to the current instance |
| 300 | MULTIPLE\_CHOICES | Indicates that is client could choice multi options for the resource |
| 301 | MOVED\_PERMANENTLY | This and all future requests should be directed to the given URI |
| 302 | FOUND | Tells the client to look at \(browse to\) another URL |
| 303 | SEE\_OTHER | The response to the request can be found under another URI using the GET method |
| 304 | NOT\_MODIFIED | Indicates that the resource has not been modified since the version specified by the request headers |
| 305 | USE\_PROXY | The requested resource is available only through a proxy |
| 306 | SWITCH\_PROXY | Subsequent requests should use the specified proxy |
| 307 | TEMPORARY\_REDIRECT | The request should be repeated with another URI for temporary |
| 308 | PERMANENT\_REDIRECT | The request and all future requests should be repeated using another URI |
| 400 | BAD\_REQUEST | The server cannot or will not process the request due to an apparent client error |
| 401 | UN\_AUTHORIZED | Similar to 403 Forbidden, but specifically for use when authentication is required and has failed or has not yet been provided |
| 402 | PAYMENT\_REQUIRED | The original intention was that this code might be used as part of some form of digital cash or micropayment scheme |
| 403 | FORBIDDEN | The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort |
| 404 | NOT\_FOUND | The requested resource could not be found but may be available in the future |
| 405 | METHOD\_NOT\_ALLOWED | A request method is not supported for the requested resource |
| 406 | NOT\_ACCEPTABLE | The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request |
| 407 | PROXY\_AUTHORIZED \_REQUIRED | The client must first authenticate itself with the proxy |
| 408 | REQUEST\_TIMEOUT | The server timed out waiting for the request |
| 409 | CONFLICT | the request could not be processed because of conflict in the current state of the resource |
| 410 | GONE | Resource requested is no longer available and will not be available again |
| 411 | LENGTH\_REQUESTED | The request did not specify the length of its content, which is required by the requested resource |
| 412 | PRECONDITION\_FAILED | The server does not meet one of the preconditions that the requester put on the request |
| 413 | PAYLOAD\_TOO\_LARGE | The request is larger than the server is willing or able to process |
| 414 | URI\_TOO\_LONG | The URI provided was too long for the server to process |
| 415 | UNSUPPORTED \_MEDIA\_TYPE | The request entity has a media type which the server or resource does not support |
| 416 | RANGE\_NOT\_SATISFIABLE | The client has asked for a portion of the file, but the server cannot supply that portion |
| 417 | EXPECTATION\_FAILED | The server cannot meet the requirements of the Expect request-header field |
| 418 | I\_AM\_A\_TEAPOT | This HTTP status is used as an Easter egg in some websites |
| 421 | MISDIRECTED\_REQUEST | The request was directed at a server that is not able to produce a response |
| 422 | UN\_PROCESSABLE\_ENTITY | The request was well-formed but was unable to be followed due to semantic errors |
| 423 | LOCKED | The resource that is being accessed is locked |
| 424 | FAILED\_DEPENDENCY | The request failed because it depended on another request and that request failed |
| 426 | UPGRADE\_REQUIRED | The client should switch to a different protocol |
| 428 | PRECONDITION\_REQUIRED | The origin server requires the request to be conditional |
| 429 | TOO\_MANY\_REQUESTS | The user has sent too many requests in a given amount of time |
| 431 | REQUEST\_HEADER\_FIELDS \_TOO\_LARGE | The server is unwilling to process the request because either an individual header field, or all the header fields collectively, are too large |
| 451 | UN\_AVAILABLE\_FOR \_LEGAL\_REASONS | A server operator has received a legal demand to deny access to a resource or to a set of resources that includes the requested resource |
| 500 | INTERNAL\_SERVER\_ERROR | A generic error message, given when an unexpected condition was encountered and no more specific message is suitable |
| 501 | NOT\_IMPLEMENTED | The server either does not recognize the request method, or it lacks the ability to fulfil the request |
| 502 | BAD\_GATEWAY | The server was acting as a gateway or proxy and received an invalid response from the upstream server |
| 503 | SERVICE\_UNAVAILABLE | The server is currently unavailable \(for temporary\) |
| 504 | GATEWAY\_TIMEOUT | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server |
| 505 | HTTP\_VERSION \_NOT\_SUPPORTED | The server does not support the HTTP protocol version used in the request |
| 506 | VARIANT\_ALSO \_NEGOTIATES | Transparent content negotiation for the request results in a circular reference |
| 507 | INSUFFICIENT\_STORAGE | The server is unable to store the representation needed to complete the request |
| 508 | LOOP\_DETECTED | The server detected an infinite loop while processing the request |
| 510 | NOT\_EXTENDED | Further extensions to the request are required for the server to fulfil it |
| 511 | NETWORK\_AUTH \_REQUESTED | The client needs to authenticate to gain network access |

### 3. Support custom status messange

This is HTTPMessage API. As you see, you can custom messange with args at index 1 \(message\)

**class HTTPMessage**

> ### constructor **HTTPMessage** \( code, message \) : Error

Used to create a Error that implement HTTP protocol status

#### **params**

* **code** \( number \) : is [http.statusCode](https://nodejs.org/api/http.html#http_response_statuscode)
* **messange** \( string \| undefined \) : is [http.statusMessage](https://nodejs.org/api/http.html#http_response_statusmessage)

#### **return**

* Error : A object description about a http status

