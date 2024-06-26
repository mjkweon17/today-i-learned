### 12 factor app
- SaaS 개발 방법론으로 애플리케이션이 Cloud 환경에서 올바르게 동작하기 위해 지켜야 하는 12가지 규칙
- CodeBase, Dependencies, Config, Backing services, Build&Release&Run, Process, Port Binding, Concurrency, Disposability, dev/prod parity, Logs, Admin Process

### SaaS의 특징
- 설정 자동화를 위한 절차(declarative)를 체계화하여 새로운 개발자가 프로젝트에 참여하는데 드는 시간과 비용을 최소화
- OS에 따라 달라지는 부분을 명확히 하고, 실행 환경 사이의 이식성을 극대화
- 클라우드 플랫폼 배포에 적합하고, 서버와 시스템의 관리가 필요없게 됨
- 개발 환경과 운영 환경의 차이를 최소화하고 민첩서을 극대화하기 위해 지속적인 배포가 가능함
- 툴, 아키텍쳐, 개발 방식을 크게 바꾸지 않고 scale up할 수 있음
- https://medium.com/dtevangelist/12-factors-%EB%9E%80-b39c7ef1ed30

### VM(가상 머신)
- 물리적 하드웨어 위에 가상화 기술을 사용하여 생성된 가상의 컴퓨터
- 자체 운영 체제(OS)를 가지며, 물리적 서버의 리소스(CPU, 메모리, 스토리지 등)를 가상화하여 분할 사용함
- 다양한 용도로 사용될 수 있으며, 각각의 VM은 독립적인 컴퓨팅 환경을 제공함
- 개발, 테스팅, 프로덕션 환경을 분리하거나, 다양한 애플리케이션을 격리하여 실행하는 데 사용될 수 있음
- 신속하게 배포, 확장, 관리할 수 있는 유연성을 제공
- VM의 모든 인스턴스는 VPC ghksruddptj wprhdgka
- AWS의 EC2

### VPC(가상 사설 클라우드)
- 클라우드 환경 내에서 사용자가 정의한 가상 네트워크
- 사용자는 VPC 내에서 자신만의 IP 주소 범위, 서브넷, 라우팅 테이블, 네트워크 게이트웨이 등을 설정하여, 마치 독립된 작은 클라우드처럼 관리할 수 있음
- 클라우드 리소스(가상 머신, 데이터베이스, 스토리지 등)를 위한 격리된 네트워크 환경을 제공함. 이를 통해 보안성과 관리 편의성을 높이며, 다른 VPC 또는 인터넷과의 연결도 세밀하게 제어할 수 있음
- 클라우드 리소스들 간의 네트워킹 및 보안 설정을 위한 기반이 되며, 기업이 클라우드에서 자신의 IT 인프라를 구축할 때 필수적인 요소