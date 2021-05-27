[![npm version](https://badge.fury.io/js/http-to-curl.svg)](https://badge.fury.io/js/http-to-curl)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)
![Depedencies](https://david-dm.org/drgx/http-to-curl.svg)
[![Build Status](https://travis-ci.org/drgx/http-to-curl.svg?branch=master)](https://travis-ci.org/drgx/http-to-curl)

# Node js HTTP request to cURL

Tired to manually generate curl from nodejs request for debugging proposes? Need to export nodejs request to your REST client (e.g. [Insomnia](https://insomnia.rest/) and [Postman](https://www.getpostman.com/))? http-to-curl come to the rescue!!

## Usage 📚

```js
// import httpToCurl on your server entry point of your project or code (e.g. server.js / index.js)
import httpToCurl from 'http-to-curl';
httpToCurl();

// Traditional way
const httpToCurl = require('http-to-curl').default;
httpToCurl();

//  Use your favorite http client to fetch (e.g. axios, isomorphic fetch or even vanilla request) all works well with http-to-curl.
//  In this example we are using axios.

import axios from 'axios'
const options = {
  url: 'https://jsonplaceholder.typicode.com/posts/1',
  method: 'get'
};

//Output
curl "https://jsonplaceholder.typicode.com/posts/1" -X GET -H "Accept: application/json, text/plain, */*" -H "User-Agent: axios/0.18.0"
```

It will listen all your nodejs http request and generate curl for each request. Its support all method (GET, POST, PUT, DELETE & PATCH)

# Options

## 1. Filtering ✅

`http-to-curl` support filtering url using regex and string. Only match url will be generated.

```js
import httpToCurl from "http-to-curl";
//Single url match
const options = {
  filter: /api\/v1/,
};
httpToCurl(options);
//Multiple url match
const options = {
  filter: [/api\/v1/, /api\/v3/],
};
httpToCurl(options);
```

## 2. Custom callback ⚙️

```js
const options = {
  customCallback: function (curlString) {
    console.log("hey this is the custom callback", curlString);
  },
};
httpToCurl(options);
```

## About this fork

This repo was forked to:

- Add support for search params in urls.
- Fix a bug where the [https://www.npmjs.com/package/got](got) library does not work.
