# Шаблоны

Подобно C++ и Java, язык **D** позволяет определять шаблонные функции. Это способ создать **обобщённую** функцию или объект, работающий с любым типом, который компилируется с выражениями в теле функции:

    auto add(T)(T lhs, T rhs) {
        return lhs + rhs;
    }

Параметр шаблона `T` задаётся в паре скобок перед параметрами вызова функции. `T` - это просто метка, которая заменяется компилятором непосредственно при *инстанцировании* (создании экземпляра) функции с использованием оператора `!`:

    add!int(5, 10);
    add!float(5.0f, 10.0f);
    add!Animal(dog, cat); // не скомпилируется, так как Animal не реализует оператор "+"

Шаблоны функций имеют два набора параметров: первый для compile-time (времени компиляции) аргументов и второй для run-time (времени исполнения) аргументов (не шаблонизированные функции могут принимать только run-time аргументы). Если один или более compile-time аргументов не указаны при вызове функции, компилятор пытается вывести их из списка run-time аргументов (как типы этих аргументов).

    int a = 5; int b = 10;
    add(a, b); // T выводится как `int`
    float c = 5.0f;
    add(a, c); // T выводится как `float`

Функция может иметь любое число параметров шаблона, заданных при инстанцировании с использованием синтаксиса `func!(T1, T2 ..)`. Параметры шаблона могут быть любого основного типа, включая строки и числа с плавающей запятой.

В отличие от generics в Java, шаблоны в D существуют исключительно во время компиляции и генерируют высокооптимизированный код, адаптированный под конкретный набор типов, который используетя при фактическом вызове функции.

Типы `struct`, `class` и `interface` также могут быть определены
как шаблонные типы.

    struct S(T) {
        // ...
    }

### Подробнее

- [Руководство по шаблонам в D](https://github.com/PhilippeSigaud/D-templates-tutorial)
- [Шаблоны в _Programming in D_](http://ddili.org/ders/d.en/templates.html)

#### Дополнительно

- [Спецификация на шаблоны](https://dlang.org/spec/template.html)
- [Templates Revisited](http://dlang.org/templates-revisited.html):  Уолтер Брайт пишет о том, как язык D сделал "работу над ошибками", взяв за основу шаблоны C++.
- [Variadic templates](http://dlang.org/variadic-function-templates.html): Статья  о реализации в D вариативных функций с вариативными шаблонами.

## {SourceCode}

```d
import std.stdio;

/**
Шаблонный класс, который разрешает обобщённую
реализацию animals.
Параметры:
    noise = string to write
*/
class Animal(string noise) {
    void makeNoise() {
        writeln(noise ~ "!");
    }
}

class Dog: Animal!("Bark") {
}

class Cat: Animal!("Meeoauw") {
}

/**
Шаблонная функция, которая принимает любой тип
T, который реализует функцию makeNoise.
Параметры:
    animal = объект, который может создавать шум
    n = количество вызовов makeNoise
*/
void multipleNoise(T)(T animal, int n) {
    for (int i = 0; i < n; ++i) {
        animal.makeNoise();
    }
}

void main() {
    auto dog = new Dog;
    auto cat = new Cat;
    multipleNoise(dog, 5);
    multipleNoise(cat, 5);
}
```