# 双击完成截图

2026-11-07；基线 8898a00；分支 fix/double-click-copy-anywhere。

## 目标与约定

已有选区时，在当前截图画布内双击即可走现有 copy 流程，包含选区外及标注模式。原始裁剪尺寸和标注必须保留。无选区不能复制。工具栏及原生文字编辑器保留自身事件（文字内双击仍选词）；多屏不新增跨画布行为。没有新权限、依赖、存储或发布。用户授权修改、提交和创建 PR，不合并或发布安装包。

已检查 CaptureCanvas.mouseDown：双击受 activeTool 和 contains 限制，外部单击立即 resetSelection。采用新增 reselect 手势：外部按下保留选区，拖动时才清空标注并重新框选，松开不改变原选区。右键重新选择行为不变。双击清理未完成手势并使用 perform(.copy)；渲染失败沿用 onFailure。

## 任务与验收

- T1（已完成，无依赖，就绪）：修改 CaptureCanvas、画布测试和中英文 README。先调整外部按下/拖动状态，再放宽双击条件；覆盖真实 down/up/down 双击序列、标注输出、无选区、外部拖动重选、文字提交。不得修改截图权限、签名、AppDelegate 输出或长截图架构。验收为相关测试通过、裁剪和标注保留。
- T2（待验证，依赖 T1）：仓库根目录执行 `scripts/run-tests.sh` 和 `scripts/build-simple.sh`，预期全部通过；核对 diff。另需真实鼠标、中文输入法、多屏手工验收，不能用合成事件替代。测试失败仅修复本次改动；若需改变事件分发或跨屏架构，先修订方案。
- T3（已完成，依赖 T2 自动检查）：提交至 CarvilleXXX fork，向 xiangyingchang/macshot-simple:main 创建 PR，写明行为、自动验证及未完成实测，检查远程分支同步。现有 origin 不更换，不合并。恢复方式为撤回独立分支修改，无数据迁移。

复核补充：画笔的第一次点击会产生一个点。保留单击画点能力，但记录该次无移动画笔点击前的历史，第二次点击确认为双击时恢复，避免完成截图时混入额外笔迹；普通新点击、工具操作和重选清除此临时状态。

## 验证记录

`scripts/run-tests.sh`：49 passed、0 failed、0 skipped（含 5 个新增回归测试）；`scripts/build-simple.sh`：Release 构建和临时签名验证通过；`git diff --check` 通过。初次测试受沙箱限制无法写入 Xcode 缓存，经授权执行后通过。最终修订后重复测试及构建均通过。真实鼠标、输入法和多屏待验证；T2 因此保留待验证状态，PR 明确列出手工检查项，不宣称发布验收完成。

PR 已创建：https://github.com/xiangyingchang/macshot-simple/pull/2 。代码提交 286352e，目标 main；后续等待维护者审阅并完成上述手工验证。
