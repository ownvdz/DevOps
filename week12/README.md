CI / CD
	CI : Continous Intergration ( 지속적 통합 )
		- 코드를 합칠 때마다 자동으로 검사, 빌드
		- 잘못된 코드가 main에 합쳐지지 않도록 함 / 자동 머지 차단은 아님

	CD : Continious Delivery ( 지속적 제공 )
		- 언제든 배포 가능한 상태 유지
	       Continious Deployment ( 지속적 배포)
		- 검증 통과한 변경을 운영 환경까지 자동 반영


	파이프라인 과정	( 중간에 실패 시 뒤 단계는 진행 X )
		
		코드 푸시 
		 ↓
	       	 CI			/		소스 가져오기 -> 검사 및 테스트
						    -> 이미지 빌드 -> 레지스트리에 푸시
		 ↓
		CD			/		쿠버네티스에 자동 배포


	검사 ( Lint )
		문법 검사 ( compileall )
			- 이 파일이 파이썬으로 읽히는가?
		린트 ( ruff, eslint, ... )
			- 읽히는데 버그가 있지 않은가?

		차이점 : ex) print(APP_TITL) 의 경우 ( 오타 난 경우 )
			문법 검사 : 통과, 실행은 실패
			Lint : 실행 안 하고도 잡아냄


	태깅 시 lastest는 계속 덮어씌워짐
	커밋 해시, 버전으로 태그하는 것이 좋음
