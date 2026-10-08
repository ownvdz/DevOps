ghcr.io/ownvdz/guestbook:custom

# ---------------------------------------------------------------
# 학생 과제: 아래 각 줄이 무엇을 하는지 주석으로 설명을 달아보세요.
# ---------------------------------------------------------------

# 빌드 스테이지는 여기서부터 시작
FROM python:3.12-slim

# /app이 없으면 생성 (작업할 디렉토리)
WORKDIR /app

# requirements를 복사 및 txt파일 내에 적혀있는 필요내용들 다운로드
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 나머지 복사
COPY . .

# 빌드시 실행
RUN useradd -m appuser
USER appuser

# 환경변수 기본값
ENV APP_TITLE="김유현 DevOps 방명록" \
    THEME_COLOR="#66FF33"

# 포트번호
EXPOSE 5000

# 컨테이너 시작시 실행
CMD ["python", "app.py"]

#-------------------------------------------------

kimyh@4-403-02:~/devops/guestbook$ docker build -t guestbook:custom .
[+] Building 1.7s (11/11) FINISHED                                                              docker:default
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 537B                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.12-slim                                       0.1s
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 120B                                                                         0.0s
 => [1/6] FROM docker.io/library/python:3.12-slim@sha256:f77ac9e44ae96ef2c90b8053ea08c31f8be030f824196b0  0.1s
 => => resolve docker.io/library/python:3.12-slim@sha256:f77ac9e44ae96ef2c90b8053ea08c31f8be030f824196b0  0.1s
 => [internal] load build context                                                                         0.0s
 => => transferring context: 400B                                                                         0.0s
 => CACHED [2/6] WORKDIR /app                                                                             0.0s
 => CACHED [3/6] COPY requirements.txt .                                                                  0.0s
 => CACHED [4/6] RUN pip install --no-cache-dir -r requirements.txt                                       0.0s
 => [5/6] COPY . .                                                                                        0.1s
 => [6/6] RUN useradd -m appuser                                                                          0.5s
 => exporting to image                                                                                    0.6s
 => => exporting layers                                                                                   0.3s
 => => exporting manifest sha256:406ca6742e86b4efbd612aff032a90cc6f5f3abaa135b0fb1c72ba5773829195         0.0s
 => => exporting config sha256:8f0d81f3c10575a9d479383a1d5ee37fadfaa5b1fe4969c85a17d5bc899fb116           0.0s
 => => exporting attestation manifest sha256:0ba6d7695f4955d7f1623f62232782d802d64497f36b7e021b920a01a1f  0.0s
 => => exporting manifest list sha256:3a7d16ef1c32282e4d9b2e4377301b956d45d1f74e743c3a9ca1cceb4284051f    0.0s
 => => naming to docker.io/library/guestbook:custom                                                       0.0s
 => => unpacking to docker.io/library/guestbook:custom


# ---------------------------------------------------------------------------

app.py 기본값 수정은 코드에서 확정지음. 코드 수정 후 재빌드
Dockerfile env파일은 이미지 빌드 시점에 재빌드
docker run -e는 컨테이너 실행 시점에.
