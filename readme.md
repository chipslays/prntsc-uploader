# Lightshot Uploader ([prnt.sc](https://prnt.sc/))

[![Tests](https://github.com/chipslays/prntsc-uploader/actions/workflows/tests.yml/badge.svg)](https://github.com/chipslays/prntsc-uploader/actions/workflows/tests.yml)
![Packagist Version](https://img.shields.io/packagist/v/chipslays/prntsc-uploader)

Easy upload screenshots to Lightshot (prnt.sc).

## Installation

```bash
$ composer require chipslays/prntsc-uploader
```

## Usage

For unlimited uploading without ban, you need get a `client_id` and `client_secret` [Imgur API](https://apidocs.imgur.com/).

#### `upload(string $file): array`

Upload image to prnt.sc by local file or url.

```php

use Imgur\Client;
use Prntsc\Uploader;

require_once 'vendor/autoload.php';

$client = new Client;
$client->setOption('client_id', '48b6xxxxxxxxxxx');
$client->setOption('client_secret', 'fd5048fxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx');

$prntsc = new Uploader($client);

$response = $prntsc->upload('images/arnold.jpg');

print_r($response);

Array
(
    [ok] => 1
    [result] => Array
        (
            [prntsc] => http://prntscr.com/wnthmb
            [imgur] => https://i.imgur.com/FXjRMZ4.jpg
            [cache] => {"jsonrpc":"2.0","method":"save","id":"1","params":{"img_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","thumb_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","delete_hash":"FyUDDstquzhymYK","app_id":"{813F8739-7DC3-7EFFF9F0E13F}","width":500,"height":383,"dpr":"1"}}
        )

)
```

#### `uploadFromCache(string $cache): array`

Upload image to prnt.sc from cache.

```php

use Prntsc\Uploader;

require_once 'vendor/autoload.php';

$response = (new Uploader)->uploadFromCache('{"jsonrpc":"2.0","method":"save","id":"1","params":{"img_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","thumb_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","delete_hash":"FyUDDstquzhymYK","app_id":"{813F8739-7DC3-7EFFF9F0E13F}","width":500,"height":383,"dpr":"1"}}');

print_r($response);

// NOTE: imgur null, because result taken from cache.
Array
(
    [ok] => 1
    [result] => Array
        (
            [prntsc] => http://prntscr.com/wntjmx
            [imgur] =>
            [cache] => {"jsonrpc":"2.0","method":"save","id":"1","params":{"img_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","thumb_url":"https:\/\/i.imgur.com\/FXjRMZ4.jpg","delete_hash":"FyUDDstquzhymYK","app_id":"{813F8739-7DC3-7EFFF9F0E13F}","width":500,"height":383,"dpr":"1"}}
        )

)
```


## Disclaimer
This repository is for educational purposes only.

Dont abuse, the owner of the repository does not bear any responsibility for the harm caused by this repository.
