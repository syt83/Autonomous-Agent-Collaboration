# Autonomous-Agent-Collaboration
> **Ollama 기반의 고성능 멀티 에이전트 오케스트레이터** > 팀장(Boss)과 분야별 전문가(Worker) 에이전트들이 협업하여 복잡한 과제를 해결하는 지능형 시스템입니다.

---

## 🚀 프로젝트 개요
사용자의 복잡한 질문을 단일 AI가 처리할 때 발생하는 정보의 얕음과 논리적 오류를 해결하기 위해, **계층적 멀티 에이전트 시스템(Hierarchical Multi-Agent System)**을 구축했습니다.

- **Frontend:** Streamlit
- **Backend:** Python (Asyncio)
- **AI Engine:** Ollama (DeepSeek-Coder 6.7B, Llama 3.2 등)
- **Architecture:** Boss-Worker Pipeline

---

## 🛠️ 핵심 트러블슈팅 (Troubleshooting)

개발 과정에서 마주한 기술적 한계와 해결 방안입니다.

### 1. Windows 환경에서의 비동기 프로세스 제어 문제
- **문제:** `asyncio`를 이용해 여러 에이전트를 동시에 실행할 때 Windows 환경에서 `NotImplementedError` 발생.
- **해결:** `WindowsProactorEventLoopPolicy`를 명시적으로 설정하여 윈도우 터미널에서도 안정적인 비동기 서브프로세스 제어가 가능하도록 최적화했습니다.

### 2. 에이전트 간 데이터 누수 및 템플릿 치환 오류
- **문제:** 런타임에서 `{{issue.title}}`과 같은 템플릿 변수가 실제 데이터로 치환되지 않고 에이전트에게 전달되는 현상 발생.
- **해결:** 문자열 파싱 로직을 정교화하고, f-string과 런타임 replace 로직의 우선순위를 재설계하여 정확한 명령 전달 체계를 구축했습니다.

### 3. 멀티 에이전트 응답 파싱 및 UI 렌더링 에러
- **문제:** 보스 에이전트의 응답이 비정형적일 경우 사원 에이전트에게 작업 할당이 실패하며 `StreamlitInvalidColumnSpecError` 발생.
- **해결:** 데이터 유효성 검사 로직을 추가하고, 에이전트 응답이 없을 경우를 대비한 예외 처리(Fallback) 로직을 구현하여 시스템 안정성을 높였습니다.

---

## 📈 앞으로의 로드맵 (Future Upgrades)

현재의 시스템을 넘어 더 강력한 기능을 추가할 예정입니다.

- [ ] **Role-Specific 전문가 라이브러리:** 로봇 공학(SLAM, Control), 일본 시장 분석, 임베디드 설계 등 특화된 사원 페르소나 구축.
- [ ] **에이전트 메모리 시스템:** 이전 대화 내용을 기억하여 연속적인 작업 수행이 가능하도록 컨텍스트 관리 기능 강화.
- [ ] **RAG(Retrieval-Augmented Generation) 통합:** 외부 기술 문서(PDF, 웹사이트)를 실시간으로 참조하여 답변의 정확도 향상.
- [ ] **다국어 최적화:** 일본 현지 기업 및 시장 분석을 위한 일본어 특화 에이전트 모드 추가.

---

## ⚙️ 시작하기 (Setup)
1. Ollama 설치 및 모델 다운로드 (`ollama run deepseek-coder:6.7b`)
2. `pip install -r requirements.txt`
3. `streamlit run app.py`

---

## 📄 License
이 프로젝트는 **MIT License**를 따릅니다.
