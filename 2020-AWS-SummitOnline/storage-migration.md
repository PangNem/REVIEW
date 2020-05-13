# AWS 스토리지 마이그레이션 서비스 및 대규모 데이터 전송 사례

## 클라우드로 데이터 전송

### 온프레미스 환경에서 스토리지 종류

- 블록 스토리지
- 파일 스토리지 (NAS의 방식)
- 오브젝트 스토리지 (HTTP 프로토콜로 접근)

### AWS에서 스토리지

EBS, EFS, FSx, S3

### 데이터 전송을 위한 고려사항

1. 어떤 데이터를 어느 스토리지로?
2. 한번만 전송? 또는 지속적 동기화?
3. 단방향? 또는 양방향?
4. 데이터량 및 가능한 전송시간은?
5. 네트워크 대역폭 제한은?

### AWS 마이그레이션 서비스

오프라인 - AWS Snowball Edge, Snowmobile
온라인 - AWS DataSync, AWS Transfer for SFTP, AWS Direct Connect
데이터베이스 - AWS Database Migration Service, CloudEndure an AWS Company

## 마이그레이션 서비스

Transfer for SFTP, DataSync, Storage Gateway, Snowball Edge

### Transfer for SFTP

완전 관리형 서비스로, Amazon S3로 SFTP를 통해 직접 파일을 송수신할 수 있도록 지원

### DataSync

데이터센터에서 온라인으로 쉽고, 자동화되고, 빠르게 데이터 전송

### Storage Gateway

온프레미스에서 무한의 클라우드 스토리지에 가상의 접근

세가지 게이트웨이 타입(파일, 볼륨 테잎)

### Snowball Edge

## 대량의 데이터 전송 사례

롯데의 온라인몰 통합 - Snowball로 이전한 사례

## 마무리

- 데이터 마이그레이션시 - 클라우드에서 목표 스토리지, 온라인 또는 오프라인 전송, 네트워크 대역폭 등 고려
- 다양한 마이그레이션 서비스 - DataSync, Transfter for SFTP, Storage Gateway, Snowball Edge
- 작은 파일이 많을 때는 대용량으로 뭉쳐서 전송
