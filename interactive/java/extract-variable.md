extract-variable:java

###

1. Создайте локальную переменную и передайте ей необходимое значение.

2. Замените исходное выражение вашей новой переменной.



###

```
double price() {
  // Price consists of: base price - discount + shipping cost
  return quantity * itemPrice -
    Math.max(0, quantity - 500) * itemPrice * 0.05 +
    Math.min(quantity * itemPrice * 0.1, 100.0);
}
```

###

```
double price() {
  final double basePrice = quantity * itemPrice;
  final double quantityDiscount = Math.max(0, quantity - 500) * itemPrice * 0.05;
  final double shipping = Math.min(basePrice * 0.1, 100.0);
  return basePrice - quantityDiscount + shipping;
}
```

###

Set step 1

# Давайте рассмотрим <i>Извлечение переменной</i> на примере этого простого метода.

# Как видите, метод состоит из одного громадного выражения, в котором сам черт ногу сломит.

# Давайте разобьём это выражение на отдельные части, причём каждую из частей поместим в отдельную переменную.

Select "quantity * itemPrice"

# Сперва определим базовую цену <code>basePrice</code>, как количество товаров в заказе, умноженное на стоимость одной единицы.

Set step 2

Go to "shipping cost|||"

Print:
```

  final double basePrice = quantity * itemPrice;
```

Select 2nd "quantity * itemPrice"
+ Select 3rd "quantity * itemPrice"

# ...и применяем новую переменную в формуле. Данное выражение повторяется несколько раз, поэтому заменим все одинаковые вычисления переменной.

Print "basePrice"

#C Давайте запустим компиляцию и удостоверимся, что все хорошо.

#S Все отлично, можем продолжать!

Select:
```
    Math.max(0, quantity - 500) * itemPrice * 0.05 +
    Math.min(basePrice * 0.1, 100.0);
```

# Теперь необходимо заменить переменными оставшиеся части сложного выражения.

Select:
```
Math.max(0, quantity - 500) * itemPrice * 0.05
```

# Определим скидку за количество купленного товара <code>quantityDiscount</code>, вынеся расчёт в новую переменную.

Go to "quantity * itemPrice;|||"

Print:
```

  final double quantityDiscount = Math.max(0, quantity - 500) * itemPrice * 0.05;
```

Select:
```

    Math.max(0, quantity - 500) * itemPrice * 0.05
```

Replace " quantityDiscount"

#C Готово, теперь запустим компиляцию и удостоверимся, что не возникло ошибок.

#S Все отлично, можем продолжать!

Select:
```
Math.min(basePrice * 0.1, 100.0)
```

# Последнее часть расчётов это доставка <code>shipping</code>. Тоже используем отдельную переменную.

Go to "itemPrice * 0.05;|||"

Print:
```

  final double shipping = Math.min(basePrice * 0.1, 100.0);
```

Select:
```

    Math.min(basePrice * 0.1, 100.0)
```

Replace " shipping"

Select:
```
  // Price consists of: base price - discount + shipping cost

```

# Кстати, теперь выражение стало вполне очевидным, поэтому комментарий можно убрать.

Remove selected

#C Запускаем финальную компиляцию.

#S Отлично, все работает!

Set final step

#Q На этом рефакторинг можно считать оконченным. В завершение, можете посмотреть разницу между старым и новым кодом.