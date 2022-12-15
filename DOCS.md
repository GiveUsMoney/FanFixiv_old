# 사용된 도구 일람

Fanfixiv를 개발하는데 사용된 도구(툴)에 대해 작성합니다. 후일 개발이 재걔될 때를 대비해 상세히 작성합시다.

## AWS

1. EC2
- 개발 서버를 운영을 위해 사용
- 보안 그룹으로 TCP 포트 3개 (3000, 8080, 8000)과 SSH 포트를 열어둘것.
2. Lambda
- S3에 올라오는 프로필 이미지의 리사이징을 위해서 사용
- 해당 Lambda에 사용된 코드의 경우 개인 소장중
3. S3
- FanFixiv에 사용되는 모든 이미지의 저장을 위해서 사용
- temp 폴더에 임시 저장한 뒤 실제 저장한 뒤 실제 폴더 (ex: profile)에 등록
- temp 폴더 내부 파일들은 한달간의 수명주기가 존재
- 사용을 위해 `fanfixiv-s3`유저의 액세스키를 따로 저장해둘것.
4. RDS
- FanFixiv에 사용되는 모든 데이터의 저장을 담당
- 개발DB의 경우 퍼블릭 액세스가 가능하도록 하되 실제 배포서버는 VPC 내부에서만 접근이 가능하도록 할것
- DB는 PostgresSQL을 사용할것.
5. API GateWay
- 개발 서버의 API 통합을 위해 사용
- 각각의 경로 (/admin, /auth, /upload)에 추가 경로(/{proxy+})를 설정해서 EC2에 연결할것
- CORS 설정 허용할것. 
6. VPC
- Fanfixiv의 모든 인프라의 네트워크 공간
- CIDR은 10.0.0.0/16로 설정할 것
- **모든 인프라가 VPC 내부에 있도록 설정할 것**
7. IAM
- Fanfixiv의 권한을 관리
- 관리자 계정 하나와 fanfixiv-email, fanfixiv-s3를 생성
- fanfixiv-email은 AmazonSESFullAccess 권한을 부여
- fanfixiv-s3는 AmazonS3FullAccess 권한을 부여
8. Amazon MQ
- MQ 서비스를 제공
- RabbitMQ를 사용 (복잡하지만 트래픽이 적은 요청이 들어오므로)
- Scure된 URL을 사용하므로 주의할것.
9. ElastiCache
- FanFixiv의 인증과정을 담당하는 소규모 DB
- 개발서버의 경우 트래픽이 많지 않고 비용을 줄이기 위해 노드를 하나만 둘 것
10. SES
- 인증이메일을 보내기 위한 이메일 서비스
- 개발서버에는 개인 이메일을 이용했지만 배포시에는 도메인을 이용할것.
- 사용을 위해 `fanfixiv-email`유저의 액세스키를 따로 저장해둘것.

## Buddy

> 배포 플랫폼

1. 3개의 백엔드 서버, 2개의 프론트엔드 서버 프로젝트를 생성할 것.
2. 배포 코드는 다음과 같이 진행 (EC2 사용시)
```
echo "애플리케이션 배포!"
CURRENT_PID=$(ps -ef | grep java | grep -v grep | awk '{print $2}' | head -1)
echo "$CURRENT_PID"

if [ -z $CURRENT_PID ]; then
  echo ">현재 구동중인 어플리케이션이 없으므로 종료하지 않습니다."
else
  echo "> kill -9 $CURRENT_PID"
  kill -9 $CURRENT_PID
  sleep 10
fi

echo "어플리케이션 배포 진행!"
nohup java -jar -Dspring.profiles.active=dev jars/auth.jar > catalina.out  2>&1 &
```
3. 종료시 디스코드에 알림을 보낼 것.