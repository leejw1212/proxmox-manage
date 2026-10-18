# proxmox-manage

Claude Code에서 Proxmox VE를 관리하기 위한 MCP 설정 레포입니다.

## MCP 서버

`.mcp.json`에 [`@bldg-7/proxmox-mcp`](https://www.npmjs.com/package/@bldg-7/proxmox-mcp)가 `proxmox`라는 이름으로 등록되어 있습니다.
토큰 등 비밀값은 커밋하지 않고 환경변수에서 읽습니다.

| 변수 | 필수 | 기본값 | 설명 |
|---|---|---|---|
| `PROXMOX_HOST` | 예 | - | Proxmox 호스트 (예: `petple.ddns.net`) |
| `PROXMOX_PORT` | 아니오 | `8006` | API 포트 |
| `PROXMOX_USER` | 예 | - | 사용자@realm (예: `claude@pve`) |
| `PROXMOX_TOKEN_NAME` | 예 | - | API 토큰 ID (예: `mcp`) |
| `PROXMOX_TOKEN_VALUE` | 예 | - | API 토큰 시크릿 |
| `PROXMOX_SSL_MODE` | 아니오 | `insecure` | `strict` / `verify` / `insecure` (자체 서명 인증서면 `insecure` 또는 `verify` + `PROXMOX_SSL_CA_CERT`) |
| `PROXMOX_ALLOW_ELEVATED` | 아니오 | `false` | `true`면 VM 생성/수정/삭제 등 쓰기 작업 허용 |

## 확인

```bash
claude mcp list          # proxmox 서버가 Connected 인지 확인
```

Claude Code 클라우드 세션에서 사용할 경우 환경 설정의 Network access 에서
`PROXMOX_HOST`(포트 8006) 접근이 허용되어 있어야 합니다.
