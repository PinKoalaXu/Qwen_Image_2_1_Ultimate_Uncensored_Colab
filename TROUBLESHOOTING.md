# 依赖故障排查 / Dependency troubleshooting

## PEFT: incompatible torchao

如果 3B 加载 LoRA 时出现 `Found an incompatible version of torchao`（例如环境中为 `0.10.0`，PEFT 要求至少 `0.16.0`），在 Colab 新建代码单元运行：

```python
import subprocess, sys
subprocess.check_call([sys.executable, "-m", "pip", "uninstall", "-y", "torchao"])
```

然后选择 **运行时 → 重新启动会话**，再按 **1 → 2 → 3 → 3B** 重新运行。重启后模型需要重新加载，通常可复用当前运行时的下载缓存。不要选择删除运行时，除非你希望重新分配环境。

本笔记本的 BF16 流程没有使用可选的 `torchao` 量化功能。新版第 2 步会在安装依赖前移除它，避免预装旧包触发 PEFT 的版本检查。失败后的会话可能已缓存包可用性信息或导入旧模块，卸载后需重启。此错误不需要手动升级 PyTorch 或 CUDA。若其他任务需要 torchao，请为它们使用独立运行时并按其 PyTorch/CUDA 兼容矩阵配置。

已进行笔记本 JSON、6 个代码单元语法、安装顺序及失败传播的本地验证；未进行 Colab GPU 端到端验证。

If LoRA loading in 3B raises `Found an incompatible version of torchao` (such as installed `0.10.0` while PEFT requires at least `0.16.0`), run the code above in a new Colab cell. Then **restart the session** and rerun **1 → 2 → 3 → 3B**. Models must be loaded again; downloads can usually reuse the current runtime's cache.

This notebook's BF16 workflow does not use optional torchao quantization. Updated cell 2 removes it before dependency installation. Restart the failed session to clear cached availability information and imported modules. No manual PyTorch/CUDA upgrade is required for this error. Use a separate, version-compatible runtime for other workflows that need torchao.

Notebook JSON, six code cells' syntax, installation ordering and error propagation were checked locally. Colab GPU inference has not been tested end to end.
