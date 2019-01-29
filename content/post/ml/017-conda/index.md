+++
Categories = ["DevOps"]
Tags = ["DevOps","ML","Conda"]
Description = ""
menu = "devops"
date = "2019-01-23"
title = "Conda как отличная замена Pip"
+++

[Conda документация](http://conda.pydata.org/docs/)
	
**Pip** - стандартный менеджер пакетов питона, позволяет устанавливать бинарные wheel сборки пакетов. Если их нет (ни в самом Pip, ни где-то еще), Pip компилирует пакеты локально. При этом могут возникнуть проблемы при сложных зависимостях, когда требуются сторонние не питон библиотеки. В этом случае удобно использовать Conda.
<!--more-->
Команды Pip:
- pip search package_name - поиск пакета через pip
- pip install package_name - установка пакета через pip

**Conda** - менеджер пакетов питона, позволяет устанавливать уже скомпилированные пакеты (может работать и в режиме компиляции пакетов перед установкой). Также Conda - менеджер окружений системы, позволяет создавать окружения с разными версиями чего угодно (библиотеки C, низкоуровневые библиотеки и т.д.).

**Conda** бывает в двух версиях:
- *Анаконда* - более 150 предустановленных пакетов (около 3 Гб) + более 250 пакетов, готовых к установке командой conda install package_name
- *Миниконда* - более 400 пакетов, готовых к установке командой conda install package_name

[Список пакетов](https://docs.continuum.io/anaconda/pkg-docs)

Анаконда и Миниконда включают: conda, интерпретатор питона, pip

**Команды Conda**: 
> conda search package_name  - поиск пакета через conda
> conda install package_name - установка пакета через conda
> conda install - установка всего стандартного набора пакетов - более 150, около 3 Гб
> conda list - список установленных пакетов
> conda update conda - обновление conda
> conda clean -t - удаление кеша - архивов .tar.bz2, которые могут занимать много места и не нужны

> conda install --name bunnies beautifulsoup4
> conda install name_lib=version
> conda install --channel https://conda.anaconda.org/pandas bottleneck

**Env** - так же создает виртуальное окружение:
```bash
$ conda env --help
create a new environment named /envs/snowflakes with the program Biopython.
$ conda create --name snowflakes biopython
$ source activate snowflakes
$ source deactivate
Создание второго окуржения с отличной версией питона:
$ conda create --name bunnies python=3 astroid babel
List env:
$ conda info --envs
Active env by *:
$ conda info --envs
Remove:
$ conda remove --name flowers --all
Дополнительные возможности: http://conda.pydata.org/docs/using/envs.html
```

**Install**:
1. [Download miniconda](http://conda.pydata.org/miniconda.html)
2. ``` $ bash Miniconda3-latest-Linux-x86_64.sh ```
3. ``` $ conda update conda ```
4. Если основной у нас 2.7 мы ставим conda 2.7 а потом будем указывать 
5. ``` $ conda create --name snakes python=3 ```

Для работы с **ML** ставим еще Jupyter и библиотеке:
- ``` $ conda install Jupyter```
- ``` $ conda install numpy pandas matplotlib scikit-learn```
