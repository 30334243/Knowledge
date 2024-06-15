Возвращает выражение prvalue типа bool, которое описывает ограничение.
**Синтаксис**
1. requires { requirement-seq }
2. requires ( parameter-list (optional) ) { requirement-seq }
***parameter-list*** - список параметров
***requirement-seq*** - последовательность требований:
- [simple requirement](#simple-requirement)
- [type requirement](#Type-requirement)
- compound requirement[[#^a5101c]]
- nested requirement

**Локальные параметры**
Requires-expression может вводить локальные параметры. Эти параметры не имеют `linkage`, `storage`, `lifetime`. Они используются только в качестве обозначения для определения требований.
Условия program `ill-formed`:
- Локальные параметры инициированы по умолчанию 
- Список параметров заканчивается многоточием

## Simple requirement
``` cpp
template<class T>
concept is_sum = requires (T a, T b) {
	a + b;
}
static_assert(is_sum<int>, "error");// ok
static_assert(is_sum<std::vector>, "error");//error
```

##Type requirement
``` cpp
template<class T>  
struct Buffer {  
    using buffer_t = int;  
};

template<class T>  
concept IsType = requires  
{  
    typename T::buffer_t;  
};

static_assert(IsType<Buffer<int>>, "error");// ok
static_assert(IsType<int>, "error");// error
```

**Compound requirement**
Проверка подстановки и семантических ограничений выполняется в следующем порядке: ^a5101c
1. Аргументы шаблона, если есть
2. Если используется `noexcept`, то набор потенциальных исключений в выражении должен быть пуст до c++17 и выражение не вызывает исключение в c++17
3. Если `return-type-requirement` используется:
	- Аргумент шаблона подставляется в `return-type-requirement`
	- `decltype((expression))` должно удовлетворять `type-constraint`. Иначе `requires-expression` будет `false`

``` cpp
constexpr std::array<uint8_t, 4> kArr1{1, 2, 3, 4};
constexpr std::array<int, 4> kArr2{1, 2, 3, 4};

template<class T>  
concept IsType = requires(T t)  
{  
    { t[0] } -> std::same_as<uint8_t const &>;  
};  
  
static_assert(IsType<decltype(kArr1)>, "error");// ok
static_assert(IsType<decltype(kArr2)>, "error");// error
```
