# ERDCloud for Claude Code

[English](#english) | [한국어](#한국어)

## English

A [Claude Code](https://claude.com/claude-code) plugin marketplace for [ERDCloud](https://www.erdcloud.com), the web-based ERD (Entity Relationship Diagram) modeling service.

### Plugins

| Plugin | Description |
|---|---|
| `erdcloud` | Connects Claude Code to the ERDCloud MCP server so Claude can read and edit your diagrams (tables, columns, relations, domains, memos), draw sequence diagrams, flowcharts, UML class diagrams and free-form shapes, and teaches Claude the right order of operations. |

What `erdcloud` contains:

- **MCP server** `erdcloud` -> `https://www.erdcloud.com/mcp`
- **Skill `erd-modeling`**: domain-first workflow, relationship workflow, and tool overview. Loaded automatically when you work on an ERD.
- **Skill `erd-from-sql`** (`/erdcloud:erd-from-sql <diagram URL> [file or description]`): build a diagram from SQL DDL or a description.
- **Skill `canvas-diagrams`**: which tool to use for sequence diagrams, flowcharts, UML class diagrams and free-form shapes, and how to edit the result. Loaded automatically.
- **Skill `diagram-from-description`** (`/erdcloud:diagram-from-description <diagram URL> <sequence|flowchart|class> <description or path>`): draw a sequence diagram, flowchart or UML class diagram from a description or from source code.

### Install

1. Start Claude Code and install the plugin. In Claude Code 2.1.275 or later one command does both steps:

   ```
   /plugin install erdcloud --marketplace erdcloud/erdcloud-claude-plugin
   ```

   Or, in two steps (any version):

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

2. Restart Claude Code, run `/mcp`, select `erdcloud` and sign in to ERDCloud in the browser window that opens. Review the permission screen and click **Allow**. No token to copy.

   No ERDCloud account yet? On the sign-in page choose **Google** or **GitHub**: an account is created automatically on your first sign-in and you return to the permission screen. If you sign up with an email address instead, verify the email first and then run `/mcp` again in Claude Code.

3. Try it:

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<your diagram id> an online shop with users, orders and products
   ```

   Other diagrams on the same canvas:

   ```
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<your diagram id> sequence login with a token check
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<your diagram id> flowchart order approval with a manager and a finance lane
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<your diagram id> class src/domain
   ```

### Permissions and security

- Claude can only access ERDs you could access yourself: ERDs you own and ERDs of teams you are an accepted member of. Public ERDs of other people are read-only. Even an ERDCloud administrator account cannot read or edit other people's private or team ERDs through this connection.
- Access tokens are short-lived (1 hour) and renewed automatically. A connection expires after at most 90 days, then you sign in again.
- You can review and disconnect connected apps at any time in ERDCloud: open a diagram, then the **AI (MCP)** panel, **Connected apps**. Disconnecting takes effect immediately.
- AI edits are applied live and can be wrong. Create a Snapshot or export a backup in ERDCloud before large changes.

### Troubleshooting

- **401 / unauthorized / "needs authentication"**: run `/mcp`, select `erdcloud` and sign in again (the connection expired or was disconnected).
- **Tools not listed**: run `/mcp` and check that `erdcloud` is connected.
- **Tools that do not support OAuth (or CI)**: use an access token instead of this plugin. Generate one in the ERDCloud **AI (MCP)** panel and add the server manually, for example `claude mcp add --transport http erdcloud https://www.erdcloud.com/mcp --header "Authorization: Bearer <token>"`. Do not commit the token.

### License

[MIT](LICENSE). The ERDCloud service itself is governed by its [Terms of Service](https://www.erdcloud.com/static/html/terms.html) and [Privacy Policy](https://www.erdcloud.com/static/html/privacy.html).

---

## 한국어

[ERDCloud](https://www.erdcloud.com)(웹 기반 ERD 모델링 서비스)용 [Claude Code](https://claude.com/claude-code) 플러그인 마켓플레이스입니다.

### 플러그인

| 플러그인 | 설명 |
|---|---|
| `erdcloud` | Claude Code를 ERDCloud MCP 서버에 연결해 다이어그램(테이블, 컬럼, 관계, 도메인, 메모)을 읽고 편집하게 하고, 시퀀스 다이어그램·플로우차트·UML 클래스 다이어그램·도형을 그리게 하며, 올바른 작업 순서를 Claude에게 알려줍니다. |

포함 내용:

- **MCP 서버** `erdcloud` -> `https://www.erdcloud.com/mcp`
- **스킬 `erd-modeling`**: 도메인 우선 워크플로, 관계 생성 워크플로, 도구 목록. ERD 작업 시 자동으로 적용됩니다.
- **스킬 `erd-from-sql`** (`/erdcloud:erd-from-sql <다이어그램 URL> [파일 또는 설명]`): SQL DDL이나 설명으로 다이어그램을 만듭니다.
- **스킬 `canvas-diagrams`**: 시퀀스 다이어그램, 플로우차트, UML 클래스 다이어그램, 도형에 어떤 도구를 쓰는지와 결과를 수정하는 방법. 자동으로 적용됩니다.
- **스킬 `diagram-from-description`** (`/erdcloud:diagram-from-description <다이어그램 URL> <sequence|flowchart|class> <설명 또는 경로>`): 설명이나 소스 코드로 시퀀스 다이어그램, 플로우차트, UML 클래스 다이어그램을 그립니다.

### 설치

1. Claude Code에서 플러그인을 설치합니다. Claude Code 2.1.275 이상에서는 명령 한 줄로 끝납니다.

   ```
   /plugin install erdcloud --marketplace erdcloud/erdcloud-claude-plugin
   ```

   또는 두 단계로 설치합니다(모든 버전).

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

2. Claude Code를 재시작하고 `/mcp`를 실행해 `erdcloud`를 선택한 뒤, 열리는 브라우저 창에서 ERDCloud에 로그인합니다. 권한 안내를 확인하고 **허용**을 누르면 끝입니다. 토큰을 복사할 필요가 없습니다.

   ERDCloud 계정이 아직 없다면 로그인 화면에서 **Google** 또는 **GitHub**를 선택하세요. 처음 로그인할 때 계정이 자동으로 만들어지고 권한 안내 화면으로 돌아옵니다. 이메일로 가입했다면 이메일 인증을 마친 뒤 Claude Code에서 `/mcp`를 다시 실행하세요.

3. 사용해 보세요.

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<다이어그램 id> 사용자, 주문, 상품이 있는 쇼핑몰
   ```

   같은 캔버스에 다른 다이어그램도 그릴 수 있습니다.

   ```
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<다이어그램 id> sequence 토큰 검증이 있는 로그인
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<다이어그램 id> flowchart 팀장과 재무 레인이 있는 주문 승인
   /erdcloud:diagram-from-description https://www.erdcloud.com/d/<다이어그램 id> class src/domain
   ```

### 권한과 보안

- Claude는 본인이 접근할 수 있는 ERD에만 접근합니다. 본인이 소유한 ERD와 수락된 팀 멤버인 팀의 ERD이며, 다른 사람의 공개 ERD는 읽기만 가능합니다. ERDCloud 관리자 계정이라도 이 연결로는 타인의 비공개/팀 ERD를 읽거나 수정할 수 없습니다.
- 액세스 토큰은 1시간짜리이며 자동 갱신됩니다. 연결은 최대 90일 후 만료되어 다시 로그인해야 합니다.
- ERDCloud에서 다이어그램을 열고 **AI(MCP)** 패널의 **연결된 앱**에서 언제든 연결을 확인하고 해제할 수 있으며, 해제는 즉시 적용됩니다.
- AI 편집은 실시간 반영되며 틀릴 수 있습니다. 큰 변경 전에는 ERDCloud에서 스냅샷을 만들거나 백업을 내보내세요.

### 문제 해결

- **401 / unauthorized / 인증 필요**: `/mcp`에서 `erdcloud`를 선택해 다시 로그인하세요(연결이 만료되었거나 해제된 경우입니다).
- **도구가 보이지 않음**: `/mcp`로 `erdcloud`가 연결되어 있는지 확인하세요.
- **OAuth를 지원하지 않는 도구/CI**: 이 플러그인 대신 액세스 토큰을 사용하세요. ERDCloud **AI(MCP)** 패널에서 토큰을 발급해 서버를 직접 추가합니다. 예: `claude mcp add --transport http erdcloud https://www.erdcloud.com/mcp --header "Authorization: Bearer <토큰>"`. 토큰은 커밋하지 마세요.

### 라이선스

[MIT](LICENSE). ERDCloud 서비스 자체에는 [서비스 약관](https://www.erdcloud.com/static/html/terms.html)과 [개인정보처리방침](https://www.erdcloud.com/static/html/privacy.html)이 적용됩니다.
