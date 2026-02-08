# Vibe Homelab

> AI-Powered Home Services with Vibe Coding

LLM Agent를 활용하여 홈랩 서비스를 구축하고 운영하는 오픈소스 프로젝트입니다.

## 🌐 Website

https://vibe-homelab.github.io

## 🎯 Mission

개인 홈랩 환경에서 AI 기반 서비스들을 self-hosted로 운영하여:
- 데이터 프라이버시 확보
- 클라우드 비용 절감
- AI 기술 학습 및 실험
- 일상 생활 자동화

## 🚀 Services

| Service | Description | Status |
|---------|-------------|--------|
| [vision-insight-api](https://github.com/vibe-homelab/vision-insight-api) | 이미지/영상 분석 API | 🔄 In Progress |
| [voice-insight-api](https://github.com/vibe-homelab/voice-insight-api) | 음성 인식/처리 API | 🔄 In Progress |
| document-insight-api | 문서 분석/처리 API | 📋 Planned |
| search-insight-api | 시맨틱 검색/RAG API | 📋 Planned |
| agent-hub | AI 에이전트 오케스트레이션 | 📋 Planned |
| [homelab-dashboard](https://github.com/vibe-homelab/homelab-dashboard) | 통합 모니터링 대시보드 | ✅ Active |

## 💡 Philosophy

### Vibe Coding
LLM Agent(Claude, GPT, Gemini 등)와 협업하여 코드를 작성합니다.
인간은 아이디어와 방향을 제시하고, AI가 구현을 담당합니다.

### Self-Hosted First
클라우드 의존성을 최소화하고 로컬 환경에서 모든 서비스를 운영합니다.

### Modular & API-First
각 서비스는 독립적으로 동작하며 REST API를 통해 상호 연결됩니다.

### Container Native
모든 서비스는 Docker 컨테이너로 패키징되어 일관된 환경에서 실행됩니다.

## 📚 Quick Start

```bash
# 1. 원하는 서비스 클론
git clone https://github.com/vibe-homelab/vision-insight-api
cd vision-insight-api

# 2. 환경 설정
# (선택) config.yaml에서 모델/메모리/포트를 조정할 수 있습니다.

# 3. 실행
make install

# 4. 확인
curl http://localhost:8000/healthz
```

## 🧱 Full Stack (Dashboard + Gateways)

미리 빌드된 Docker 이미지를 사용해 **Dashboard + Vision/Voice Gateway**를 한 번에 실행할 수 있습니다.

- Compose: `stack/docker-compose.yml`
- Guide: `stack/README.md`

```bash
git clone https://github.com/vibe-homelab/vibe-homelab.github.io
cd vibe-homelab.github.io

# Prerequisite: Vision/Voice Worker Managers are running on host (see stack/README.md)
docker compose -f stack/docker-compose.yml up -d

open http://localhost:4000
```

## 🖥️ Hardware Requirements

**Minimum:**
- CPU: 4 cores
- RAM: 8GB
- Storage: 50GB SSD

**Recommended:**
- CPU: 8+ cores
- RAM: 32GB
- Storage: 200GB NVMe
- GPU: NVIDIA RTX 3060+

## 🤝 Contributing

기여를 환영합니다! 다음 방법으로 참여할 수 있습니다:

- 🐛 버그 리포트
- 💡 새로운 기능 제안
- 📝 문서 개선
- 💻 코드 기여

## 📄 License

MIT License
