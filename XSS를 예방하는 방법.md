# XSS를 예방하는 방법

참조 : https://resources.hacware.com/how-to-secure-frontend-code-from-cross-site-scripting/



## XSS 란?

크로스사이트 스크립팅이란 브라우저를 제어하려는 악의적인 스크립을 이용하는것을 말한다.

이러한 보안위협은 동일출처정책같은 보안정책을 무효화 시킵니다.

![image-20211010214449514](C:\Users\PRO\AppData\Roaming\Typora\typora-user-images\image-20211010214449514.png)

위의 표를 보면 XSS 의보안위협은 지속적으로 증가하는것을 볼수있으며 다른 위협보다 월등히 높은것을 볼수있다.

종류에는

- DOM-based XSS
  - 요청한 돔 요소를 읽고 응답으로 악의적인 스크립트를 보내는 경우
- Reflected XSS
  - 자바스크립트가 포함된 악의적인 링크를 클릭시 대상자의 브라우저에 자바스크립트를 삽입한다.
- Stored XSS
  - 스크립트가 DB에서 저장되어서 유저의 요정에 들어간다.

![image-20211010215403216](C:\Users\PRO\AppData\Roaming\Typora\typora-user-images\image-20211010215403216.png)

```
https://exampble.com/login.php?arg=<script>alert('malicious_script');</script>
```

공격자는 위 링크처럼 악성스크립트가 담아진 링크를 보내고

이를 클릭하면 클라이언트 시스템에서 클라이언트의 정보가 공격자에게 넘어가도록 실행이 된다.

비슷하게 공격자는 세션이나 쿠키의 정보를 훔칠수있고 실제 사용자인척 가장할수있다.





```
http://example.com/search?par=car
```

일반적인 URL을 살펴보면 이렇다. par에 car라는 파라매터가 입력되어서 출력을 하지만



```
http://example.com/search?par=car++%3Cscript%3EMALICIOUS_SCRIPT()%3C/script%3E
```

악의적인 스크립트로 인해서 클라이언트 측에서 파라매터를 이런식으로 받을수있다.

위같은 파라매터는 클라이언트측에게 치명적으로 다가온다.



## 그러면 어떻게 XSS 를 피해야할까??



secure code는 이를 포함한다.

- 항상 프레임워크를 사용한다. 이들은 대부분 보안에 강하긴때문
- 사용자가 제공하는 input 필드를 항상 안정성있게 취급해야한다.
- 출력에 대해서 인코딩 메커니즘을 채택해라
- 사용자의 입력을 처리하기 전에 확인해라
- 항상 defense-in-depth 원리를 따라라
- OWASP에서 제공되는 cheat cheet를 따라라
  - OWASP는  오픈소스 웹 애플리케이션 보안 프로젝트이다.
- 적절한 응답헤더를 사용해라
- 콘텐츠에 대해서 보안정책을 설계해라
- 웹에플리케이션에대해 개발전 분석이 필요
- XSS 방지기술에 대해 업데이트하고 HacWare의 시큐어 코드를 따라라



### 어떻게 XSS 취약한지 테스트할수있을까?

XSS 취약성은 일반적으로 로그인/등록 및 연락처 페이지와 같이 웹 응용 프로그램에서 사용자가 제공한 입력 필드가 주어지는 곳에 존재한다.

백엔드의 인풋필드에 악성스크립트가 심어진다. 사용자가 인풋필드에 데이터를 넣을 경우 악성스크립트가 동작이되고 원치않은 동작이 일어난다.

즉, XSS는 테스트 할수있고,HTML과 자바스크립트 양족에서 입력필드를 검사함으로써 피할수있다.

Reflected and Stored XSS 에 대해서는 광범위하고 복잡한 수동테스트가 필요로 한다.

예를 면 영숫자, 특수문자, 자바스크립트 코드같은 인풋에 대해서 말이다.

마찬가지로, 각 입력에 대해 브라우저에서 HTTP 응답을 관찰하고 백엔드에서 침입을 식별하거나 입력 정보가 손상될 수 있는 코너 케이스를 분석합니다.

> 코너 케이스는 여러 가지 변수와 환경의 복합적인 상호작용으로 발생하는 문제다.

DOM-based XSS는 URL에 단순하고 복잡한 입력을 전달하고 브라우저의 개발자 도구를 사용하여 해당 입력에 대해 DOM 요소를 관찰함으로써 테스트할 수 있습니다.

지속적인XSS 칩입으로 인해 많은 XSS 테스트 툴이 제공되고있따.

- XSS Scanner
- XSStrike
- Maria-Grabber/XSS-Scanner
- Acunetix
- OWASP zap XSS Scanner
- IBM Rational AppScan
- Burp Suite
- Zed Attack Proxy
- https://xss-scanner.com/
- XSS Hunter
- XSSER
- Pybelt



아 근데 어떻게 예방하는지는 왜 안알려줌?? 