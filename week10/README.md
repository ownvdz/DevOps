3층 구조
	       Deployment        >        ReplicaSet       >         Pod
	(버전관리, 롤링 업데이트)    개수 유지 담당         컨테이너 단위


YAML에서 기억해야 할 4가지
	apiVersion: apps/v1		# API 버전
	kind: Deployment		# 무엇을 할 것인가
	metadata:				# 이름표
		name: guestbook
	spec:					# 원하는 상태
		replicas:2
		selector:
	(생략)

	*apiVersion 확인 방법
	-> kubectl api-resources | grep -E "^deployments|^services"
	-E : 정규표현식, ^: 줄의 시작, |: OR 조건


template
	template / Pod 는 붕어빵 틀 / 붕어빵의 관계


label, selector
	lable : IP, 이름을 몰라도 레이블만으로 찾을 수 있게 해줌
	selector : 레이블로 골라내는 조건
	
	* label과 selector를 이용해 deployment와 service를 이어줌


Service
	Pod가 죽었다가 살아나면 IP 주소가 바뀌므로 Service로 고정된 이름과 IP를 제공

	서비스 타입
		서비스 이름 = DNS 주소
		port (서비스의 문)
		targetPort (컨테이너의 문)
	
	                     nodePort                   /                    port         /       targetPort
	(NodePort 타입일 때만) 서버에 있는 바깥 문 / 서비스 자신의 포트 / 요청을 받는 포트
