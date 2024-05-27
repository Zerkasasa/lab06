
## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```sh
$ open https://travis-ci.org
```

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в [прошлый раз](https://github.com/tp-labs/lab03#Homework). Настройте сборочные процедуры на различных платформах:

Создаем директорию `.github/workflows` и файл `cmake/yml`
``` bush
name: CMake_Build

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]


  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: checkout
      uses: actions/checkout@v3
    
    - name: Build a *formatter* library
      run: |
        cmake -H. -B_build
        cmake --build _build
      shell: bash
      working-directory: lab_4/formatter_lib
      
    - name: Build a *formatter_ex* library
      run: |
        cmake -H. -B_build
        cmake --build _build
      shell: bash
      working-directory: lab_4/formatter_ex_lib
      
    - name: Build a *hello_world* application
      run: |
        cmake -H. -B_build
        cmake --build _build
      shell: bash
      working-directory: lab_4/hello_world_application
      
      S
    - name: Build a *solver* application
      run: |
        cmake -H. -B_build
        cmake --build _build
      shell: bash
      working-directory: lab_4/solver_application
```






```
Copyright (c) 2015-2021 The ISC Authors
```
