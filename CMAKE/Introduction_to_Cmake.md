## Why CMake?
	Just using one file to contain all your source files is easy to setup the compilation process. But imagine that you working with a project with multiple files. Then, you would need to write multiple times the compilation process. So CMake is used to solve this problem and automate the process of compiling your program.

 Crie um arquivo <mark style="background: #ADCCFFA6;">CMakeLists.txt</mark>
	 Dentro desse arquivo é necessário escrever:
	 - cmake_minimum_required(VERSION <version>)
	 - project(<nome-projeto>)
	 - add_executable(<nome-executavel> <sources>)

Crie uma pasta auxiliar para gerenciar suas builds. Por exemplo uma pasta build.

```
mkdir build
cd build
make ..
```

Após definir esses atributos podemos fazer:

```
cmake --build
-- Espere o processo terminar
cd Debug
-- Aqui estará seu executável
```

Para modificar o padrão que esteja sendo utilizado dentro do CMAKE podemos fazer:
```
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
-- Após rodar dentro de build:
cmake --build .
-- Teremos nosso projeto.
```

