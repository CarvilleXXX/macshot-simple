# 项目进度

2026-11-07：双击完成截图贡献，详见 [EXECUTION_PLAN.md](EXECUTION_PLAN.md)。

- T1 已完成：支持选区内外及标注模式双击复制；保留外部拖动重选；避免画笔双击额外加点。
- T2 待验证：49 项自动测试通过；Release 构建及签名验证通过；diff 检查通过。真实鼠标、中文输入法、多屏尚未实测。
- T3 已完成：代码已提交并推送到 CarvilleXXX fork，已创建 [PR #2](https://github.com/xiangyingchang/macshot-simple/pull/2)；未合并或发布安装包。
- 接续入口：执行计划及 CaptureCanvas.swift；分支 fix/double-click-copy-anywhere。PR 审核时执行手工验收：框选后内外双击、六类标注后双击、画笔单击画点、外部拖动重选、中文输入和文字双击选词、多屏。
