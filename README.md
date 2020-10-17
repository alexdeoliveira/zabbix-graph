# 📈 PHP Zabbix Graph

Get a graph from Zabbix to display on a webpage or save to a file. If you are using Laravel, then please check out [this repository](https://github.com/alexdeoliveira/laravel-zabbix-graph). 

## Original Package
https://github.com/casperboone/zabbix-graph

## Installation
You can install the package via composer:

``` bash
composer require alexdeoliveira/zabbix-graph
```

Require Composer's autoload (probably already done):
```php
require __DIR__.'/../vendor/autoload.php';
```


## Usage
### Basic Usage
You can create an instance of `Alexdeoliveira\ZabbixGraph` and pass the full URL to your Zabbix installation, the username and the password through the constructor. On this instance you can get a graph from Zabbix by calling `->find($graphId)`. Graph IDs can be found in the URL of the Zabbix UI of a certain graph.

Example:
```php
$zabbixGraph = new Alexdeoliveira\ZabbixGraph('http://my-zabbix.com', 'username', 'passsword');

$zabbixGraph->width(500)
    ->height(300)
    ->find(54);
```

The output of find is a binary image that can be saved to a file or converted to an HTTP response.

### Available Methods
The following methods are available to adjust the parameters of the graph:

| Method                          | Description                                                |
| ------------------------------- | ---------------------------------------------------------- |
| `->width(int $width)`           | The width of the graph in pixels*                          |
| `->height(int $width)`          | The height of the graph in pixels*                         |
| `->startTime(DateTime $start)`  | The start date and time of the data displayed in the graph |
| `->endTime(DateTime $end)`      | The end date and time of the data displayed in the graph   |

_* The graph that Zabbix returns is usually slightly bigger because of added legends or labels_
### Old Zabbix versions
If you're using Zabbix 1.8 or older, then you need to set the last parameter of the constructor to `true`. 

Example:
```php
$zabbixGraph = new Alexdeoliveira\ZabbixGraph('http://my-zabbix.com', 'username', 'passsword', true);
```