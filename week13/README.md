GitOps - Git + Operations : Git으로 운영을 한다
Sync - 동기화
Drift - 표류 : 실제 상태가 선언에서 조금씩 벗어나는 것
Prune - 가지치기 : 관리하던 리소스가 Git에서 삭제되면 클러스터에서도 제거 
Self-heal - 자가 치유: Git 기준으로 되돌리기


PUSH 방식 / PULL 방식
PUSH 방식: CI 실행 주체에 배포 권한, 접속 경로가 필요.
		배포 기록이 남도록 파이프라인, 감시 로그를 따로 설계
		클러스터가 내부망에 있다면 접근이 힘듦.

PULL 방식: 클러스터 내 에이전트(CD)가 Git을 지켜보다가 바뀌면 적용
		외부에 클러스터 권한을 주지 않음.
		Git 히스토리로 기록 관리, selfHeal 가능, 되돌리기 간단.

--> PULL 방식이 대표적인 GitOps 방식


GitOps의 선언형 완성
 : 원하는 상태를 Git에 적어둬
  클러스터와 다르면 자동으로 맞춤.


CI -> CD 사이 필수 연결
1. CI가 새 이미지를 GHCR에 게시
2. deployment.yaml의 iamge:를 커밋태그로 바꾸는 PR을 머지
3. Argo CD가 바뀐 GIt을 감지해 배포


배포 전략
Argo CD 덕에 Git에 머지하면 자동으로 배포됨
만약) 새 버전에 버그가 있다면
--> 이런 상황을 대비해 여러 배포 전략이 있음

Recreate : 옛 Pod를 전부 내리고 새 Pod를 만듦
RollingUpdate : 새 Pod를 점진적으로 늘리며 기존 Pod를 점진적으로 줄임 / 기본값
Blue/Green : v2를 다 띄우고 이후 한 번에 전환
Canary : 일부에게만 v2를 제공, 지켜보다가 양호하면 v2를 늘리기


실험 전략
A/B 테스트
 : 배포 위에서 하는 실험
일부 대상에게는 조금 다른 서비스를 제공해 어느 방식이 나은지 비교

* Canary는 안전성 테스트, A/B는 더 나은 방식 테스트



모니터링

Metric : 측정값, 시간에 따라 기록한 숫자
Obsrvability : 관측 가능성, 바깥에서 보고 안의 상태를 알 수 있는 정도
Prometheus : 어두운 시스템 안을 밝혀주는 도구 = 데이터 수집
Grafana : graph + kibana / 메트릭을 그래프와 대시보드로 보여주는 시각화 도구

골든 시그널
 : 지연 / 트래픽 / 에러 / 포화
