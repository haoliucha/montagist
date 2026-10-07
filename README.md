奇镜是一个 AI 制作台，让一个人也能做出纪录片质感的解说视频：资料带出处，画面用真实镜头，每道关口由你拍板，素材和成片都留在你自己的 Mac 上。

# Montagist · 奇镜 Agent Skill

这份仓库提供给 Claude Code 和 Codex 使用的 Montagist Skill。制作台需要另行安装 [Montagist Mac 版](https://montagist.haoliucha.com/download)，打开并登录后，Skill 才能通过本机工具查看和推进你的一期。

安装 Skill：

```sh
npx skills add haoliucha/montagist -g -a claude-code codex -y
```

使用时，你对 AI 说想做什么、想检查哪一步。五道关口只有你亲口批准或退回，AI 才能带着你的原话执行；花钱、删除一期、导出发布材料会在 Mac 上再次问你；素材和成片保存在你的 Mac 上。

本仓库的 Skill 按 [MIT 许可证](LICENSE)开放，版权人为 Hidawn LLC。Montagist Mac App 与服务端不属于这份 MIT 授权，源代码未在此仓库开放。
