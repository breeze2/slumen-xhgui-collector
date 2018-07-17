# slumen-xhgui-collector
an xhgui collector in [slumen](https://github.com/breeze2/slumen)

## config

```php
<?php
// xhgui_config.php
return [
    'debug' => false,
    'mode' => 'development',

    'save.handler' => 'mongodb',
    'db.host' => 'mongodb://127.0.0.1:27017',
    'db.db' => 'xhprof',

    'db.options' => array(),
    'templates.path' => dirname(__DIR__) . '/src/templates',
    'date.format' => 'M jS H:i:s',
    'detail.count' => 6,
    'page.limit' => 25,

    'profiler.enable' => function() {
        return rand(1, 100) === 42;
    },
    'profiler.simple_url' => function($url) {
        return preg_replace('/\=\d+/', '', $url);
    },
    'profiler.options' => array(),

];
```

## usage

```php
<?php
// in slumen
// swoole http server onRequest
$server->onRequest($request, $response) {
    $xhguiCollector = new XhguiCollector('/path/to/xhgui_config.php');
    $xhguiCollector->setInfo($request->server['request_uri'], $request->get, $request->server);

    $xhguiCollector->collectorEnable(); // start collecting

    // do something

    $xhguiCollector->collectorDisable(); // stop collecting
};

```

