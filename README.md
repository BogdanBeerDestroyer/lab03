# Лабораторная 3. Шумилишский Богдан. ИУ8-22.
## Задание 1
### Условие:
Вам поручили перейти на систему автоматизированной 
сборки CMake. Исходные файлы находятся в директории <br>
formatter_lib. В этой директории находятся файлы 
для статической библиотеки formatter. Создайте <br>
CMakeList.txt в директории formatter_lib, с 
помощью которого можно будет собирать статическую <br>
библиотеку formatter.
### Решение:
```touch CMakeLists.txt```<br>
Затем открываем созданный файл в ide или любом редакторе:<br>
```
cmake_minimum_required(VERSION 3.16.3)
project(formatter)
set(SOURCE_LIB formatter.cpp)
add_library(formatter STATIC ${SOURCE_LIB})
```
Задали минимальную версию, назвали проект, объявили переменную 
и добавили библиотеку.<br>
В cpp-файле должен быть уже подключен хедер, так что его можно не писать
в ```add_library```.
## Задание 2
### Условие:
У компании "Formatter Inc." есть перспективная 
библиотека, которая является расширением предыдущей<br>
библиотеки. Т.к. вы уже овладели навыком созданием
CMakeList.txt для статической библиотеки formatter,<br>
ваш руководитель поручает заняться созданием
CMakeList.txt для библиотеки formatter_ex, которая<br>
в свою очередь использует библиотеку formatter.
### Решение:
```
cmake_minimum_required(VERSION 3.16.3)
project(formatter_ex)
include_directories(formatter)
add_subdirectory(formatter)
add_library(formater_ex STATIC formater_ex.cpp)
target_link_libraries(formater_ex formater)
```
Задали минимальную версию, назвали проект, подключили и добавили
поддиректорию, <br>
добавили ```formatter_ex```, и залинковали библиотеки.
## Задание 3
### Условие:
Конечно же ваша компания предоставляет примеры использования 
своих библиотек. Чтобы продемонстрировать как работать с <br>
библиотекой formatter_ex, вам необходимо создать два 
CMakeList.txt для двух простых приложений:
1. hello_world, которое использует библиотеку formatter_ex;
2. solver, приложение, которое использует статические библиотеки formatter_ex и solver_lib.
### Решение пункта 1:
```
cmake_minimum_required(VERSION 3.16.3)
project(hello_world)
include_sublibrary(formatter_ex)
add_subdirectory(formatter_ex)
add_executable(hello_world hello_world.cpp)
target_link_libraries(hello_world formatter_ex)
```
Здесь мы просто подключили библиотеку, добавили её, добавили исходник
и залинковали их.
### Решение пункта 2:
```
cmake_minimum_required(VERSION 3.16.3)
project(solver)
add_library(solver_lib STATIC solver_lib.cpp)
include_sublibrary(formatter_ex)
add_subdirectory(formatter_ex)
add_executable(hello_world hello_world.cpp)
target_link_libraries(hello_world solver_lib formatter_ex)
```
Здесь то же самое, только добавляем еще одну библиотеку и линкуем 
на одну директорию больше. 
