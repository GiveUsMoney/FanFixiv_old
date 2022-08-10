# 팬픽시브 백엔드 설계서

> 총 3~4개의 마이크로 서비스로 구현할 예정. 모든 서버의 API는 Swagger(API 문서 라이브러리)가 있어야함.

## ~~기능 정리~~

> 기능의 경우 [기능 명세서](FS.md)를 확인할 것.

## 설계

> 1. 모든 마이크로 서비스는 다른 프레임워크를 이용할 것!
> 2. AWS 람다 사용또한 고려할 것.

### 개발 가능한 프레임워크 총정리

- JAVA
    - Spring Boot
- JavaScript
    - Express
    - Koa
- TypeScript
    - NestJS
- Python
    - Flask
    - DJango
    - Fast Api
- AWS
    - AWS Lambda
- ~~C++~~
    - ~~Crow~~

**인증서버**
1. Spring Boot(선택)
    - 뛰어난 보안성
    - Spring Security의 사용경험 있음
    - 복잡할수 있음.
2. Node계열
    - Node 계열은 적은 인증 경험 (근데 애초에 내가 인증 서비스 개발 경험이 적음)
3. Python
    - 인증 경험이 적음

**업로드 서버**
1. Spring Boot
    - 간단한 기능에 비해 코드 자체가 복잡해질 가능성이 있음.
2. Node계열(선택-NestJS)
    - 간단한 기능에 걸맞음.
    - 많은 ORM 지원으로 여러 DB 사용 가능
3. Python
    - 사용 경험 자체가 적지만 이용 할려고 하면 할수는 있음.
4. AWS Lambda
    - 필요 API가 많아 적합하지 않음.

**검색 서버**
1. Spring Boot
2. Node계열
3. Python
4. AWS Lambda (선택)

**이메일 서버**
1. Spring Boot
2. Node계열
3. Python (선택)
4. AWS Lambda