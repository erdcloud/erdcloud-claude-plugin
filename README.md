# ERDCloud for Claude Code

[English](#english) | [한국어](#한국어)

## English

A [Claude Code](https://claude.com/claude-code) plugin marketplace for [ERDCloud](https://www.erdcloud.com), the web-based ERD (Entity Relationship Diagram) modeling service.

### Plugins

| Plugin | Description |
|---|---|
| `erdcloud` | Connects Claude Code to the ERDCloud MCP server so Claude can read and edit your diagrams (tables, columns, relations, domains, memos), and teaches Claude the right order of operations. |

What `erdcloud` contains:

- **MCP server** `erdcloud` -> `https://www.erdcloud.com/mcp`
- **Skill `erd-modeling`**: domain-first workflow, relationship workflow, and tool overview. Loaded automatically when you work on an ERD.
- **Skill `erd-from-sql`** (`/erdcloud:erd-from-sql <diagram URL> [file or description]`): build a diagram from SQL DDL or a description.

### Install

1. Start Claude Code and install the plugin:

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

2. Restart Claude Code, run `/mcp`, select `erdcloud` and sign in to ERDCloud in the browser window that opens. Review the permission screen and click **Allow**. No token to copy.

3. Try it:

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<your diagram id> an online shop with users, orders and products
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
| `erdcloud` | Claude Code를 ERDCloud MCP 서버에 연결해 다이어그램(테이블, 컬럼, 관계, 도메인, 메모)을 읽고 편집하게 하고, 올바른 작업 순서를 Claude에게 알려줍니다. |

포함 내용:

- **MCP 서버** `erdcloud` -> `https://www.erdcloud.com/mcp`
- **스킬 `erd-modeling`**: 도메인 우선 워크플로, 관계 생성 워크플로, 도구 목록. ERD 작업 시 자동으로 적용됩니다.
- **스킬 `erd-from-sql`** (`/erdcloud:erd-from-sql <다이어그램 URL> [파일 또는 설명]`): SQL DDL이나 설명으로 다이어그램을 만듭니다.

### 설치

1. Claude Code에서 플러그인을 설치합니다.

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

2. Claude Code를 재시작하고 `/mcp`를 실행해 `erdcloud`를 선택한 뒤, 열리는 브라우저 창에서 ERDCloud에 로그인합니다. 권한 안내를 확인하고 **허용**을 누르면 끝입니다. 토큰을 복사할 필요가 없습니다.

3. 사용해 보세요.

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<다이어그램 id> 사용자, 주문, 상품이 있는 쇼핑몰
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
