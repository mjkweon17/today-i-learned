### 쿠버네티스
- 쿠버네티스는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 플랫폼. 
- 도커와 같은 컨테이너 도구를 사용해 애플리케이션을 컨테이너로 패키징하고 실행하는 것은 시작에 불과. 
- 애플리케이션을 대규모로 운영하려면 컨테이너의 배포, 관리, 확장, 네트워킹 설정 등을 효율적으로 처리할 수 있는 추가 도구가 필요함. 바로 여기서 쿠버네티스의 역할이 시작됨
TODO: 컨테이너를 확장할  이유가 뭐지? 시나리오가 필요해.
- 도커와 쿠버네티스는 서로 보완적인 관계에 있음. 도커는 애플리케이션을 컨테이너화하는 데 필요한 도구를 제공하고, 쿠버네티스는 이러한 컨테이너들을 대규모로 관리하는 데 필요한 플랫폼을 제공함. 따라서, 복잡하고 다양한 서비스를 운영하고 이를 효율적으로 관리하고자 한다면 쿠버네티스 학습은 매우 가치 있는 투자가 될 것.
TODO: 다양한 서비스를 운영한다는 시나리오

### 컨테이너를 확장해야 하는 이유
애플리케이션을 운영하면서 컨테이너를 확장하는 이유는 주로 애플리케이션의 성능, 가용성, 안정성을 개선하고 비즈니스 요구 사항을 충족시키기 위함입니다. 컨테이너 기술과 오케스트레이션 도구(예: 쿠버네티스)를 사용하여 확장성을 관리함으로써, 다양한 상황에서 애플리케이션의 요구를 만족시킬 수 있습니다. 다음은 컨테이너를 확장할 주요 이유들입니다:

- 트래픽 증가 대응
    - 사용자 기반의 성장이나 이벤트 기반 트래픽 증가로 인해 애플리케이션에 더 많은 요청이 발생할 수 있습니다. 이러한 경우, 컨테이너를 추가로 확장하여 처리 용량을 증가시키고, 사용자 요청에 신속하게 응답할 수 있습니다.
- 높은 가용성 유지
    - 여러 인스턴스에 걸쳐 애플리케이션을 분산시킴으로써, 단일 장애 지점(Single Point of Failure, SPOF)을 제거하고 가용성을 향상시킬 수 있습니다. 특정 컨테이너나 노드에 문제가 발생하더라도, 다른 컨테이너 인스턴스가 트래픽을 처리하여 애플리케이션의 중단 없이 서비스를 지속할 수 있습니다.
- 리소스 효율성 증가
    - 컨테이너를 동적으로 확장하거나 축소함으로써, 실제 트래픽과 요구 사항에 따라 필요한 리소스를 최적화할 수 있습니다. 이는 불필요한 리소스 낭비를 줄이고 비용 효율성을 높이는 데 도움이 됩니다.
- 지연 시간 감소
    - 글로벌 사용자 기반을 가진 애플리케이션의 경우, 다양한 지역에 컨테이너 인스턴스를 배포하여 지역별 사용자에게 더 가까운 서버에서 요청을 처리하게 함으로써 지연 시간을 감소시킬 수 있습니다.
- 배포와 업데이트의 용이성
    - 컨테이너 확장성을 이용하면 새로운 버전의 애플리케이션을 점진적으로 배포하고 테스트할 수 있습니다. 트래픽 일부를 새로운 버전으로 전환하면서, 문제가 발생할 경우 신속하게 롤백할 수 있어, 안정적인 서비스 제공이 가능합니다.
- 성능 최적화
    - 컨테이너를 특정 작업이나 서비스에 특화되도록 분리하고 확장함으로써, 전체 애플리케이션의 성능을 최적화할 수 있습니다. 예를 들어, 데이터베이스, 웹 서버, 캐시 등을 별도의 컨테이너로 분리하여 관리하고 확장할 수 있습니다.

### 쿠버네티스를 사용하는 이유
1. 자동화된 롤아웃과 롤백
   - 쿠버네티스를 사용하면 애플리케이션의 배포 및 업데이트 과정을 자동화할 수 있음. 오류가 발생했을 때 이전 버전으로 롤백하는 것도 간단.
   TODO: 어떻게 이전 버전으로 롤백하는 것이 간단하는 거지?
2. 스케일링
   - 트래픽이 증가하거나 감소할 때 쿠버네티스는 애플리케이션을 자동으로 확장하거나 축소할 수 있음. 이는 수동으로 컨테이너 인스턴스를 추가하거나 제거하는 번거로움을 줄여줌
3. 로드 밸런싱과 서비스 디스커버리
   - 쿠버네티스는 자동으로 컨테이너에 IP 주소와 하나의 DNS 이름을 할당함. 여러 컨테이너 간에 트래픽을 분산(로드 밸런싱)할 수 있으므로, 애플리케이션이 더 높은 가용성과 안정성을 가질 수 있습니다.
   TODO: 컨테이너에 IP 주소하고 DNS 이름을 할당한다는 것이 뭐야?
4. 자가 치유(Self-healing)
   - 쿠버네티스는 실패한 컨테이너를 자동으로 재시작하고, 정의된 사용자의 상태와 다르게 동작하는 컨테이너를 교체하며, 준비되지 않은 컨테이너로의 트래픽을 차단합니다.
5. 시크릿과 구성 관리
   - 쿠버네티스를 사용하면 비밀번호, OAuth 토큰, ssh 키와 같은 민감한 정보를 컨테이너에 안전하게 저장하고 관리할 수 있음. 구성 정보를 이미지로부터 분리하여 애플리케이션 구성을 변경하지 않고도 애플리케이션 스택의 구성을 업데이트할 수 있음.

### 쿠버네티스 사용 시기
- 다중 컨테이너 애플리케이션을 운영할 때: 단일 컨테이너 애플리케이션의 경우 쿠버네티스의 복잡성이 과할 수 있음. 하지만 여러 컨테이너로 구성된 복잡한 애플리케이션을 관리해야 한다면 쿠버네티스가 큰 도움이 됨.
TODO: 다중 컨테이너를 사용해야 할 이유가 왜 있어
- 클라우드 환경에서 애플리케이션을 운영할 때: 쿠버네티스는 클라우드 환경과 잘 통합되어, 여러 클라우드 제공업체에서 호스팅할 수 있음.
- 자동화된 확장, 관리, 업데이트가 필요할 때: 쿠버네티스는 이 모든 과정을 자동화하므로, 인프라 관리에 소요되는 시간과 노력을 크게 줄일 수 있음.
    TODO: docker를 사용해도 GitHub Actions 같은 도구들을 이용하여 CI/CD 파이프라인 구축하면 자동화할 수 있는 게 아닐까? 쿠버네티스를 활용해야 하는 이유를 도저히 모르겠어.
