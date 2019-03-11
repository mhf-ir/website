---
id: more-pushmsg
title: (more) Push message examples
---

Have a look at [Here](pushmsg.md) for "How to obtain an application token".

NOTE: Assuming Gotify is running on `http://localhost:8008`.

### Node.JS

```js
const fs = require('fs'); // for read ca certificate
const request = require('request'); // npm i request

request(
  {
    uri: 'http://localhost:8008/message?token=<apptoken>',    
    method: 'POST',
    json: {
      message: 'Well hello there. ',
      priority: 2,
      title: 'This is my title',
    },
    agentOptions: {
      ca: fs.readFileSync('path/to/ca.public.pem'),
    },
  },
  (error, response, body) => {
    //
  },
);
```

### PHP

#### CURL
```php
<?php
$message = [
    "message" => "Well hello there.",
    "priority" => 2,
    "title" => "This is my title",
];
$messageString = json_encode($message);

$ch = curl_init('http://localhost:8008/message?token=<apptoken>');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $messageString);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
]);

$result = curl_exec($ch);
```

#### Guzzle
```php
use GuzzleHttp\Client; // php composer.phar require guzzlehttp/guzzle:~6.0

$message = [
  "message" => "Well hello there.",
  "priority" => 2,
  "title" => "This is my title",
];

$client = new Client();
$client->request('POST', 'http://localhost:8008/message', [
  'query' => [
    'token' => '<apptoken>',
  ],
  'json' => $message,
]);
```

### Python

```python
import requests #pip install requests
resp = requests.post('http://localhost:8008/message?token=<apptoken>', json={
    "message": "Well hello there.",
    "priority": 2,
    "title": "This is my title"
})
```

### Golang

```go
package main

import (
        "net/http"
        "net/url"
)

func main() {
    http.PostForm("http://localhost:8008/message?<apptoken>",
        url.Values{"message": {"My Message"}, "title": {"My Title"}})
}
```
