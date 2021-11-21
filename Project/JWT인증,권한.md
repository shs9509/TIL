Authentication,인증

401 Unauthorized  비인증

누구인지 확인

로그인이 인증



Authorization,권한부여 허가

인증이되어도 권한을 받는건아니다

403 Forbidden

서버는 클라이언트가 누군지 알고있다.

401은 모름

로그인하고 부여된거에 대한 권한





세션인증

세션아디를 담은 쿠키를 통해서 서버가 확인하고 ㅇㅋ함



토큰인증

JWT (Json Web Token) - JSON 포맷을 활용해 요소간 정보를 교환하기위한 표준 포맷

세션처럼 서버에 정보를 담는게아닌 토큰자체가 검증이됨

높은 보안의 수준

JSON의 범용성, 서버의 자원절약



[헤더].[페이로드].[시그니쳐] 로 이루어짐

header

type 과 해시알고리즘

payload

토큰에 넣을 정보 (claim)을 넣는다.

signature

헤더와 페이로드의 encoding 값을 더하고 거기에 비밀키를 해싱하여 만든다.

https://jwt.io/

jwt 해석

https://jpadilla.github.io/django-rest-framework-jwt/

 'JWT_EXPIRATION_DELTA': datetime.timedelta(seconds=300), 기존 5분유지

days=1 이건 하루유지 토큰 유지기간



토큰은 로컬스토리지에 저장해야한다.

```vue
.then((res)=>{
        // res에 들어있는 token 세팅!
        localStorage.setItem('jwt', res.data.token)
		this.$emit('login') //로그인되었다는걸알려야됨 왜? 그냥이동하는건 의미없(부모는모름)
        this.$router.push({ name: 'TodoList' }) 
      })

생성한 토큰의 유무로 이렇게 쓸수있음

  created: function () {
    const token = localStorage.getItem('jwt')
    if (token) {
      this.isLogin = true
    }
  }
```

지금까지 인증



권한부여는 

CRUD에서 토큰의 유무를 적어줘야함

```python
from rest_framework.decorators import authentication_classes, permission_classes
from rest_framework.permissions import IsAuthenticated
from rest_framework_jwt.authentication import JSONWebTokenAuthentication


@authentication_classes([JSONWebTokenAuthentication])
#JWT가 유효한지 여부
@permission_classes([IsAuthenticated])
#인증
```


