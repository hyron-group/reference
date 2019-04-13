---
description: Used to handle response by default
---

# ResponseHandler

## Why ?

* Cast other data type into string for response
* Response with error track

## Usage

The response handler supports **converting** other **basic data types** to the form that can be responded to the client \(`string` or `Buffer`\)

You can **customize** the data back to the client **using a backware**, or use an **existing backware** is [custom-response](custom_response.md)

| origin type | converted type |
| :--- | :--- |
| primitive type \(string, number, boolean, undefined\) | string |
| Buffer | Buffer |
| object | application/json |
| Error | text/html \(dev env\) |

