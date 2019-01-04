
---
title: "Книга ML Python Пример 0"
date: 2019-01-03
description: ""
tags: ["ML", "Python"]
draft: true
---

Книга ML Python Пример 0


```python
import sys
print("версия Python: {}".format(sys.version))

import pandas as pd
print("версия pandas: {}".format(pd.__version__))

import matplotlib
print("версия matplotlib: {}".format(matplotlib.__version__))

import numpy as np
print("версия NumPy: {}".format(np.__version__))

import scipy as sp
print("версия SciPy: {}".format(sp.__version__))

import IPython
print("версия IPython: {}".format(IPython.__version__))

import sklearn
print("версия scikit-learn: {}".format(sklearn.__version__))
```

    версия Python: 3.6.1 |Anaconda custom (64-bit)| (default, May 11 2017, 13:25:24) [MSC v.1900 64 bit (AMD64)]
    версия pandas: 0.20.1
    версия matplotlib: 2.0.2
    версия NumPy: 1.12.1
    версия SciPy: 0.19.0
    версия IPython: 6.2.1
    версия scikit-learn: 0.18.1
    


```python
!pip install mglearn
```

    Requirement already satisfied: mglearn in c:\anaconda3\lib\site-packages (0.1.6)
    Requirement already satisfied: matplotlib in c:\anaconda3\lib\site-packages (from mglearn) (2.0.2)
    Requirement already satisfied: pillow in c:\anaconda3\lib\site-packages (from mglearn) (4.1.1)
    Requirement already satisfied: pandas in c:\anaconda3\lib\site-packages (from mglearn) (0.20.1)
    Requirement already satisfied: numpy in c:\anaconda3\lib\site-packages (from mglearn) (1.12.1)
    Requirement already satisfied: cycler in c:\anaconda3\lib\site-packages (from mglearn) (0.10.0)
    Requirement already satisfied: scikit-learn in c:\anaconda3\lib\site-packages (from mglearn) (0.18.1)
    Requirement already satisfied: six>=1.10 in c:\anaconda3\lib\site-packages (from matplotlib->mglearn) (1.11.0)
    Requirement already satisfied: python-dateutil in c:\anaconda3\lib\site-packages (from matplotlib->mglearn) (2.6.1)
    Requirement already satisfied: pytz in c:\anaconda3\lib\site-packages (from matplotlib->mglearn) (2017.2)
    Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=1.5.6 in c:\anaconda3\lib\site-packages (from matplotlib->mglearn) (2.1.4)
    Requirement already satisfied: olefile in c:\anaconda3\lib\site-packages (from pillow->mglearn) (0.44)
    


```python
!pip install pandas
```

    Requirement already satisfied: pandas in c:\anaconda3\lib\site-packages (0.20.1)
    Requirement already satisfied: python-dateutil>=2 in c:\anaconda3\lib\site-packages (from pandas) (2.6.1)
    Requirement already satisfied: pytz>=2011k in c:\anaconda3\lib\site-packages (from pandas) (2017.2)
    Requirement already satisfied: numpy>=1.7.0 in c:\anaconda3\lib\site-packages (from pandas) (1.12.1)
    Requirement already satisfied: six>=1.5 in c:\anaconda3\lib\site-packages (from python-dateutil>=2->pandas) (1.11.0)
    
