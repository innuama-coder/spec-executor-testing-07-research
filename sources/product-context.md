# Product Context

spec-executor 是一个以 `spec.yaml` 为任务契约的本地执行器。它启动 Claude 或 Codex，在 tmux 会话中运行任务，并通过 OpenClaw 监控进度。2.2 的重点是把进度信息拆成 spec-executor、tmux、claude/codex 三类用户可理解信息。

