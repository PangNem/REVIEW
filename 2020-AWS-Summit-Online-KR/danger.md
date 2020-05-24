# AWS 환경에서의 위험 탐지 및 사냥

## 이상 징후의 탐지를 위한 기본 서비스

식별 -> 보호 -> 탐지(자동화, 분석) 대응 -> 복구

### 이상 징후의 탐지를 위한 데이터 소스

#### API 호출 이력 - CloudTrail

사용자의 API 사용 내역과 현황을 추적 분석

#### 트래픽 정보 - VPC Flow Log, VPC Mirroring

VPC 내 ENI에서 발생되는 트래픽 정보

#### 시스템 상태 정보/로그 - CloudWatch

시스템이나 어플리케이션 상태 및 각종 시스템 로그

#### DNS 로그

VPC 내에서 발생되는 다양한 DNS 요청 이력

### CloudTrail

AWS 서비스 사용과 관련한 API 로그 분석

사용자의 API 사용 내역과 현황을 추적 분석

#### 관리 이벤트

EC2 Instance의 생성/삭제/변경 등과 같은 리소스 제어 행위

- 일반적으로 데이터 이벤트에 비해 자주 발생하지 않음
- 거의 모든 서비스에서 지원

#### 데이터 이벤트

S3의 특정 Object를 읽어들이는 것과 같은 상세한 행위

- 일반적으로 아주 빈번하게 발생
- Lambda와 S3에서 지원

#### CloudTrail Insights - 비정상 API 활동 감지

- CloudTrail Insights 활성화 시 CloudTrail에서 자동으로 비정상적인 API 활동을 감지
- 탐지된 비정상 API 활동은 Management Console대시보드에 그래프 형태로 제공
- AWS CLI나 SDK등을 이용한 조회 가능
- 최근 90일간의 Insight 이벤트를 콘솔에서 제공
- Insight 다운로드 가능(CSV, JSON 포맷)

### CloudWatch Logs Insights

AWS 서비스 사용과 관련한 API 로그 분석

- VPC Flow Logs
- Route53 Logs
- Lambda Logs
- CloudTrail Logs
- Other fomats

### CloudWatch Anomaly Detection

비정상 탐지

일정 기간 동안 저장된 정보를 기반으로 비정상 사용 패턴 파악

## Amazon GuardDuty

고객 설정 등이 필요 없이, 알아서 위험에 대해 탐지한다.

- 정찰
- 인스턴스 침해
- 어카운트 침해

## Amazon Detective

### 분석 과정에서의 과제

- 데이터 선별
- 복잡도
- 기술 숙련도
- 비용

### 도입 배경

보안 이슈에 대한 빠른 분석 및 가시성 확보를 통한 근본 원인에 대한 빠른 추론

- 데이터 수집 통합
- 자동화된 분석
- 가시성 확보

### Amazon Detective 동작 원리

1. AWS 데이터 소스로부터 데이터 수집
2. 지속적으로 데이터를 그래프 모델로 병합
3. 데이터 분석
4. 분석 결과에 대한 시각화 및 내용에 대한 가시성 제공

### Amazon Detective 사용 사례

#### 경보 수준 조정 - 알람에 대한 분석

- 얼마나 많은 양의 데이터 전송이 이뤄졌는지?
- 이 데이터 패턴이 정상적인 것인지?
- 이전에 무슨 일이 벌어졌었는지?
- 현재 수준의 API 실패율이 정상적인 것인지?

#### 사고 분석 - 사고 연관 분석

- 특정 IP에서 발생된 API 호출 내역?
- 해당 호출이 정찰 활동과 관련된 것인지?
- 어떤 자격증명이 사용이 되었는지?
- 어떤 IP와 통신이 이뤄졌는지?

#### 위협 사냥 - 사고의 근본 원인 파악

- 위협 리포트내의 IP가 과거에 조직내 EC2 인스턴스와 통신한 이력이 있는지?
- 의심스러운 User Agent가 어떤 API 호출을 했는지?

## Security Hub

### Insights 및 규정 준수 확인

- 규정 준수 확인
- AWS 보안서비스나 3rd Party 보안 서비스에서 탐지한 다양한 보안 탐지 내역을 통합하여 모니터링
- 보안 트렌드에 대한 분석 및 발견된 보안 탐지 내역에 대한 가중치 기준 선별

### 보안 탐지 내역 제공 서비스

Inspector, GuardDuty, Macie, Config, MAnager, IAM Access Analyzer
