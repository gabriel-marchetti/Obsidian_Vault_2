A linguagem de programação C++ tinha como finalidade ser uma extensão da linguagem C. De fato, há alguns anos atrás o nome da linguagem era "C with Classes"(Hoje em dia já não sei se é assim, porque algumas implementações de C não necessariamente funcionam em C++). Ela surge, como o nome já diz, para implementar estruturas de classe dentro da linguagem C, portanto, ela utiliza classes e herança para apps. 

Características:
- É uma linguagem fortemente tipada.
- Possui uma extensa biblioteca chamada STL (Standard Template Library).

Algumas funcionalidades da linguagem podem ser vistas no seguinte código:

```cpp
#include <iostream>

// A simple function to add two numbers
int add(int a, int b) {
    return a + b;
}

class Calculator {
public:
    // A member function to multiply two numbers
    int multiply(int a, int b) {
        return a * b;
    }
};

int main() {
    int x = 5;
    int y = 3;

    // Using the standalone function 'add'
    int sum = add(x, y);
    std::cout << "Sum: " << sum << '\n';

    // Using a class and member function
    Calculator calc;
    int product = calc.multiply(x, y);
    std::cout << "Product: " << product << '\n';

    return 0;
}
```