# podcast-workflow 使用说明

## 推荐入口

### 一键从纯文本生成双人播客音频

```bash
./bin/podcast-make --file article.txt -o episode.mp3
```

或者：

```bash
./bin/podcast-make --text '这里是一大段正文' -o episode.mp3
```

这条命令会自动执行：

1. `podcast-script`：纯文本 → 双人对话稿
2. `doubao-dialogue`：双人对话稿 → 双人 mp3

---

## 分步调用

### 1. 纯文本改写成双人对话稿

```bash
./bin/podcast-script --file article.txt -o dialogue.txt
```

### 2. 双人对话稿生成双人音频

```bash
./bin/doubao-dialogue --file dialogue.txt -o episode.mp3
```

### 3. 直接单段 TTS

```bash
./bin/doubao-tts '今天先聊三件事。' -s zh_female_mizai_uranus_bigtts -o out.mp3
```

---

## 当前验证成功的双人默认配置

- A: `zh_female_mizai_uranus_bigtts`
- B: `zh_male_dayi_uranus_bigtts`
- volume: A=100, B=85

---

## 凭证

当前豆包语音合成 API key 默认从 macOS Keychain 读取：

- service: `openclaw.volcengine.tts.apikey`
- account: `Evan`

手动检查：

```bash
security find-generic-password -s openclaw.volcengine.tts.apikey -a Evan -w
```


## `podcast-script` 常用参数

- `--turns`：目标轮数
- `--max-chars`：单句目标长度，便于 TTS 口播


## `podcast-script` 事实保真原则

- 忠于原文事实
- 不新增原文没有的信息
- 不改变判断方向、因果关系和语义强弱
- 只优化语气、衔接和文本编排


## 一键生成并发布到 GitHub Pages 播客 feed

```bash
./bin/podcast-publish \
  --file article.txt \
  --slug 2026-03-26-episode-001 \
  --title "案例 001：标题" \
  --summary "这一期的简短介绍"
```

这条命令会自动完成：

1. 纯文本 → 双人对话稿
2. 双人对话稿 → 双人 mp3
3. 复制音频到 `../private-podcast/episodes/`
4. 更新 `../private-podcast/feed.xml`
5. git commit + push 到 GitHub Pages 仓库
