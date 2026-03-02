# 모듈 11: MCP 서버 - Claude Code 한계 돌파 확장팩

**목표:** Model Context Protocol (MCP) 서버를 직접 설치하고 내 프로젝트 도구를 쥐여주며, Claude Code를 범용 AI에서 완전한 맞춤형 괴물 비서로 진화시키는 법 배우기

**예상 소요 시간:** 45-55분

---

## 무엇을 배우게 되나요?

이 모듈은 Claude Code가 단순히 "코딩 좀 치는 알바생"에서 "회사 내부망 DB, 최신 문서 검색, 실제 크롬 브라우저 조작까지 다 하는 만능 사원"으로 승급하는 비법을 다룹니다. MCP가 무엇인지, 어떻게 설정 파일을 엮는지, 필수로 깔아야 할 알짜배기 확장팩은 뭔지, 그리고 정 안 되면 내가 직접 커스텀 서버를 만들어 붙이는 법까지 배웁니다.

---

## 레슨 1: MCP가 도대체 뭡니까?

### MCP의 핵심

**Model Context Protocol (MCP)** 은 한마디로 Claude Code에게 쥐여주는 **외부 접속용 USB 포트 확장팩**입니다. 기본 Claude Code도 똑똑하지만, 여러분의 회사 보안 내부 데이터베이스나 최신 버전의 생소한 언어 공식 문서 같은 건 모릅니다.

MCP 서버 플러그인을 끼우면, Claude가 눈을 뜨고 직접 여러분의 로컬 데이터베이스를 조회하거나 실시간 인터넷 공식 문서를 긁어옵니다.

---

### 왜 써야 하나요?

이거 없으면, 에러 뜰 때마다 여러분이 직접 DB 쿼리 결과 복사해서 채팅창에 붙여넣기 해야 합니다.
이걸 깔아두면, Claude가 "음, 에러 났네요? 제가 직접 DB 테이블 조회해보고, 깃헙 통신해서 확인해 볼게요" 라며 지가 알아서 쑤시고 파헤칩니다. **사용해 보면, 안 쓰던 시절로는 절대 못 돌아갑니다.**

---

## 레슨 2: MCP 서버 플러그인 설치하기

### 설정(Config) 파일 위치

MCP 서버 설정은 아주 심플한 JSON 파일 두 곳에 저장됩니다.

팀원 다 같이 쉐어하는 **프로젝트 전용 설정:**

```
.mcp.json    # 내 프로젝트 폴더 한가운데 위치 (Git에 올려 공유)
```

나 혼자 몰래 전역으로 쓰는 **글로벌 유저 설정:**

```
~/.claude/settings.json    # 이 파일 안쪽에 "mcpServers" 공간
```

웬만하면 프로젝트 전용(`.mcp.json`)을 쓰세요. 팀원들이 이 프로젝트를 클론받을 때 똑같이 똑똑한 AI 세팅을 누릴 수 있습니다.

### 설정 파일 작성 예시

프로젝트(`.mcp.json`):

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/접근허용할/절대폴더경로"]
    }
  }
}
```

---

### 가장 쉽게 MCP 까는 꿀팁

JSON 칠 줄 몰라도 됩니다. Claude Code한테 그냥 던지세요:

```
내 프로젝트에 filesystem MCP 서버 좀 깔고 연동해 줘. 
내 /home/user/projects 경로에 접근할 권한도 같이 세팅해 놓고 알아서 다 쳐!!
```

이러면 Claude가 알아서 JSON 파일 작성하고, 연결 확인까지 보고합니다.

---

## 레슨 3: 무조건 깔아야 하는 공인 기초 MCP들

### 1) Filesystem (파일 시스템) MCP 서버

현재 열려있는 프로젝트 폴더 외곽에 있는 다른 동네 파일들에 접근 권한을 줍니다.

```json
// 세팅 생략 (위의 예시 참조)
```

**명령법:**

```
filesystem MCP 서버 도구 써서 내 바탕화면에 있는 Python 파일 좀 싹 찾아봐.
```

---

### 2) PostgreSQL / SQLite (데이터베이스) MCP 서버

Claude가 내 로컬/서버 DB에 빨대를 꽂고 직접 테이블을 조회하게 해줍니다.
더 이상 "쿼리 결과 복붙" 같은 원시적인 짓거릴 안 해도 됩니다.

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "POSTGRES_URL": "postgresql://ID명:비번@localhost:5432/DB이름"
      }
    }
  }
}
```

**명령법:**

```
postgres MCP 서버 연결해서, 저기 users 테이블 구조(Schema) 좀 싹 다 까서 보여줘 봐.
```

---

### 3) GitHub (깃허브) MCP 서버

내 터미널을 안 떠나고 클로드가 내 깃허브 API를 조작(PR생성, 이슈 생성 등)합니다.

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "여러분의-개인-인증-토큰값"
      }
    }
  }
}
```

---

## 레슨 4: 진짜 시간 아껴주는 "사기급" 미친 MCP 3대장

수많은 쓸데없는 MCP가 떠돌지만, 아래 3개는 당신의 코딩 인생을 바꿉니다.

### 1대장: Context7 (실시간 공식 문서(Docs) 강제 주입기)

AI 최대 질병인 '환각(없는 함수를 지어내는 병)'을 고치는 특효약입니다. Context7은 항상 최신 버전의 라이브러리 공식 문서를 실시간 웹에서 긁어와서 Claude 뇌에 주입합니다.

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@context7/mcp-server"]
    }
  }
}
```

**써보세요, 장담하건대 이거 하나로 스트레스 90%가 소멸합니다.**

---

### 2대장: Playwright (보이지 않는 브라우저 자동 조작)

웹사이트 프론트 화면을 조작하거나 테스트하고 싶나요? 이걸 까는 순간 Claude가 백그라운드에서 진짜 브라우저 화면을 띄워서 버튼 누르고, 폼 채우고, 렌더링 검사까지 알아서 다 합니다.

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-playwright"]
    }
  }
}
```

---

### 3대장: Claude in Chrome (내가 보는 크롬 디버깅 모드)

이건 Playwright 랑 다릅니다. 백그라운드 가상 브라우저가 아니라, **방금 내 눈앞에 에러 터져있는 '내 실제 크롬 브라우저 창'**의 F12 화면 로그, 네트워크 요청 등을 Claude가 직접 들여다보게 접속 권한을 줍니다.

```json
{
  "mcpServers": {
    "chrome": {
      "command": "npx",
      "args": ["-y", "@anthropic/claude-in-chrome-mcp-server"]
    }
  }
}
```

### [중요] 사공이 많으면 배가 산으로 간다

너무 많은 MCP를 덕지덕지 달지 마세요. 부팅 속도만 짜증 나게 느려집니다. Context7을 메인으로 달고, 필요할 때 크롬이나 DB를 붙이는 식으로 3~4개만 콤팩트하게 쓰세요.

---

## 레슨 5: 내가 직접 '커스텀 MCP 서버' 만들어 꽂기

기존에 풀린 툴 중에 우리 회사 내부 보안망 API를 조작하는 MCP 따윈 없습니다. 그럼 직접 10분 만에 짜서 연동하면 그만입니다. Node.js 스크립트 하나 짤 줄 알면 뚝딱입니다.

### 날씨(Weather) 조회용 미니 MCP 서버 직접 만들기 실습

Claude에게 커스텀 도구(Tool)를 뚫어봅시다.
`weather-mcp-server.js` 파일을 만들고 아래 코드를 박습니다:

```javascript
// weather-mcp-server.js
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// 1. 서버 인스턴스 뼈대 선언
const server = new McpServer({
  name: "weather-custom",
  version: "1.0.0"
});

// 2. Claude가 호출할 무기(Tool) 하나 등록해 줍니다.
server.tool(
  "get_weather", // 도구 이름
  { city: z.string().describe("도시 이름") }, // 클로드가 던져줘야 할 파라미터 규격
  async ({ city }) => {
    // 실제 날씨 API 통신 로직
    const response = await fetch(`https://api.weather.com/...?city=${encodeURIComponent(city)}`);
    const data = await response.json();

    // 클로드에게 JSON 문자열 세트로 가공해서 토스!
    return {
      content: [{
        type: "text",
        text: JSON.stringify({ temp: data.temp, cond: data.conditions }, null, 2)
      }]
    };
  }
);

// 3. 터미널 I/O를 통해 클로드 코드와 영혼의 통신망 연결
const transport = new StdioServerTransport();
await server.connect(transport);
```

### 이 커스텀 서버를 내 Claude Code와 합체시키기

`.mcp.json` 에 내가 짠 파일을 npx가 아닌 node 로 구동하라고 박아주면 끝입니다.

```json
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["/절대/경로/weather-mcp-server.js"],
      "env": {
        "WEATHER_API_KEY": "내_진짜_날씨_API_비빌키"
      }
    }
  }
}
```

이제 Claude 에 대고 말해봅시다:

```
weather MCP 서버 도구 켜서 서울 날씨 좀 가져와 봐.
```

클로드는 방금 여러분이 만든 자바스크립트 엔진을 돌려 서울 날씨를 가져와 브리핑합니다.

---

## 레슨 6: MCP 고인물용 핵심 기능 (Resources & Prompts)

MCP는 단순 '도구 호출(Tools)'만 하는 게 아닙니다.

### 1) 자원(Resources) 통째로 읽기 전용으로 열어두기

절대 변하지 않는 사내 직원 명부 DB나 문서들 있죠? 클로드 호출 시 언제든 읽어볼 수 있는 서재(Resource)로 열어둘 수 있습니다.

```javascript
server.resource(
  "company://employees",
  async (uri) => {
    // DB에서 직원 리스트 긁어옴
    const employees = await db.query('SELECT * FROM employees');
    return { contents: [{ uri: uri.href, text: JSON.stringify(employees) }] };
  }
);
```

### 2) 기업용 커스텀 프롬프트 템플릿(Prompts) 강제 지정

코드 리뷰 시 "우리 회사 코딩 표준 문서"를 무조건 읽고 검사하라고 템플릿을 고정시킬 수 있습니다.

```javascript
server.prompt(
  "company_code_review",
  { filename: z.string() },
  async ({ filename }) => {
    const 룰북 = await loadCompanyStandards(); // 사내 규정 불러오기
    return {
      messages: [{ role: "user", content: { type: "text", text: `${filename}을 리뷰하는데 다음 사내 규정을 강제해:\n${룰북}` } }]
    };
  }
);
```

---

## 레슨 7: 명심보감 (MCP 사용할 때 조심할 점)

- **보안 (Security)**: API 비밀키, DB 접속 정보 절대 하드코딩하지 마십시오! 환경변수(.env)로 빼세요.
- **클로드를 맹신하지 마라**: "오오, 이거 쓰면 내가 안 눌러도 클로드가 우리 서버 배포(Deploy) API 직접 때려서 런칭도 해주겠네?" → **자살행위입니다.** 클로드가 실수로 서버 날려버릴 수 있습니다. 수정이나 파괴가 들어가는 권한은 절대 쥐여주지 말고 오직 R(Read)만 주십시오.
- **에러 핸들링**: 당신이 만든 Custom MCP가 에러를 뿜으면 (try/catch 누락), 클로드 전체의 뇌가 멈추고 뻗습니다. 예외처리 빡세게 방어막 두르세요.

---

## 모듈 11 요점 체크리스트

모듈 12 로 넘어가기 전:

- [ ] MCP 서버 세팅 파일(.mcp.json) 위치와 구동 개념을 이해했다.
- [ ] 파일 시스템, 데이터베이스, 깃허브 등 알짜배기 기본 MCP를 킬 줄 안다.
- [ ] Context7 나 Playwright 같은 미친 효율의 MCP를 내 작업에 더할 수 있다.
- [ ] 직접 Node.js 등 스크립트로 나만의 커스텀 API MCP를 빌드하고 꽂을 수 있다.
- [ ] MCP 개발 시 보안(Secret, Auth) 수칙을 지킨다.

---

*모듈 11 완료*
