HTTPMessage is an inherited Error class, which allows to break the processing thread with a throwable

## Features

-   Allow break processing thread with a 'throw' / reject
-   Loaded as a global var, so you can call anywhere
-   Human readable status code from 1XX - 5XX
-   Support custom status message

# Guide

## 1. Break processing with 'thow'

This is a interested feature of Hyron buildin lib, that allow you break the flow of hyron processing using a throw, or a Promise reject. Such as throw a normal Error

It could be used at every where. But, you need to remember that you need to require 'hyron' first.

Example :

```js
// main-handler
class User {
    ...
    async findUser(name) {
        // mongoose
        var userData = UserModel.findOne(name).exec();
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

## 2. Human readable status code

With StatusCode - a class mapping http code with a readable name, you can easy to choise a code fit you case. Bellow is a code mapping for http

| code  | represent name                   | description                                                                                                      |
| :---: | -------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
|  100  | CONTINUE                         | Server has received the request headers and client should proceed to send the request body                       |
|  101  | SWITCHING_protocol               | Server agreed to switch protocol by client                                                                       |
|  102  | PROCESSING                       | Server has received and is processing the request, but no response is available yet                              |
|  103  | EARLY_HINTS                      | Return some response headers before final HTTP message                                                           |
|  200  | OK                               | Standard response for successful HTTP requests                                                                   |
|  201  | CREATED                          | Resulting in the creation of a new resource                                                                      |
|  202  | ACCEPTED                         | Request has been accepted for processing, but the processing has not been completed                              |
|  203  | NON_AUTHORIZED_INFORMATION       | Transforming proxy server notify that missing auth info                                                          |
|  204  | NO_CONTENT                       | Server success with no response content                                                                          |
|  205  | RESET_CONTENT                    | Response has no content and request client to reset view                                                         |
|  206  | PARTIAL_CONTENT                  | The server is delivering only part of the resource because interrupted download                                  |
|  207  | MULTI_STATUS                     | Body contain a number of separate response codes                                                                 |
|  208  | ALREADY_REPORTED                 | The members of a DAV binding have already been enumerated in a preceding part                                    |
|  226  | IM_USED                          | Response is a representation of the result of one or more instance-manipulations applied to the current instance |
|  300  | MULTIPLE_CHOICES                 |
|  301  | MOVED_PERMANENTLY                |
|  302  | FOUND                            |
|  303  | SEE_OTHER                        |
|  304  | NOT_MODIFIED                     |
|  305  | USE_PROXY                        |
|  306  | SWITCH_PROXY                     |
|  307  | TEMPORARY_REDIRECT               |
|  308  | PERMANENT_REDIRECT               |
|  400  | BAD_REQUEST                      |
|  401  | UN_AUTHORIZED                    |
|  402  | PAYMENT_REQUIRED                 |
|  403  | FORBIDDEN                        |
|  404  | NOT_FOUND                        |
|  405  | METHOD_NOT_ALLOWED               |
|  406  | NOT_ACCEPTABLE: 406,             |
|  407  | PROXY_AUTHORIZED_REQUIRED        |
|  408  | REQUEST_TIMEOUT                  |
|  409  | CONFLICT                         |
|  410  | GONE                             |
|  411  | LENGTH_REQUESTED                 |
|  412  | PRECONDITION_FAILED              |
|  413  | PAYLOAD_TOO_LARGE                |
|  414  | URI_TOO_LONG                     |
|  415  | UNSUPPORTED_MEDIA_TYPE           |
|  416  | RANGE_NOT_SATISFIABLE            |
|  417  | EXPECTATION_FAILED               |
|  418  | I_AM_A_TEAPOT                    |
|  421  | MISDIRECTED_REQUEST              |
|  422  | UN_PROCESSABLE_ENTITY            |
|  423  | LOCKED                           |
|  424  | FAILED_DEPENDENCY                |
|  426  | UPGRADE_REQUIRED                 |
|  428  | PRECONDITION_REQUIRED            |
|  429  | TOO_MANY_REQUESTS                |
|  431  | REQUEST_HEADER_FIELDS_TOO_LARGE  |
|  451  | UN_AVAILABLE_FOR_LEGAL_REASONS   |
|  500  | INTERNAL_SERVER_ERROR            |
|  501  | NOT_IMPLEMENTED                  |
|  502  | BAD_GATEWAY                      |
|  503  | SERVICE_UNAVAILABLE              |
|  504  | GATEWAY_TIMEOUT                  |
|  505  | HTTP_VERSION_NOT_SUPPORTED       |
|  506  | VARIANT_ALSO_NEGOTIATES          |
|  507  | INSUFFICIENT_STORAGE             |
|  508  | LOOP_DETECTED                    |
|  510  | NOT_EXTENDED                     |
|  511  | NETWORK_AUTHENTICATION_REQUESTED |

## 3. Support custom status messange

This is HTTPMessage API. As you see, you can custom messange with args at index 1 (message)

**class HTTPMessage**

> ## constructor HTTPMessange ( code, message ) : Error

Used to create a Error that implement HTTP protocol status

### **params**
- **code** ( number ) : is [http.statusCode](https://nodejs.org/api/http.html#http_response_statuscode)
- **messange** ( string | undefined ) : is [http.statusMessage](https://nodejs.org/api/http.html#http_response_statusmessage)

### **return**
- Error : A object description about a http status
