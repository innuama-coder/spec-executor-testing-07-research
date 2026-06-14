# Technical Context

2.2 版本使用本地 JSONL 会话日志作为 Claude/Codex agent 进度来源。tmux 原生命令提供会话、窗口、pane、process 和 client 状态；capture-pane 只作为证据摘要，不作为 agent 主进度来源。

