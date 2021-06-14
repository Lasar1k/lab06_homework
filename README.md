[![Build Status](https://travis-ci.com/Rogopl/lab06_homework.svg?branch=master)](https://travis-ci.com/Rogopl/lab06_homework)

.travis.yml:
```
language: cpp

script:
- cd hello_world_application/                                                # переходим в папку hello_world_application
- cmake . && cmake --build . && cmake --build . --target package             # собираем симэйк, билд и создаём пакет
- cmake . && cmake --build . && cmake --build . --target package_source      # то же с новым пакетом
- cd ..//solver_application/                                                 # здесь всё аналогично
- cmake . && cmake --build . && cmake --build . --target package
- cmake . && cmake --build . && cmake --build . --target package_source

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
      - mingw-w64
      - rpm
```
В файлы CMakeLists.txt добавляем строки, чтобы подключить cpack в папках solver_application и hello_world_application:
```
install(TARGETS solver DESTINATION bin)
set(CPACK_PACKAGE_NAME "solver")
set(CPACK_PACKAGE_VENDOR "Company_Name")
set(CPACK_PACKAGE_CONTACT "https://github.com/Rogopl")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "alf.ivan2002@gmail.com")
set(CPACK_PACKAGE_DESCRIPTION "some program")
set(CPACK_GENERATOR "DEB")
include(CPack)
```
После этого всё работает и сборка на трэвисе проходит успешно
