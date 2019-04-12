---
description: >-
  Custom-response is a default backware plugins that help to pass result from
  main-handler into server response
---

# custom\_response

## Why ?

* **Custom response** for client
* **Friendly output**

## Usage

### 1. Declare plugins

{% hint style="info" %}
You need to declare this plugins to uses
{% endhint %}

```javascript
backware : ["custom_response"]
```

{% code-tabs %}
{% code-tabs-item title="Example" %}
```javascript
static requestConfig(){
    return {
        retrieveImage : {
            method : "get",
            backware : ["custom_response"]
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 2. Using plugins

```javascript
// Or used Promise::resolve/async-await if it is async function
return {
     $type : // response data type
     $data : data // response data
     ...
}
```

{% code-tabs %}
{% code-tabs-item title="Example" %}
```javascript
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
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Features

### 1. Support commonly used attributes

Custom response supports many types of attributes commonly used in [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse). They are all special attributes, and should be started with a '$' character

Below is a list of supported special attributes

<table>
  <thead>
    <tr>
      <th style="text-align:left">name</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">$addTrailers</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_addtrailers_headers">res.addTrailers</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$cookie</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li><b>content</b> ( object ) : object contain cookie content that will be
            serializable as headers/Set-Cookie properties</li>
          <li><b>options</b> ( object ) : object contain options, from <a href="https://www.npmjs.com/package/cookie#options-1">cookie package</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$data</td>
      <td style="text-align:left">string | buffer | Array&lt;args&gt;</td>
      <td style="text-align:left">as res.write</td>
    </tr>
    <tr>
      <td style="text-align:left">$end</td>
      <td style="text-align:left">string | buffer | Array&lt;args&gt;</td>
      <td style="text-align:left">as res.end. But it auto called if this properties has not set</td>
    </tr>
    <tr>
      <td style="text-align:left">$headers</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_setheader_name_value">res.setHeader</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$message</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_statusmessage">res.statusMessage</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$redirect</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">redirect to a special url</td>
    </tr>
    <tr>
      <td style="text-align:left">$removeHeader</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_removeheader_name">res.removeHeader</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$sendDate</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_removeheader_name">res.removeHeader</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$response</td>
      <td style="text-align:left">function</td>
      <td style="text-align:left">as function with args at 0 is <a href="https://nodejs.org/api/http.html#http_class_http_serverresponse">http.ServerResponse</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$timeout</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_settimeout_msecs_callback">res.setTimeout</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$socket</td>
      <td style="text-align:left">function</td>
      <td style="text-align:left">as function with args at 0 is <a href="https://nodejs.org/api/http.html#http_response_socket">http.socket</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$status</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_statuscode">res.statusCode</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">as headers/Content-Type</td>
    </tr>
    <tr>
      <td style="text-align:left">$writeHead</td>
      <td style="text-align:left">Array&lt;args&gt;</td>
      <td style="text-align:left">as <a href="https://nodejs.org/api/http.html#http_response_writehead_statuscode_statusmessage_headers">res.writeHead</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$writeProcessing</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">true if call <a href="https://nodejs.org/api/http.html#http_response_writeprocessing">res.writeProcessing</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$writeContinue</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">true if call <a href="https://nodejs.org/api/http.html#http_response_writecontinue">res.writeContinue</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$onClose</td>
      <td style="text-align:left">function</td>
      <td style="text-align:left">a function that handle <a href="https://nodejs.org/api/http.html#http_event_close_1">event &apos;close&apos;</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">$onFinish</td>
      <td style="text-align:left">function</td>
      <td style="text-align:left">a function that handle <a href="https://nodejs.org/api/http.html#http_event_finish">event &apos;finish&apos;</a>
      </td>
    </tr>
  </tbody>
</table>