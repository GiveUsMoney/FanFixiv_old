# 팬픽시브 백엔드 기획서

총 3~4개의 마이크로 서비스로 구현할 예정

## 서버 정리

1. 인증 서버
    - 만화를 올릴 사람이야 당연히 필요할테니
    - 부가적인 이메일 서버 사용 예정 있음
2. 업로드 서버
    - 파일 업로드는 AWS S3를 이용할 예정
    - 태그, 원작자, 번역가 등록 기능도 이곳에 있을 예정
    - 관리자 API 또한 여기에 추가될 예정.
3. 검색 서버
    - 말 그대로 검색 서버
    - 문법을 통한 검색도 이용할 예정
    - 제외 문법 추가할 예정
4. *좋아요, 댓글 서버*
    - 만약 추가적인 기능이 없을 경우 업로드 서버에 통합될 가능성이 있음

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