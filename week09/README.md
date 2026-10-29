kimyh@4-403-02:\~/devops$ kubectl get nodes

NAME       STATUS   ROLES           AGE   VERSION

minikube   Ready    control-plane   92m   v1.37.0



kimyh@4-403-02:\~$ kubectl get pods -w

NAME                         READY   STATUS    RESTARTS   AGE

guestbook-858896d6cb-tfwv8   1/1     Running   0          3m14s

guestbook-858896d6cb-tfwv8   1/1     Terminating   0          4m6s

guestbook-858896d6cb-k7xrb   0/1     Pending       0          0s

guestbook-858896d6cb-tfwv8   1/1     Terminating   0          4m6s

guestbook-858896d6cb-k7xrb   0/1     Pending       0          0s

guestbook-858896d6cb-k7xrb   0/1     ContainerCreating   0          0s

guestbook-858896d6cb-k7xrb   0/1     ContainerCreating   0          0s

guestbook-858896d6cb-k7xrb   1/1     Running             0          1s



방명록 브라우저 화면은 img/ 폴더 안에



선언형이란,

기존에 사용하던 명령형은 어떻게 하라고 지시하는 것에 가까웠다면,

선언형은 어떤 상태를 유지하라고 선언하는 명령어이다.

(택시를 이용할 때,  여기서 좌회전, 저기서 우회전이라고 하는 대신 목적지를 말하는 것과 비슷)



막혔던 부분:

minikube start --driver=docker로 minikube를 실행하려고 했는데 문제가 발생함.

\-> 도커 데스크톱을 켠 상태에서 실행을 하니 해결됨







\-----------------------------------------------------------------------------------------------------------------------------------------------------------

kubectl

: 클러스터에게 명령을 보내는 명령줄 도구



minikube

: 노트북 안에 기본적으로 노드 1개의 클러스터를 만들어주는 도구



kind (Kubernetes IN Docker)

: 도커 컨테이너 안에 클러스터를 만드는 도구



\----------------------------------------------------------------------------------------------------------------------



쿠버네티스 (Kubernetes, k8s)

: 컨테이너화된 애플리케이션 배포, 확장, 관리를 자동으로 처리해주는 오픈소스 시스템



\- 오케스트레이션 : 여러 서버의 컨테이너들을 자동으로 배치하고 관리하기 (쿠버네티스가 표준)



\- 명령형 / 선언형

&#x09;명령형 : "이렇게 해라" / 어떻게? 지시		   ex) docker run -d nginx

&#x09;선언형 : "이런 상태를 원한다" / 무엇을 선언  	   ex) replicas: 3



&#x09;쿠버네티스는 명령형 명령어도 지원하지만, 원하는 상태를 선언하고 지속적인 유지가 핵심



\- 조정 루프 (reconcilation loop)

&#x09;'관찰 -> 비교 -> 조치' 를 반복

&#x09;ex) 원하는 상태 - Pod 3개, 현재 상태 - Pod 2개 -> 조정 : 부족한 1개를 생성해 원하는 상태로



\- 클러스터 (Cluster) : 1개 이상의 노드로 구성된 쿠버네티스 관리 환경 / 아키텍처를 다 외울 필요는 X

&#x09;Control Plan (본부 / 두뇌)

&#x09;	API Server : kubectl이 말을 거는 창구

&#x09;	Scheduler : Pod를 어느 노드에 놓을지

&#x09;	Controller : 원하는 상태와 다르면 수정

&#x09;	etcd : 모든 상태를 저장하는 DB



&#x09;노드

&#x09;	kubelet : Pod를 실제로 띄우는 관리자 (1 노드 당 1 kubelet)

&#x09;	Pod : 컨테이너를 감싼 최소 단위



&#x09;\* Control Plan이 각 노드에 지시를 내림

&#x09;  kubectl은 직접 컨테이너를 띄우지 않음 (kubectl은 등록만, 실행은 각 노드의 kubelet이)



\- Pod : 쿠버네티스가 다루는 가장 작은 단위

&#x09;대부분의 Pod 1개는 컨테이너 1개



\- 네임스페이스 : 한 클러스터를 여러 구역으로 나눠 쓰는 칸막이

&#x09;

\----------------------------------------------------------------------------------------------------------------



kubectl 명령어



&#x20;    kubectl 동사 무엇을 이름 옵션

ex) kubectl get pods mynginx -o wide

&#x09;

&#x09;동사	

&#x09;	get - 리소스 조회

&#x09;	describe - 하나를 자세히 본다

&#x09;	logs - 로그 조회

&#x09;	exec - 컨테이너 내부에서 명령어 실행

&#x09;	run / create - 생성

&#x09;	delete - 제거

&#x09;

&#x09;종류 (\* 줄여서 사용 가능)

&#x09;	pods (po)

&#x09;	deployments (deploy)

&#x09;	namespaces (ns)



&#x09;옵션

&#x09;	-o wide(넓게 보기), -w (실시간), -A (모든 네임스페이스)

&#x09;	-n (특정 네임스페이스), -l (레이블로 고르기)



\----------------------------------------------------------------------------------------



