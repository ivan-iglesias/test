# PHPUnit Mock

[phpunit doc](https://phpunit.readthedocs.io/en/9.5/test-doubles.html)

Para realizar pruebas unitarias de una clase podemos encontrarnos en la situación de que tenga dependencias respecto a otras clases, las cuales no nos interesan, por lo que podemos pasar por el constructor objectos "falsos" (mocks).

Hay diferentes formas de crear mocks, siendo la mas sencilla `createMock`, la cual los crea usando las mejores practicas disponibles

```php
$stub = $this->createMock(SomeClass::class);
```

Si necesitamos algo mas específico, podemos hacerlo mediante `getMockBuilder`

```php
$caller = $this
    ->getMockBuilder(SomeClass::class)
    ->disableOriginalConstructor()
    ->disableOriginalClone()
    ->disableArgumentCloning()
    ->disallowMockingUnknownTypes()
    ->getMock();

$stub
    ->method('doSomething')
    ->willReturn('foo');
```

Para asegurarnos de que se llama un método podemos usar los métodos `expects` y `with`.

```php
$event = $this->createMock(RequestEvent::class);
$event
    ->expects($this->once())
    ->method('isMasterRequest')
    ->willReturn(false);
```

Para hacer un mock de una clase **abstracta**, usaremos `getMockForAbstractClass`

```php
$caller = $this->getMockForAbstractClass(Caller::class);

$caller = $this
    ->getMockBuilder(Caller::class)
    ->disableOriginalConstructor()
    ->disableOriginalClone()
    ->disableArgumentCloning()
    ->disallowMockingUnknownTypes()
    ->getMockForAbstractClass();
```

```css
p { color: red }
```
