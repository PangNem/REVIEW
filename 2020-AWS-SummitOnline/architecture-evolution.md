# 모범사례 - 천만사용자를 위한 AWS 클라우드 아키텍처 진화하기

사용자가 늘어날 때 마다 아키텍처가 변화해야 한다.

사용자 증가에 따른 아키텍처의 변화

## 사용자수 < 1,000

- 서버 선정 및 이중화 구성
- db구성
- 소스코드 관리 및 배포

용도에 맞는 EC2 선택
업무에 적합한 서버 선정

필요시 손쉬운 서버 타입 변경 가능

cpu, processor, 메모리, 스토리지 등 다양한 옵션

서버 이중화 구성 - 한 서버가 꺼졌을 경우 서비스가 정지됨을 방지

AWS Elastic Load Balancing을 이용해 부하 분산

ALB vs NLB

데이터베이스 - Amazon RDS
6개의 엔진 기반 데이터 관리형 서비스

Amazon Aurora의 경우 MySQL, PostreseSQL 지원
자동 스토리지 확장, 백업

사용자 인증 서비스 구현
회원가입, 로그인 등등
Amazon Cognito를 이용한 빠른 인증구현(개발자들은 어플리케이션 개발에만 집중)

AWS CodePipeLine을 통해

## 사용자수 > 1000

EC2 오토 스케일링 - 부하, 장애 대응, 비용절감 효과
Auto Scaling으로 가변적 동시 접속자 대응
DBMS 고가용성 고려 - DB 장애 시 시스템 서비스 불가

Amazon RDS 다중 AZ 배포
master와 stand-by 동기식 복제
master 장애 시 stand-by가 master db로 승격

중요한 데이터의 경우 백업도 고려(AWS BACKUP)

### CloudWatch를 활용한 모니터링

알람에 대한 액션

## 10,000

- 성능
- 부하분산

### Amazon CloudFront

빠른 컨텐츠 전달을 위해 캐싱
오리진 측의 부담을 덜어줌

### Amazon Aurora 읽기 복제본 오토스케일링

평균 cpu 사용량, 메모리 오토스케일링 제공

### Amazon ElasticCache

관리형 Memcached 또는 Redis
한개에서 여러 개의 노드로 확장
자가 복구
빠른 응답 속도
캐시, 세션 저장소, 채팅, 게임리더보드 등 다양한 Case로 활용

## 100,000

Loosely Coupled, 분산 아키텍처
서버리스 아키텍처
분산 시스템 모니터링

비동기 서비스를 활용한 Loose Coupling

- 완전 관리형 서비스
- 부하에 따라 자동확장
- 관리 오버헤더 제거
- SQS - 메시지 큐 서비스
- SNS - 메시지 푸시 알림 서비스

서비스 재활용
직접 개발하지 말고 AWS의 다양한 관리형 서비스 활용

서버리스, 이벤트 기반 아키텍처 적용

- 서버리스
- 이벤트가 발생하면 함수가 실행
- 내북적으로 스케일링
- 다양한 언어 지원

AWS Lambda의 다양한 활용
요청에 따라 컨테이너가 자동으로 바뀜

용도에 맞는 DB 서비스 활용하기.

분산 아키텍처 활용
AWS X-Ray
분산 어플리케이션에 대한 모니터링 제공
서비스 호출 그래프의 시각화

## 1,000,000

재해복구(DR)/ 멀리 리전 시스템 고려
멀티 리전 시스템 배포

CloudFormation으로 인프라 리소르를 모델링

S3 교차 리전 복제

RDS snapshot 교차 리전 복사 - DB 엔진까지 백업 가능

DynamoDB에서 비슷한 기능도 제공 - 특정 시점으로 복원하는 기능도 제공

Redis용 ElastiCache 백업

멀티 리전 배포

Route 53를 통한 멀티 리전 라우팅

## 10,000,000

글로벌 시스템 확장
멀티 리전 확장

Aurora 글로벌 데이터베이스

DynamoDB 글로벌 테이블

ElastiCache 글로벌 데이타스토어 for Redis

## 요약

멀티-az를 활용한 이중화 구성
ec2 오토 스케일링 이용
서능 및 부하 분산을 위해 데이터 캐시
적절한 지표/모니터링/로깅
확장성이 뛰어난 관리형 서비스 활용

CloudFormation을 이용한 프로비저닝
용도에 적합한 데이터베이스
느슨한 결함/분산을 위한 이키텍처,어플리케이션 구조 변경
멀티 리전으로 진화