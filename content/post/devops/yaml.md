+++
Categories = ["DevOps"]
Tags = ["DevOps","Linux"]
Description = ""
menu = "devops"
date = "2019-01-23"
title = "YAML"
+++

**YAML** с версии 1.2 
- это надмножество JSON. 
- все, что правильно для JSON, годится и для YAML.
- По сути yaml - это расширение json. Или json подмножество yaml :)
- удобно писать конфиги, которые конвертятся в json
<!--more-->
```yaml
multiliners:
    ugly_multiline: "ugly\nugly\nugly\nugly\n"

    multiline_with_line_ending: |
        multiline text
        with ending

    multiline_without_line_ending: |-
        multiline text
        without ending
```                

```yaml
commands:
    - do something with --a long --list of --parameters 
    - do something 
        with 
        --a long 
        --list of 
        --parameters     
```                

```yaml
singleliners:
    simple: 
        single
        line
        text

    single-line-text: >-
        single
        line
        text

    single-line-text-with-line-ending: >
        single
        line
        text
```                

```yaml
inheritance:
    _basic: &basic
        cpu:  2
        ram:  2
        disk: 10
        os: rhel6 

    vm-profiles:
        small: 
            <<: *basic
            cpu: 1
        large: 
            <<: *basic
            cpu: 4
```                

```yaml
inheritance:
    _basic: &basic
        cpu:  2
        ram:  2
        disk: 10
        os: rhel6 

    vm-profiles:
        small: {<<: *basic,  cpu: 1}
        large: {<<: *basic,  cpu: 4}
```                

элементы & и * позволяют определить ссылку на элемент и затем его использовать.        
```yaml
references:
    value1: &reference "Don't repeat yourself!"  
    value2: *reference 
```                

```yaml
json:
    vm-profiles-yaml:
        small:
            cpu:  2
            ram:  2
            disk: 10
            os: rhel6 
        large:
            cpu:  4
            ram:  4
            disk: 10
            os: rhel6 

    vm-profiles-json:
        small:  { cpu: 2, ram: 2, disk: 10, os: rhel6 } 
        large:  { cpu: 4, ram: 4, disk: 10, os: rhel6 } 
```                

```yaml
matrices:
    matrix_json_style: [
        [1, 0, 0],
        [0, 1, 0],
        [0, 0, 1],
    ]
    matrix_yaml_style: 
        - [1, 0, 0]
        - [0, 1, 0]
        - [0, 0, 1]
```                

Так же можно использовать в **Python**:
```python
>>> import yaml
>>> print(yaml.dump({(True, False): 1}))
? !!python/tuple [true, false]
: 1
>>> print(yaml.dump([['w','1', {'r': {'s': [1, 2, 3]}, 'd': 4}]]))

>>>print yaml.load("""
... name: Vorlin Laruknuzum
... sex: Male
... class: Priest
... title: Acolyte
... hp: [32, 71]
... sp: [1, 13]
... gold: 423
... inventory:
... - a Holy Book of Prayers (Words of Wisdom)
... - an Azure Potion of Cure Light Wounds
... - a Silver Wand of Wonder
... """)
{'sex': 'male', 'inventory': ['a Holy', 'an Azure', 'a Silver'], 'gold': 100, 'name': 'vol'}

>>> print yaml.load("""
... - [1, 0, 0]
... - [0, 1, 0]
... - [0, 0, 1]
... """)
[[1, 0, 0], [0, 1, 0], [0, 0, 1]]

>>> yaml.load('[1, a, false]')  # парсим yaml-строку
[1, 'a', False]
>>> yaml.dump([2, 'b', None])  # дампим в yaml-строку
'[2, b, null]\n'

>>> cfg = yaml.load(open('test.yaml'))
```
