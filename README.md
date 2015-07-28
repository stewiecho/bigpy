
# Python for Data Analysis

## 강사
- seongjoo@codebasic.co
- @LeeSeongjoo
- [github](https://github.com/lseongjoo/bigpy)
- [책] 데이터/수치 분석을 위한 파이썬 라이브러리 Scipy와 Numpy

## Download
- [Anaconda 2.3](http://continuum.io/)
- [Python for Data Analysis Sample Data](https://github.com/pydata/pydata-book)

## Background
- fortran, c 등을 설치하기 귀찮다 (numpy, panda를 설치하세요)
- exe 파일 대신 ipython notebook 을 쓰는 이유는 다른 패키지에서도 동일한 방법으로 실행가능하다.
- enthought Canopy (Numpy와 scipy를 만든 사람이 만든회사)
	- 독자적인 platform을 사용하는 경향이 있다 (그래서 anaconda 사용)
- Scikit-lean, Scikit-Image

## Basic

- ctrl + m b (insert new cell)

```python
## python 3 의 기본 문자열은 unicode
a = '한글' # python 2
a = u'한글' # python 3 의 기본

## Python 2 에서 python 3의 print 사용
from __future__ import print_function
```
	


#### BIF (Built-in Function)
```python
## for 중복도 가능 + filtering
[a*b for a in [1,2,3] for b in [4,5,6,7] if b > 6]
```


## pandas

#### Missing Value 처리
```python
# 해당 데이터에 tz 필드가 없는 경우
clean_tz = frame['tz'].fillna('Missing')
# 필드는 있는데, 값이 빈 경우
clean_tz[clean_tz == ''] = 'Unknown'

# 정리된 데이터에 대해 통계 수치 추출
tz_counts = clean_tz.value_counts()
tz_counts[:10]
```

#### 특정 필드에 대한 분기
```python
import numpy as np

# frame의 'a' 필드의 값이 없는 경우 걸러낸다
cframe = frame[frame.a.notnull()]

# cframe의 'a' 필드의 문자열이 'Windows'를 포함하면 그 값을 'Windows' 아니면 'Not Windows'라고 함
operating_system = np.where(frame['a'].str.contains('Windows'), 'Windows', 'Not Windows')
operating_system[:5]
```

#### Load Separated Data from File
```python
import pandas as pd

unames = ['user_id', 'gender', 'age', 'occupation', 'zip']
users = pd.read_csv('pydata/ch02/movielens/users.dat', sep='::', header=None, names=unames, encoding='latin1')
users[:5]

rnames = ['user_id', 'movie_id', 'rating', 'timestamp']
ratings = pd.read_csv('pydata/ch02/movielens/ratings.dat', sep='::', header=None, names=rnames, encoding='latin1')
rnames[:5]

mnames = ['movie_id', 'title', 'genre']
movies = pd.read_csv('pydata/ch02/movielens/movies.dat', sep='::', header=None, names=mnames, encoding='latin1')
movies[:5]

## Merge
data = pd.merge(pd.merge(ratings, users), movies)

# aggfunc 는 mean average 등이 있음
mean_ratings = data.pivot_table('rating', index='title', columns='gender', aggfunc='mean')
## mean_ratings = data.pivot_table('rating', index='title', columns='gender', aggfunc=my_func) 도 가능
```



