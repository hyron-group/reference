Custom-response is a default backware plugins that help to pass result from main-handler into server response

\*) note : custom-response is not a global plugins. so, you need to declared it in router if used

## Features

-   Light syntax, easy to tracking
-   Support attributes that are frequently used in [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse)

# Guide

## 1. Light syntax

Hyron was born with the aim of making your source code easily **reusable**. so is the main-handler. Sometimes, we don't use them only once, but sometimes we need to call them in other services. Or, sometimes we need to **test** a function before it is called by the client. This will save time, reduce latency during build and run the program. Full support for http protocol

Example :

```js
class demo {
    static requestConfig(){
        return {
            retrieveImage : {
                method : "get",
                backware : ["custom_response"]
            }
        }
    }

    // used to retrieve image file from server
    retrieveImage() {
        return new Promise(resolve => {
            var file = fs.readFile((err, data) => {
                // custom response type
                resolve({
                    $type: "image/png",
                    $data: data
                });
            });
        });
    }
}
```

So, you see, Basically, to use custom response, you just need to do follow step

1. **Turn it on requestconfig->backware**
   ```js
   backware : ["custom_response"]
   ```
2. **Returns an object containing the description** in the response of the main-handler
   ```js
   // Or used Promise::resolve/async-await if it is async function
   return {
        $type : // response data type
        $data : data // response data
        ...
   }
   ```

## 2. Support commonly used attributes

Custom response supports many types of attributes commonly used in [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse). They are all special attributes, and should be started with a '$' character

Below is a list of supported special attributes :
- **$addTrailers** ( object ) : as [res.addTrailers](https://nodejs.org/api/http.html#http_response_addtrailers_headers)
- **$cookie** ( object )
  - **content** ( object ) : object contain cookie content that will be serializable as headers/Set-Cookie properties
  - **options** ( object ) : object contain options, from [cookie package](https://www.npmjs.com/package/cookie#options-1)
- **$data** ( string | buffer | Array< args > ): as [res.write](https://nodejs.org/api/http.html#http_response_write_chunk_encoding_callback)
- **$end** ( string | buffer | Array< args > ) : as [res.end](https://nodejs.org/api/http.html#http_response_end_data_encoding_callback). But it auto called if this properties has not set
- **$headers** ( object ) : as [res.setHeader](https://nodejs.org/api/http.html#http_response_setheader_name_value)
- **$message** ( string ) : as [res.statusMessage](https://nodejs.org/api/http.html#http_response_statusmessage)
- **$redirect** ( string ) : redirect to a special url
- **$removeHeader** ( string ) : as [res.removeHeader](https://nodejs.org/api/http.html#http_response_removeheader_name)
- **$sendDate** ( boolean ) : as [res.sendDate](https://nodejs.org/api/http.html#http_response_senddate)
- **$response** ( function ) : as function with args at 0 is [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse)
- **$timeout** ( number ) : as [res.setTimeout](https://nodejs.org/api/http.html#http_response_settimeout_msecs_callback)
- **$socket** ( function ) : as function with args at 0 is [http.socket](https://nodejs.org/api/http.html#http_response_socket)
- **$status** ( number ) : as [res.statusCode](https://nodejs.org/api/http.html#http_response_statuscode)
- **$type** ( string ) : as headers/Content-Type
- **$writeHead** ( Array< args > ) : as [res.writeHead](https://nodejs.org/api/http.html#http_response_writehead_statuscode_statusmessage_headers)
- **$writeProcessing** ( boolean ) : true if call [res.writeProcessing](https://nodejs.org/api/http.html#http_response_writeprocessing)
- **$writeContinue** ( boolean ) : true if call [res.writeContinue](https://nodejs.org/api/http.html#http_response_writecontinue)
- **$onClose** ( function ) : a function that handle [event 'close'](https://nodejs.org/api/http.html#http_event_close_1)
- **$onFinish** ( function ) : a function that handle [event 'finish'](https://nodejs.org/api/http.html#http_event_finish)