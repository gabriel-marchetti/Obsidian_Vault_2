### Why do Makefiles existis?
They help you decide which parts of the project need to be recompiled. 

![[dependency_graph.png | center]]

Here we can see an example of dependency of files in a C++ project. Note that whenever two.cpp changes, then main.cpp needs to be recompiled.

### Alternativos do Makefiles.
- SCons - https://scons.org/
- CMake - https://cmake.org/
- Bazel - https://bazel.build/?hl=pt-br
- Ninja - https://ninja-build.org/

If you are specially seeking something to compile <mark style="background: #ADCCFFA6;">Java</mark> projects, you can use:
- Ant - https://ant.apache.org/
- Maven - https://maven.apache.org/what-is-maven.html
- Gradle - https://gradle.org/

## Pattern of a Makefile
A Makefile is construct based on rules each rule is based on:
```
targets: prerequisites
	command
	command
	command
```
Criando um exemplo:
```
hello: 
	echo "Hello, world."
	echo "If file 'hello' does not exists this should not run."
```
Como o código sugere, se criarmos um arquivo com "touch hello" veremos que rodar "make" não trará os mesmos efeitos.

As únicas variáveis que estamos interessados dentro do Makefile são strings. elas podem ser definidas através de:
```
files := file1 file2

some_file: $(files)
	echo "Look at this variable: " $(files)
	touch some_file

file1:
	touch file1
file2:
	touch file2

clean:
	rm -f file1 file2 some_file
```
We can invoke a variable using $() or ${}.
We can also use the all target to invoke multiple other targets:

```
all: one two three

one:
	touch one
two:
	touch two
three:
	touch three
```

If we want to use multiple targets we can use:
```
all: one two

one two:
	touch @$
```
OBS: @$ will iterate through each of the entries in the target name.

### Automatic Variables and Wildcards

Both "\*" and "%" are called wildcards 

``` python
thing_wrong := *.c # is converted to a string "*.o"
thing_right := $(wildcard *.c)

one: $(things_right)

two: $(wildcard *.c)
```

Using some special names:

```python
hey: one two
	# output target name: "hey"
	echo $@
	# output name of prerequisites newer than hey
	echo $?
	# output name of all prerequisites
	echo $^
	# output name of first prerequisite
	echo $<
	touch hey
one:
	touch one
two:
	touch two
clean
	rm -f one two hey
```

