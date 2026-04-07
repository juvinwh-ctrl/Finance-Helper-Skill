[SKILL.md](https://github.com/user-attachments/files/26530860/SKILL.md)
---
name: finance-doc-processor
description: 财务文档处理助手，用于执行自定义的财务文档处理任务。
metadata: { "openclaw": { "emoji": "💰" } }
user-invocable: true
command-dispatch: tool
command-tool: exec
command-arg-mode: raw
---

# 财务文档处理助手 (Finance Document Processor)

这是一个专门为财务人员设计的文档处理技能。它通过调用一个 Python 脚本来执行预装的自定义二进制命令，从而实现高效的文档自动化处理。

## 功能描述

当用户需要处理财务文档时，例如发票、报表或凭证，可以调用此技能。技能会接收用户提供的参数，并将其传递给内部的 Python 脚本。该脚本随后会执行一个您预先安装在系统中的自定义二进制命令（例如 `finance-tool`），并将处理结果返回。

## 使用方式

您可以通过以下方式调用此技能：

*   **通过自然语言**：例如，“帮我处理一下这个月的发票文档 /path/to/invoices.pdf”

## 内部执行流程

1.  OpenClaw 接收到用户指令或 Slash 命令。
2.  根据 `command-dispatch: tool` 和 `command-tool: exec` 配置，OpenClaw 会调用 `exec` 工具。
3.  `exec` 工具会执行以下命令，将用户提供的所有参数作为原始字符串传递给 `handler.py` 脚本：
    ```bash
    python3 {baseDir}/handler.py "$@"
    ```
4.  `handler.py` 脚本会解析这些参数，并调用您指定的自定义二进制命令（例如 `finance-tool`）。

## 注意事项

*   请确保 `handler.py` 脚本位于技能文件夹的根目录。
*   您需要将实际的二进制命令（例如 `finance-tool`）安装在系统 PATH 中，或者在 `handler.py` 脚本中指定其完整路径。
*   `handler.py` 脚本需要具有执行权限（`chmod +x handler.py`）。
---
