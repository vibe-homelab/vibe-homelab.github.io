# Vibe Homelab Stack (Docker Compose)

이 폴더는 **대시보드 + Vision/Voice Gateway**를 Docker 이미지로 빠르게 띄우기 위한 compose 파일을 제공합니다.

주의: Vision/Voice는 MLX 워커를 위해 **Host(로컬 머신)에서 Worker Manager가 먼저 실행**되어야 합니다.

## 1) Host Worker Manager 준비

### Vision Worker Manager (기본: `:8100`)

```bash
git clone https://github.com/vibe-homelab/vision-insight-api
cd vision-insight-api

./scripts/setup.sh
./scripts/install-service.sh

curl http://localhost:8100/health
```

### Voice Worker Manager (기본: `:8210`)

```bash
git clone https://github.com/vibe-homelab/voice-insight-api
cd voice-insight-api

make install-worker
make service-install
make service-start

curl http://localhost:8210/health
```

## 2) Stack 실행

`vibe-homelab.github.io` 레포 루트에서:

```bash
docker compose -f stack/docker-compose.yml up -d
```

## 3) 접속/확인

```bash
open http://localhost:4000

curl http://localhost:8000/healthz  # Vision Gateway
curl http://localhost:8200/healthz  # Voice Gateway
curl http://localhost:4010/healthz  # Dashboard Backend
```

## 4) 중지

```bash
docker compose -f stack/docker-compose.yml down
```
