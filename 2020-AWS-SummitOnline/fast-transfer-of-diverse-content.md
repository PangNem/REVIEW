# AWS 서비스를 통하여 다양한 컨텐츠를 빠르게 전송하기

## 컨텐츠의 빠른 전송이 중요한 이유

사용자가 서비스를 이용하는 중 버퍼링 등이 걸리면, 서비스를 이탈할 확률이 높음.
비즈니스에 악영향을 미치게 된다.

## 엣지 로케이션을 이용하는 대표적인 서비스들

Amazon CloudFront
Amazon Global Accelerator

## Amazon CloudFront

사용자에게 최적의 로케이션을 찾아
정적인 컨텐츠는 캐시를 통해 전달
동적인 컨텐츠는 AWS 글로벌 네트워크를 통해 빠르게 전송

다른 AWS tjqltmdhk tnlqrp dusehd(aws waf, s3, media, ACM)
aws 리전 data transfer out 비용 면제의 효과

### 최적의 엣지 로케이션 연결하기

사용자가 isp dns resolver -> aws
여러 요소를 고려해 가장 최적의 아이피 주소 발행

### 캐시를 이용한 응답

3계층 구조
l1 - hot 컨텐츠 캐시
l2 - 대형 캐시 계층
l3 - 지속 연결

l3는 원본까지 연결을 하고 있어, 정보를 빠르게 가져올 수 있음.

### 동적인 컨텐츠의 가속

동적인 컨텐츠(api, 회원정보)

l3 계층과 오리진의 지속연결
엣지에서 tls 연결의 종단
l1 -> l3로 직접 연결

## Amazon Global Accelerator

- 고정된 ip로 엔드포인트 제공
- 다중 리전 구성에서 최적의 리전으로 연결
- aws 글로벌 네트워크를 통해 빠른 전송

다음과 같은게 CloudFront와 다름

- 상위 프로토콜에 무관하게 tcp / udp의 가속
- 캐시 기능 없음

### dns 관리가 필요없는 엔드포인트

엣지 로케이션 2개는 모두 동일한 ip

사용자에게 가까운 리전으로 접속

### 최적의 리전으로 트패릭 연결

다이얼 기능을 통해 2개의 트래픽 조절 가능

헬스 체크를 통한 자동 트래픽 제어

## 요약

컨쳍츠 전송의 지연은 비즈니스에 악영향
HTTP 어플리케이션은 Amazon CloudFront
Non-HTTP 어플레케이션은 Amazon Global Accelerator