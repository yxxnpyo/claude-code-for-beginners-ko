# 모듈 13: 언어 및 프레임워크 씹어먹기

**목표:** Python, JS, Go 등 언어를 가리지 않고 Claude Code에게 최고의 결과물을 뽑아내는 비법 배우기

**예상 소요 시간:** 45-60분

---

## 무엇을 배우게 되나요?

Claude Code에게 언어 장벽 따위는 없습니다. 이 모듈에서는 Python의 깔끔한 구조, TypeScript의 엄격한 타입시스템, Go의 고도화된 동시성 등 **언어별 최강의 베스트 프랙티스**를 어떻게 Claude에게 뽑아내는지 배웁니다. 이것만 제대로 던지면, 당신이 한 번도 안 써본 언어로도 시니어 급의 초기 구조를 찍어낼 수 있습니다.

---

## 레슨 1: 파이썬 (Python) 개발 세팅

데이터 분석, AI 머신러닝, 백엔드의 제왕입니다.

### 초기 프로젝트 폭파 셋팅

```
깔끔하고 완벽한 Python 프로젝트 뼈대 하나 빈 폴더에 생성해:
- 가상환경(venv) 세팅
- requirements.txt 의존성 목록
- src/ 내부 아키텍처 폴더 구조
- 테스팅은 무조건 pytest
- 코드 예쁘게 만드는 건 black
- 린팅(더러운 코드 잡기)은 pylint 
- 패키징은 setup.py 로 묶게 만들어
```

### FastAPI 초스피드 앱 찍어내기

FastAPI는 파이썬 백엔드의 희망입니다. Pydantic 타입 지원 덕에 Claude가 미친 듯이 코드를 잘 짜냅니다.

```
FastAPI 어플리케이션 전체 구조 짜봐. 필수 조건:
- 자동 API 문서화(Swagger) 통과하게
- Pydantic 모델로 데이터 방어벽 세우기
- 데이터베이스 쿼리는 비동기(Async)로 빠르게
- JWT 로그인 보안
- CORS 개방 설정
- Docker 돌리기 쉬운 세팅으로
```

---

## 레슨 2: 자바스크립트 / 타입스크립트 (JS/TS)

세상에서 제일 많이 쓰지만 제일 걸레짝 되기 쉬운 생태계입니다. 클로드를 통해 엄격하게 통제해야 합니다.

### Node.js (Express 백엔드)

```
Express 기반 TypeScript 백엔드 API 뼈대 찍어내:
- TypeScript 무조건 존나 엄격한 Strict 모드 켤 것
- Express 라우터에 전부 타입 명시해
- TypeORM (또는 Prisma) 써서 DB 구조 잡아
- 인증은 JWT
- 들어오는 쓰레기 데이터는 Zod 패키지로 쳐내
- 테스팅은 Jest
- ESLint랑 Prettier 구동 세팅 해
```

### Next.js (풀스택 괴물)

```
최신 버전 Next.js 어플리케이션 구축해:
- 무조건 최신 App Router 적용
- 서버 컴포넌트 적극 활용
- 하단 API 호출용 API Routes 추가
- 데이터 페치는 Server Actions 쓰기
- 인증은 NextAuth
- 데이터베이스는 Prisma
- CSS는 닥치고 Tailwind CSS
```

---

## 레슨 3: Go (Golang) 개발

### Go Web Server (속도의 제왕)

```
Go 언어 기반 웹 서버 앱 하나 기깔나게 뽑아 줘:
- 라우터는 Chi 프레임워크 쓸 것
- 각종 미들웨어 필수로 발라놔 (로깅, 서버 다운 뻗지않는 Recovery, CORS)
- DB는 sqlx나 GORM 둘 중 하나 골라서 세팅
- JWT 인증 로직
- 고도화된(Structured) 로그 남기기
- 셧다운 될 때 Graceful Shutdown(처리 중인거 다 끝나고 곱게 죽는) 세팅
```

---

## 레슨 4: Rust(러스트) 개발

**(※경고※) 러스트는 깐깐한 컴파일러(Borrow Checker) 때문에 클로드가 한 번에 완벽한 코드를 짜기 힘들 수 있습니다. 컴파일 에러 뜨면 당황하지 말고 에러 메시지를 클로드한테 긁어다 바치면 알아서 고쳐냅니다.**

### Rust CLI 도구 제작

```
Rust 언어로 터미널 조작하는 CLI 프로그램 짜줘:
- 명령행 파라미터 쪼개는 건 Clap 패키지 써
- 에러 컨트롤은 thiserror 나 anyhow 라이브러리로 감싸
- 파일 쓰고 읽는 IO 로직 추가
- JSON 파싱은 serde 패키지 써서 
- 문서 주석(rustdoc) 아주 기깔나게 달아놔!
```

---

## 레슨 5: Java & Spring Boot (자바)

치기 귀찮고 어마무시하게 긴 엔터프라이즈급 어노테이션 떡칠 코드들을 클로드가 모조리 대필해 줍니다.

```
Spring Boot 싹 다 뼈대 잡아내:
- 빌드는 Gradle 로
- Spring Data JPA 박아넣고
- 보안은 Spring Security + JWT
- 엔티티 Validation 제약조건 달아놓고
- 전역 Exception 오류 처리 빈(Bean) 세팅
- Swagger (OpenAPI) 문서 자동 생성
- Docker 세팅까지 완벽하게
```

---

## 레슨 6: 하이브리드(Polyglot) 다중 언어 짬뽕 프로젝트

파이썬 백엔드 API 서버를 띄우고 프론트 화면은 React로 띄울 때. 이게 클로드의 진가가 드러나는 영역입니다.

```
나 지금 다국어 연합군 프로젝트 만들고 있어:
- 파이썬 머신러닝 분석 서비스 (FastAPI)
- 중간 문지기 서버 Go API Gateway
- 유저 화면은 Node.js (Next.js)

도와줘:
1. 이거 다 담을 Monorepo(모노레포) 폴더 구조 찢어봐
2. 한 방에 다 켤 수 있게 Docker Compose 구성해
3. 언어가 다른데 통신할 수 있게 공용 타입(Contract/DTO) 설계안 내놔보고
4. 서비스끼리 내부 네트워킹 통신(HTTP/gRPC)은 어떻게 할지 뼈대 짜!
```

---

## 레슨 7: 각 언어별 시니어 개발자의 "코드 감리(Review) 지시" 스킬

각 언어마다 고유의 사투리(관습)가 있습니다. 클로드에게 리뷰를 맡길 때 이 관습 스위치를 켜주면 기가 막힌 참견을 합니다.

### 파이썬 전문 꼰대스위치 켬

```
내 파이썬 코드들 다 스캔하고 쫙 까봐. 기준점:
- PEP 8 (파이썬 표준 코딩 스타일) 위반 잡기
- 타입 힌트(Type hints) 안 달아놓은 무적권 다 지적해
- Class나 함수에 Docstring 주석 빼먹은 곳
- 미련하게 for 문 돌리지 말고 '리스트 컴프리헨션' 치환 가능한 곳
```

### TypeScript 전문 꼰대스위치 켬

```
내 TypeScript 전부 감사(Audit)해. 기준점:
- `any` 타입 쓴 곳 무조건 색출해서 줘 패기
- var 쓴 곳 색출
- 거지 같은 콜백 함수들 전부 Async/Await 로 업그레이드
- 리액트면 Error Boundaries 똑바로 세팅 안 한 곳 지적
```

---

## 모듈 13 요점 체크리스트

모듈 14로 넘어가기 전:

- [ ] 파이썬(FastAPI), TS(React), Go, Java 등 프레임워크의 코어 뼈대를 주문할 수 있다.
- [ ] 다수의 언어가 뒤섞인 미친 구조도 Docker를 앞세워 묶을 수 있다.
- [ ] Rust 처럼 빡센 언어의 컴파일 에러를 AI에게 던져 해결하는 근성을 가졌다.
- [ ] 언어에 맞는 맞춤형 '코드 감리(Code Review) 가이드'를 클로드에게 명령할 수 있다.

---

*모듈 13 완료*
