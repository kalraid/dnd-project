# DnD Projects

던전앤파이터(DnF) 파티·시세 도구에서 시작해 갤러리 커뮤니티까지 붙인 개인 웹 서비스입니다.
(2020-08 ~ 2021-02)

> 원래 [VRChatAINpc](https://github.com/kalraid/VRChatAINpc) 저장소 안에서 개발했고, 2026-11-09에 커밋 이력을 유지한 채 이 저장소로 분리했습니다.
> ETF 정보 기능(`fund` 패키지)은 게임과 상관없어서 [etfholdings](https://github.com/kalraid/etfholdings) 저장소로, 마비노기 도구(`mabinogi` 패키지)는 [mabi-look-matcher](https://github.com/kalraid/mabi-look-matcher)의 `legacy/mabinogi-tools-2020/`으로 옮겼습니다. 두 패키지는 이 저장소 이력에서도 지웠습니다.
> 분리하면서 이력 전체에서 API 키·DB 비밀번호·키스토어 비밀번호를 `***REMOVED***`로 바꿨고, 빌드 결과물(`bin/`, jar), 인증서 파일(`*.jks`, `*.p12`, `keys/`), chromedriver를 지웠습니다.

## 구성

| 경로 | 내용 | 스택 |
|---|---|---|
| `backend/` | REST API 서버 (원래 `DnDPartes`) | Spring Boot 2.3, Java 11, Gradle, JPA·MyBatis, MySQL, JWT |
| `frontend/` | 웹 화면 (원래 `dnd-project`) | Vue 2, Vuetify 2, Vuex, Vue Router, axios, GCP App Engine |

## 기능 (backend 패키지 기준)

- **party** — 던전앤파이터
  - `dndapi`: Neople Open API 연동 (경매장, 아바타 마켓, 캐릭터)
  - `dndOffApi`, `search`: 캐릭터 검색과 파티 구성용 데이터 (`dndOffApi`는 셀레니움으로 공식 사이트 크롤링)
  - `tensorflow/characterSpec`: 캐릭터 스펙 분석 실험
- **gallery** — 커뮤니티
  - 게시판·댓글(`board`), 그룹(`group`), 채팅(`chat`), 포인트(`point`), 회원(`user`)
  - OCR(`ocr`, Tess4J 한국어 데이터)
- **common** — JWT 인증 필터, API 접근 로그, 공통 페이징·예외 처리

## 실행

`backend/src/main/resources/application*.yml|properties`의 `***REMOVED***` 자리에 본인의 Neople API 키, DB 비밀번호, SSL 키스토어 정보를 넣어야 합니다. 셀레니움 기능을 쓰려면 `backend/src/main/resources/selenium/`에 chromedriver를 직접 받아 두세요.

```bash
# backend
cd backend && ./gradlew bootRun

# frontend
cd frontend && npm install && npm run dev
```

## 관련 저장소

- [VRChatAINpc](https://github.com/kalraid/VRChatAINpc): 이 프로젝트가 원래 들어 있던 저장소
- [etfholdings](https://github.com/kalraid/etfholdings): 여기서 함께 만들던 ETF 정보 기능(IEX Cloud API)을 따로 떼어 낸 저장소
- [dnfParty](https://github.com/kalraid/dnfParty): 2025년에 새로 만든 던전앤파이터 파티 관리 서비스 (이 프로젝트의 후속)
