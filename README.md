# podcast-workflow

从内容输入到 TTS 到 podcast feed 的工作流项目。

## 目标

逐步做成一条可复用流水线：

1. 输入内容（长文 / 链接 / PDF / 新闻）
2. 整理成适合口播的播客稿
3. 调用中文 TTS（当前优先豆包语音合成 2.0）
4. 输出音频文件
5. 生成 / 更新 RSS feed
6. 发布到 GitHub Pages 或后续更私有的托管

## 当前状态

- GitHub Pages feed 原型已存在于 `../private-podcast`
- 已验证豆包语音合成 2.0 的可用调用方式
- 凭证存储方案：macOS Keychain

## 后续建议目录

- `bin/`：CLI 脚本
- `docs/`：接口说明、工作流设计
- `episodes/`：生成的音频
- `feeds/`：RSS 模板 / 输出
- `tmp/`：中间文件

## 已验证双人案例

- 输入格式：`A|...` / `B|...`
- 当前成功配置：
  - A: `zh_female_mizai_uranus_bigtts`
  - B: `zh_male_dayi_uranus_bigtts`
  - volume: A=100, B=85
- 示例输入文件：`examples_dialogue.txt`
- 已生成样片：`episodes/dialogue-demo-dayi.mp3`

## 一键双人生成

```bash
./bin/doubao-dialogue --file examples_dialogue.txt -o episodes/dialogue-demo-cli.mp3
```

默认配置：
- A: `zh_female_mizai_uranus_bigtts`
- B: `zh_male_dayi_uranus_bigtts`
- volume: A=100, B=85

## 纯文本转双人对话稿

```bash
./bin/podcast-script --file article.txt -o dialogue.txt
```

输出格式为：

```text
A|...
B|...
A|...
B|...
```

说明：当前先做纯文本输入，不负责网页/PDF/搜索入口。该脚本现在默认走大模型改写，而不是规则拼句。该脚本现在默认走大模型改写，而不是规则拼句。


## `podcast-script` 模型调用

`podcast-script` 现在默认通过 `OPENAI_API_KEY` 调模型，把纯文本改写成双人对话稿。可选环境变量：

- `OPENAI_API_URL`
- `OPENAI_MODEL` 或 `PODCAST_SCRIPT_MODEL`
