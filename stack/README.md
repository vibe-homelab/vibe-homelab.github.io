# Vibe Homelab Stack (Docker Compose)

이 폴더는 **대시보드 + Vision/Voice Gateway**를 **사전 빌드된 Docker 이미지(GHCR)**로 빠르게 띄우기 위한 compose 파일을 제공합니다.

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

## (선택) API Key 인증

Vision/Voice Gateway에서 `/v1/*` 인증을 켠 경우, Dashboard에도 같은 키를 설정해야 합니다.

- Vision/Voice: `GATEWAY_API_KEY` 또는 각 서비스 `config.yaml`의 `gateway.api_key`
- Dashboard: `homelab-dashboard/backend/config.yaml`의 `services.<id>.api_key`

## 2) Stack 실행

`vibe-homelab.github.io` 레포 루트에서:

```bash
docker compose -f stack/docker-compose.yml pull
docker compose -f stack/docker-compose.yml up -d
```

> 만약 `pull` 단계에서 이미지가 아직 없다는 에러가 난다면,
> `pull`을 생략하고(또는 잠시 후 재시도) 개별 레포에서 로컬 빌드로 실행할 수 있습니다.

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

## Troubleshooting

| 증상 | 원인 | 해결 |
|---|---|---|
| Gateway 컨테이너가 시작되지 않음 | Host Worker Manager 미기동 | Vision: `curl http://localhost:8100/health`, Voice: `curl http://localhost:8210/health` |
| `host.docker.internal` 연결 실패(리눅스 등) | Docker/OS 차이 | compose의 `WORKER_MANAGER_HOST`/Dashboard 설정을 호스트 IP로 변경 |
