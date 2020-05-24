# 모범사례 - 천만사용자를 위한 AWS 클라우드 아키텍처 진화하기

사용자가 늘어날 때 마다 아키텍처가 변화해야 한다.

## 사용자수 < 1,000

> 1. 서버 선정 및 이중화 구성
> 2. db구성
> 3. 사용자 인증 서비스
> 4. 소스코드 관리 및 배포

### 서버 선정 및 이중화 구성

#### 서버 선정

> 용도에 맞는 EC2 선택
> 업무에 적합한 서버 선정

필요시 손쉬운 서버 타입 변경 가능

용량 산정에 대해 고민하지 말고, _사용해보면서 적합한 용량 선택_

cpu, processor, 메모리, 스토리지 등 다양한 옵션

#### 서버 이중화 구성

> 한 서버가 꺼졌을 경우 서비스가 정지됨을 방지

AWS Elastic Load Balancing을 이용해 부하 분산

### 데이터베이스

Amazon RDS - 6개의 엔진 기반 데이터 관리형 서비스

Amazon Aurora의 경우 MySQL, PostreseSQL 지원

자동 스토리지 확장, 백업

### 사용자 인증

> 사용자 인증 서비스 구현

회원가입, 로그인 등등

Amazon Cognito를 이용한 빠른 인증구현(개발자들은 어플리케이션 개발에만 집중)

### 소스코드 관리 및 배포

> AWS CodePipeLine을 통해 전체 흐름 관리

AWS의 모든 서비스를 활용할 수도 있음

## 사용자수 > 1000

> 1. 시스템 확장
> 2. DBMS 고가용성
> 3. 백업
> 4. 시스템 모니터링

### EC2 오토 스케일링

- 컴퓨팅 클러스터의 자동 수량 조절
- Pool 사이즈의 최소/최대 값을 지정
- 서버 장애 시 최소 수량만큼 자동 복구
- Amazon CloudWatch 지표 기반 스케일링
- 온디맨드 또는 스팟 인스턴스

### Amazon RDS 다중 AZ 배포

> Master와 StandBy를 활용한 동기식 복제
> Master DB 장애 시 StandBy가 Master DB로 승격

### AWS Backup 서비스를 이용한 백업 관리 자동화

중요한 데이터의 경우 백업도 고려(AWS Backup)

### CloudWatch를 활용한 모니터링

알람에 대한 액션 기능 및 다양한 기능

## 사용자수 > 10,000

> 1. 성능
> 2. 부하 분산

### Amazon CloudFront

- 빠른 컨텐츠 전달을 위해 캐싱
- 오리진 측의 부담을 덜어줌
- 동적 / 정적 컨텐츠 / 스트리밍 라디오
- 사용자 SSL dlswmdtj
- 낮은 TTL(0초까지 설정 가능)
- AWS와 최적화

### Amazon Aurora 읽기 복제본 오토스케일링

평균 cpu 사용량, 메모리 오토스케일링 제공

### Amazon ElasticCache

- 관리형 Memcached 또는 Redis
- 한개에서 여러 개의 노드로 확장
- 자가 복구
- 빠른 응답 속도
- 캐시, 세션 저장소, 채팅, 게임리더보드 등 다양한 Case로 활용

## 사용자수 > 100,000

> 1. Loosely Coupled, 분산 아키텍처
> 2. 서버리스 아키텍처
> 3. 분산 시스템 모니터링

### 비동기 서비스를 활용한 Loose Coupling

- 완전 관리형 서비스
- 부하에 따라 자동확장
- 관리 오버헤더 제거
- SQS - 메시지 큐 서비스
- SNS - 메시지 푸시 알림 서비스

### 서비스 재활용

직접 개발하지 말고 AWS의 다양한 관리형 서비스 활용

### 서버리스, 이벤트 기반 아키텍처 적용

- 서버리스
- 이벤트가 발생하면 함수가 실행
- 내북적으로 스케일링
- 다양한 언어 지원

### AWS Lambda의 다양한 활용

요청 양에 따라 컨테이너가 자동으로 바뀌게 된다.

### 용도에 맞는 DB 서비스 활용

### AWS X-Ray

- 성능의 병목 원인과 에러 파악
- 어플리케이션의 특정 서비스 이슈를 파악
- 분산 어플리케이션에 대한 모니터링 제공
- 서비스 호출 그래프의 시각화

## 사용자수 > 1,000,000

> 1. 재해복구(DR)/ 멀리 리전 시스템 고려
> 2. 멀티 리전 시스템 배포

- CloudFormation으로 인프라 리소르를 모델링
- S3 교차 리전 복제
- RDS snapshot 교차 리전 복사 - DB 엔진까지 백업 가능
- DynamoDB에서 비슷한 기능도 제공 - 특정 시점으로 복원하는 기능도 제공
- Redis용 ElastiCache 백업
- 멀티 리전 배포
- Route 53를 통한 멀티 리전 라우팅

## 사용자수 > 10,000,000

> 1. 글로벌 시스템 확장
> 2. 멀티 리전 확장

- Aurora 글로벌 데이터베이스
- DynamoDB 글로벌 테이블
- ElastiCache 글로벌 데이타스토어 for Redis

## 요약

### 아키텍처 기본적인 구성

- 멀티-az를 활용한 이중화 구성
- ec2 오토 스케일링 이용
- 서능 및 부하 분산을 위해 데이터 캐시
- 적절한 지표/모니터링/로깅
- 확장성이 뛰어난 관리형 서비스 활용

### 점점 더 커지는 서비스에 대한 아키텍처 개선

- CloudFormation을 이용한 프로비저닝
- 용도에 적합한 데이터베이스
- 느슨한 결함/분산을 위한 이키텍처,어플리케이션 구조 변경
- 멀티 리전으로 진화