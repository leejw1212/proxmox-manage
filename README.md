# proxmox-manage

Claude Code에서 Proxmox VE를 관리하기 위한 MCP 설정 레포입니다.

## MCP 서버

`.mcp.json`에 [`@bldg-7/proxmox-mcp`](https://www.npmjs.com/package/@bldg-7/proxmox-mcp)가 `proxmox`라는 이름으로 등록되어 있습니다.
토큰 등 비밀값은 커밋하지 않고 환경변수에서 읽습니다.

| 변수 | 필수 | 기본값 | 설명 |
|---|---|---|---|
| `PROXMOX_HOST` | 예 | - | Proxmox 호스트 (권장: `pve.autops.run`) |
| `PROXMOX_PORT` | 아니오 | `443` | API 포트 (Proxmox 에 직접 붙으면 `8006`) |
| `PROXMOX_USER` | 예 | - | 사용자@realm (예: `claude@pve`) |
| `PROXMOX_TOKEN_NAME` | 예 | - | API 토큰 ID (예: `mcp`) |
| `PROXMOX_TOKEN_VALUE` | 예 | - | API 토큰 시크릿 |
| `PROXMOX_SSL_MODE` | 아니오 | `strict` | `strict` / `verify` / `insecure` (8006 자체 서명 인증서로 직접 붙을 때만 `insecure`) |
| `PROXMOX_ALLOW_ELEVATED` | 아니오 | `false` | `true`면 VM 생성/수정/삭제 등 쓰기 작업 허용 |

## 확인

```bash
claude mcp list          # proxmox 서버가 Connected 인지 확인
```

## 접속 경로

`https://pve.autops.run` 은 dashboard-songhee 의 nginx 가 Let's Encrypt 인증서로 받아서
집 안 Proxmox(:8006)로 넘겨준다. Proxmox 기본 자체 서명 인증서는 클라우드 세션의
프록시를 통과하지 못하므로 이 경로를 쓴다.

Claude Code 클라우드 세션에서 쓸 때는 환경 설정 → Network access → Allowed domains 에
`pve.autops.run` 이 있어야 한다.
