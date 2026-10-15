kimyh@4-403-02:~/devops/guestbook$ docker compose ps
NAME                IMAGE            COMMAND                  SERVICE   CREATED          STATUS                    PORTS
guestbook-nginx-1   nginx:alpine     "/docker-entrypoint.…"   nginx     23 minutes ago   Up 23 minutes             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
guestbook-redis-1   redis:7-alpine   "docker-entrypoint.s…"   redis     39 minutes ago   Up 39 minutes (healthy)   6379/tcp
guestbook-web-1     guestbook-web    "python app.py"          web       6 minutes ago    Up 6 minutes (healthy)    5000/tcp

scale 후 화면 결과 -> img/

down 후 up, down -v 후 up 차이:
그냥 down만 하면 volume은 제거되지 않기 때문에 작성한 글은 남아있다.
하지만 down -v를 하게되면 volume까지 제거되기 때문에 작성한 글이 제거된 후 다시 시작된다.

.env를 Git에 올리지 않는 이유:
.env에는 비밀번호 등 Git에 올리면 문제가 될만한 사항들이 들어있다.
따라서 .gitignore에 .env를 넣어둬 Git에 올라가는 상황을 방지해야 한다.

-----------------------------------------------------------------------------------

Docker Compose

- 독립된 컨테이너들이 함께 동작하도록 구성 및 관리하는 도구
- 보통 컨테이너에는 역할 하나만 부여하기 때문에
이를 하나로 묶어주는 역할을 함.

- 원하는 서비스 구성을 YAML에 정의하고 Compose에 실행 및 관리를 맡기는 방식.

compose.yaml
- 여러 컨테이너를 연결하는 명령어를 반복해서 입력하는 대신 설정을 파일로 정의한 것

- 추천 순서 (외울 필요는 없이 그저 추천일 뿐)
	image, build
	command
	ports, expose
	environment
	volumes
	depends_on
	healthcheck
	restart
	develop
	

컨테이너를 통째로 지워도 데이터가 남아있다.
- Volume은 기본적으로 삭제되지 않기 때문.
  (Volume은 컨테이너 밖 호스트에 저장된다.)

.env
- 민감한 정보를 담아둠
- .gitignore로 업로드 방지

healthcheck
- redis가 완료될 때까지 시작을 보류하기 위해 사용

scale
- 컨테이너 인스턴스의 개수를 조절

nginx
- 리버스 프록시: 클라이언트 요청을 대신 받아 내부 서버에 전달
- 로드 밸런싱: 들어온 요청을 web들에게 분산

config
- ${...}가 다 채워진 최종 설정을 보여줌 (단, 컨테이너는 띄우지 않음)
  --quiet : 출력 없이 검사만
  -A1 : 검색된 줄과 아래 1줄을 같이 출력
	A: after, B: before, c: context(위, 아래) // ex) -B2: +아래 2줄

watch
- 파일을 지켜보다가 action을 통해 자동으로 작동하도록 가능
