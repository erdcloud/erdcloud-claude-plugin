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

1. Generate an access token in ERDCloud: open a diagram and use the **AI (MCP)** panel. The token is shown only once. It expires after at most 90 days.
2. Make the token available to Claude Code as an environment variable, for example in your shell profile:

   ```bash
   export ERDCLOUD_MCP_TOKEN=erdmcp_xxxxxxxx
   ```

3. Start Claude Code and install the plugin:

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

4. Restart Claude Code (so it picks up the token and the MCP server), then try:

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<your diagram id> an online shop with users, orders and products
   ```

### Security notes

- The token grants access to the diagrams of the account that generated it. Treat it like a password and never commit it. This plugin only references it through the `ERDCLOUD_MCP_TOKEN` environment variable.
- Regenerating the token in ERDCloud immediately invalidates the previous one.
- AI edits are applied live and can be wrong. Create a Snapshot or export a backup in ERDCloud before large changes.

### Troubleshooting

- **401 / unauthorized**: the token is missing, expired or regenerated. Generate a new one, update `ERDCLOUD_MCP_TOKEN`, and restart Claude Code.
- **Tools not listed**: run `/mcp` in Claude Code and check that `erdcloud` is connected.

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

1. ERDCloud에서 액세스 토큰을 발급합니다. 다이어그램을 열고 **AI(MCP)** 패널을 사용하세요. 토큰은 발급 시 한 번만 표시되며 최대 90일 후 만료됩니다.
2. 토큰을 환경변수로 설정합니다(예: 셸 프로필).

   ```bash
   export ERDCLOUD_MCP_TOKEN=erdmcp_xxxxxxxx
   ```

3. Claude Code에서 플러그인을 설치합니다.

   ```
   /plugin marketplace add erdcloud/erdcloud-claude-plugin
   /plugin install erdcloud@erdcloud
   ```

4. Claude Code를 재시작한 뒤 사용해 보세요.

   ```
   /erdcloud:erd-from-sql https://www.erdcloud.com/d/<다이어그램 id> 사용자, 주문, 상품이 있는 쇼핑몰
   ```

### 보안 안내

- 토큰은 발급한 계정의 다이어그램에 접근할 수 있으므로 비밀번호처럼 다루고 절대 커밋하지 마세요. 이 플러그인은 `ERDCLOUD_MCP_TOKEN` 환경변수로만 토큰을 참조합니다.
- ERDCloud에서 토큰을 재발급하면 이전 토큰은 즉시 무효화됩니다.
- AI 편집은 실시간 반영되며 틀릴 수 있습니다. 큰 변경 전에는 ERDCloud에서 스냅샷을 만들거나 백업을 내보내세요.

### 문제 해결

- **401 / unauthorized**: 토큰이 없거나 만료·재발급된 경우입니다. 새로 발급해 `ERDCLOUD_MCP_TOKEN`을 갱신하고 Claude Code를 재시작하세요.
- **도구가 보이지 않음**: Claude Code에서 `/mcp`로 `erdcloud`가 연결되어 있는지 확인하세요.

### 라이선스

[MIT](LICENSE). ERDCloud 서비스 자체에는 [서비스 약관](https://www.erdcloud.com/static/html/terms.html)과 [개인정보처리방침](https://www.erdcloud.com/static/html/privacy.html)이 적용됩니다.
