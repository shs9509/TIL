# ManyToManyField

### M대 N 관계를 정의하기 위한 클래스 

 M대N 관계를 정의하기 위해서는 중간 조인 테이블을 생성해야한다.



- related_name

  이거는 Foreign key의 related_name 과 같다.



- symmetrical

  `self`  경우를 위해 쓰이며 

  `self` 는 자기자신 모델과 M대N 관계라는 것을 의미한다. 

  

  - symmetrical = Ture

    : [나는 너가 친구] 그래서 [너에게 나는 친구]  이게 성립되는 상황, (+ default)

    

  - symmetrical = False

  ​		: 인스타의 팔로우와 팔로잉의 경우에는 한쪽이 팔로우 한다하더라도 반대쪽은 그렇지 않다. 

  ​		이 경우가 symmetrical = False 인 관계다.

  

 ​ 표현 방식

```python
class Person(models.Model):
	friends = models.ManyToManyField('self', symmetrical= Flase, related_name = ' ')
```

​	:question:   `symmetrical= Flase`인 경우 `related_name`을 써서 구분을 꼭 해줘야 한다.

​	 :exclamation:    안하면!? 자기자신의 모델과 관계해 있지만 서로 다른 상황임에도 구분이 안되기 떄문



 생성된 필드

- id: 기본키

- `form_<model>_id` : 원본 인스턴스

- `to_<model>_id`: 타겟 인스턴스



+) 다대다 관계를 더 알고싶다면

https://docs.djangoproject.com/en/3.1/topics/db/examples/many_to_many/