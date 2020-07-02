---
layout: page
title: PHP
parent: Example code
permalink: /php/
description: >-
  Convert HTML to an image (png, jpg or webp) with PHP + the HTML/CSS to Image
  API. Renders exactly like Google Chrome.
---
{% include intro.md language="PHP" %}


```php
{% include_snippet everything from snippets/plain_php.php %}
```

## PHP example with Guzzle library

Using an HTTP library such as [Guzzle](https://github.com/guzzle/guzzle) can simplify your code even further. Here's an example of how to use the HTML/CSS to Image API with Guzzle.

Installation instructions for Guzzle are [here](https://github.com/guzzle/guzzle#installing-guzzle).

```php
<?php
require 'vendor/autoload.php';

$html = "<div class='ping'>Pong ✅</div>";
$css = ".ping { padding: 20px; font-family: 'sans-serif'; }";

$client = new GuzzleHttpClient();
// Retrieve your user_id and api_key from https://htmlcsstoimage.com/dashboard
$res = $client->request('POST', 'https://hcti.io/v1/image', [
  'auth' => ['user_id', 'api_key'],
  'form_params' => ['html' => $html, 'css' => $css]
]);

echo $res->getBody();
// {"url":"https://hcti.io/v1/image/5803a3f0-abd3-4f56-9e6c-3823d7466ed6"}
?>
```

The code turns out to be a bit more readable and less complex when using Guzzle. A great option if you're open to adding the library to your project.

### More examples

This page showed really simple image examples. The API can render anything that Google Chrome can. For more advanced examples, [take a look here](../#examples).

### Need help?

Email us **support@htmlcsstoimage.com**

Share with us what you're building. We're experts at generating images and love to help.

