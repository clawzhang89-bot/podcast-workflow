# 豆包语音合成 2.0 接入说明

## 已验证参数

- Endpoint: `https://openspeech.bytedance.com/api/v3/tts/unidirectional`
- Header:
  - `x-api-key: <API_KEY>`
  - `X-Api-Resource-Id: seed-tts-2.0`
  - `Content-Type: application/json`
- 返回为多段 JSON chunk，每段包含 base64 `data`
- 必须提取全部 chunk，逐段 decode 并按顺序拼接为完整 mp3

## Keychain

当前约定：

- service: `openclaw.volcengine.tts.apikey`
- account: `Evan`

读取示例：

```bash
security find-generic-password -s openclaw.volcengine.tts.apikey -a Evan -w
```
