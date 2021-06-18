# DB Draw

**Generate an ER diagram from your existing database.**

## How to use

Because **DB Draw** is a library, you have to use it as a dependency and instantiate it in your project.

In order to create a diagram you have to follow these steps:

1. Your application must provide a valid [doctrine/dbal](https://github.com/doctrine/dbal) connection.
2. Instantiate `\Jawira\DbDraw\DbDraw` using your _dbal connection_.
3. Choose your diagram size (`mini`, `midi`, `maxi`) and call `DbDraw::generatePuml`.
4. Then `DbDraw::generatePuml` will return a [PlantUML diagram](https://plantuml.com/ie-diagram).
5. Is up to you to convert the _puml_ diagram to another image format (e.g. _png_ or _svg_). I suggest to
   use [jawira/plantuml-client](https://github.com/jawira/plantuml-client).

Example:

```php
use Doctrine\DBAL\Connection;
use Jawira\DbDraw\DbDraw;
use Jawira\PlantUmlClient\{Client, Format};

// Write some logic here to retrieve $connection

// Generating PlantUML diagram
/** @var Connection $connection */
$dbDiagram = new DbDraw($connection);
$puml      = $dbDiagram->generatePuml(DbDraw::MIDI);
file_put_contents('database.puml', $puml);

// Converting & saving png image
$client = new Client();
$png    = $client->generateImage($puml, Format::PNG);
file_put_contents('database.png', $png);
```

## Diagram sizes

```php
$dbDraw = new DbDraw($connection);
$miniDiagram = $dbDraw->generatePuml(DbDraw::MINI); // only table names
$midiDiagram = $dbDraw->generatePuml(DbDraw::MIDI); // like mini with columns
$maxiDiagram = $dbDraw->generatePuml(DbDraw::MAXI); // like midi with views
```

## Installing

```console
$ composer require jawira/db-draw
```

## Contributing

If you liked this project, ⭐ [star it on GitHub](https://github.com/jawira/db-draw).

## License

This library is licensed under the [MIT license](LICENSE.md).

***

## Packages from jawira

<dl>

<dt>
    <a href="https://packagist.org/packages/jawira/plantuml-client"> jawira/plantuml-client
    <img alt="GitHub stars" src="https://badgen.net/github/stars/jawira/plantuml-client?icon=github"/></a>
</dt>
<dd>Convert PlantUML diagrams into images.</dd>

<dt>
    <a href="https://packagist.org/packages/jawira/plantuml-encoding"> jawira/plantuml-encoding
    <img alt="GitHub stars" src="https://badgen.net/github/stars/jawira/plantuml-encoding?icon=github"/></a>
</dt>
<dd>PlantUML encoding functions.</dd>

<dt>
    <a href="https://packagist.org/packages/jawira/plantuml">jawira/plantuml
    <img alt="GitHub stars" src="https://badgen.net/github/stars/jawira/plantuml?icon=github"/></a>
</dt>
<dd>Provides PlantUML executable and plantuml.jar</dd>

<dt><a href="https://packagist.org/packages/jawira/">more...</a></dt>
</dl>
