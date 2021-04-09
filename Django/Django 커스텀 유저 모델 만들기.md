# Django 커스텀 유저 모델 만들기

https://docs.djangoproject.com/en/3.1/topics/auth/customizing/



## 0. 왜 해야하는가?



기존 Django 에는 'user'가 등록이 되어있다.

하지만 내가 원하는 유저의 정보들을 정해서 커스텀 해야할때가 있다. 

( 성별을 추가한다던가, 인스타링크를 넣는다던가)



+추가적으로 **Django**에서도 선호되어지는 코딩이다.

![image-20210331021009465](C:\Users\ssej0\AppData\Roaming\Typora\typora-user-images\image-20210331021009465.png)

​																	**'highly recommended'**



그래서 해야한다.





## 1. 어떻게 해야하는가?

공식문서에 잘나와있지만 영어로 되어있기때문에 보기 힘들다



0. 프로젝트 시작하기전!!!! 에 무조건 하자.



1. `AUTH_USER_MODEL`  을 추가해서 기존의  user 를 덮어씌운다.

```python
#settings.py
AUTH_USER_MODEL = 'myapp.MyUser' #
```



2. User 모델 설정

```python
#models.py
#나중에 여기서 수정 진행
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass
```



3. admin 에 등록

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User

admin.site.register(User, UserAdmin)
```



4. 