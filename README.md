# QChildProcessWidget

Виджет, отображающий окно дочернего процесса (например, браузера или, может, графического редактора).

Этот виджет меняет позицию, размер, а также видимость окна другого процесса, который сам при создании запускает.
На время перемещения или изменения размеров данного виджета, делается скриншот от окна дочернего процесса и отображается этот скриншот. По завершении изменения геометрии виджета окно дочернего виджета снова отображается уже с новой геометрией, поверх нашего окна.

## Ограничения:

### Первое

Как определить, какое окно нужно захватить: запускаемое окно должно иметь уникальный (и заранее известный нам!) заголовок.

Альтернативное решение: дочерний процесс при старте должен писать "window id: 0x12345678" первой строкой сразу после запуска. Получение id окна таким образом на данный момент **НЕ РЕАЛИЗОВАНО**.

### Второе

Работает корректно только когда один монитор
