설정 분리
	- 설정 분리의 이유 : 이미지는 하나만 만들고, 설정만 바꾸어서 여러 환경에서 사용.

	ConfigMap
	Secret

	무상태 (Stateless)
		Pod : 설정 - ConfigMap/Secret에서 받아옴
			데이터 - DB (Redis)에 저장
			로그 - 표준 출력으로 흘려 보냄

		-> 이런 상태를 '무상태' 라고 함
	
	base64
		아무 데이터나 글자로 안전하게 옮기려고 만든 표기법
		ex) $ echo -n devops1234 | base64
		     ZGV2b3BzMTIzNA==		# 인코딩

		     $ echo ZGV2b3BzMTIzNA== | base64 -d
                     devops1234				# 디코딩


	       인코딩 	/      암호화     /     해시
	표기방식 바꾸기 / 열쇠로 잠그기 / 지문 만들기
	

	Secret = 인코딩
	Secret을 쓰는 이유:
		kubectl get 화면에 바로 안 뜸 (실수 노출 방지)			# 진짜 보안은 아님
		설정과 비밀을 분리해서 관리


상태 점검
	- 왜 헬스체크를 하는가? : 앱은 살아있으나, 제기능을 하지 못하는 상태가 있음.
		무한루프에 빠진 경우 / DB 연결이 끊기는 경우 / 메모리 누수로 멈추는 경우
	
	프로세스는 살아있어서 쿠버네티스는 정상이라 생각, 하지만 사용자는 사용 불가
	-> 해결법 : 쿠버네티스가 주기적으로 상태를 물어보는 것. ex) 우리 앱의 '/healthz', '/readyz'


	프로브 (probe, 검사)
		liveness (live) - '살아있는가'					ex) GET /healthz
		readiness (ready) - '요청 받을 준비가 되었는가'		ex) GET /readyz
	

----------------------------------------------------------------------------------------------------

kimyh@4-403-02:~/devops/guestbook$ kubectl get secret guestbook-secret -o jsonpath='{.data.REDIS_PASSWORD}' | base64 -d; echo
devops1234

secret은 base64로 인코딩한 것일 뿐이므로 진짜 암호화가 아니기에 완전히 안전하지는 않다.
		
