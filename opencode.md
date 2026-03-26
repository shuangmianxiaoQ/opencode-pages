
# OpenCode 指令速查表

新人第一天注册linux do社区,第一次发帖,如果帮助到您帮忙点点赞,谢谢啦 :grinning_face:

---

> 最后更新：2026-03-10 | 官方文档：https://opencode.ai/docs

---

##  安装

| 方式 | 命令 |
|------|------|
| 官方脚本（推荐） | `curl -fsSL https://opencode.ai/install \| bash` |
| npm | `npm install -g opencode-ai` |
| bun | `bun install -g opencode-ai` |
| pnpm | `pnpm install -g opencode-ai` |
| yarn | `yarn global add opencode-ai` |
| Homebrew (macOS/Linux) | `brew install anomalyco/tap/opencode` |
| Arch Linux（稳定版） | `sudo pacman -S opencode` |
| Arch Linux（AUR最新版） | `paru -S opencode-bin` |
| Chocolatey (Windows) | `choco install opencode` |
| Scoop (Windows) | `scoop install opencode` |
| Mise | `mise use -g github:anomalyco/opencode` |
| Docker | `docker run -it --rm ghcr.io/anomalyco/opencode` |

---

##  基本启动

```bash
opencode                        # 启动 TUI（当前目录）
opencode /path/to/project       # 启动 TUI（指定目录）
opencode -c                     # 继续上次会话
opencode -s <sessionID>         # 继续指定会话
opencode -m anthropic/claude-sonnet-4-5  # 指定模型启动
```

---

##  CLI 命令一览

### `opencode run` — 非交互模式

```bash
opencode run "你的问题"
opencode run -c "继续上次会话"
opencode run -s <sessionID> "继续指定会话"
opencode run -m anthropic/claude-opus-4-5 "使用指定模型"
opencode run -f file.txt "附加文件"
opencode run --share "运行并分享会话"
opencode run --attach http://localhost:4096 "连接到已运行的服务端"
opencode run --format json "输出原始 JSON 事件"
```

### `opencode serve` — 启动无头服务器

```bash
opencode serve                          # 启动 API 服务器
opencode serve --port 4096              # 指定端口
opencode serve --hostname 0.0.0.0      # 指定主机名
opencode serve --mdns                   # 启用 mDNS 发现
```

### `opencode web` — 启动 Web 界面

```bash
opencode web                            # 启动 Web 服务器
opencode web --port 4096
opencode web --hostname 0.0.0.0
```

### `opencode attach` — 附加到已运行服务器

```bash
opencode attach http://10.20.30.40:4096
opencode attach http://localhost:4096 --session <id>
```

---

##  Auth 认证管理

```bash
opencode auth login         # 配置 API Key（存于 ~/.local/share/opencode/auth.json）
opencode auth list          # 列出已配置的 Provider
opencode auth ls            # 同上（简写）
opencode auth logout        # 登出某个 Provider
```

---

##  Agent 管理

```bash
opencode agent list         # 列出所有可用 Agent
opencode agent create       # 创建新 Agent（向导式）
```

---

##  Session 会话管理

```bash
opencode session list                   # 列出所有会话
opencode session list -n 10             # 列出最近 10 条
opencode session list --format json     # JSON 格式输出
opencode export [sessionID]             # 导出会话为 JSON
opencode import session.json            # 从文件导入会话
opencode import https://opncd.ai/s/abc  # 从分享链接导入
```

---

##  Model 模型管理

```bash
opencode models                         # 列出所有可用模型
opencode models anthropic               # 按 Provider 筛选
opencode models --refresh               # 刷新模型缓存
opencode models --verbose               # 显示模型元数据（含费用）
```

---

##  Stats 统计

```bash
opencode stats                          # 显示 token 用量和费用
opencode stats --days 7                 # 最近 7 天
opencode stats --tools 10               # 显示前 10 个工具
opencode stats --models 5               # 显示前 5 个模型使用情况
opencode stats --project ./             # 按项目筛选
```

---

##  MCP 服务器管理

```bash
opencode mcp add            # 添加 MCP 服务器（向导式）
opencode mcp list           # 列出所有 MCP 服务器及连接状态
opencode mcp ls             # 同上（简写）
opencode mcp auth [name]    # 为 OAuth MCP 服务器认证
opencode mcp auth list      # 列出支持 OAuth 的服务器
opencode mcp logout [name]  # 移除 OAuth 凭证
opencode mcp debug <n>      # 调试 OAuth 连接问题
```

---

##  GitHub 集成

```bash
opencode github install     # 在仓库中安装 GitHub Agent
opencode github run         # 运行 GitHub Agent（通常在 Actions 中使用）
opencode github run --event <event> --token <token>
```

---

##  升级与卸载

```bash
opencode upgrade                        # 升级到最新版本
opencode upgrade v0.1.48               # 升级到指定版本
opencode upgrade -m npm                # 指定安装方式（curl/npm/pnpm/bun/brew）

opencode uninstall                      # 卸载 OpenCode
opencode uninstall --keep-config        # 保留配置文件
opencode uninstall --keep-data          # 保留会话数据
opencode uninstall --dry-run           # 预览将删除的内容
opencode uninstall -f                   # 跳过确认直接卸载
```

---

##  Global Flags 全局参数

| 参数 | 简写 | 说明 |
|------|------|------|
| `--help` | `-h` | 显示帮助 |
| `--version` | `-v` | 打印版本号 |
| `--print-logs` | | 将日志输出到 stderr |
| `--log-level` | | 日志等级（DEBUG/INFO/WARN/ERROR） |

---

##  TUI 内部指令（`/` 命令）

在 TUI 输入框中输入 `/` 前缀执行：

| 指令 | 别名 | 快捷键 | 说明 |
|------|------|--------|------|
| `/connect` | | | 添加 Provider / API Key |
| `/compact` | `/summarize` | `ctrl+x c` | 压缩当前会话上下文 |
| `/details` | | `ctrl+x d` | 切换工具执行详情显示 |
| `/editor` | | `ctrl+x e` | 用外部编辑器撰写消息 |
| `/exit` | `/quit` `/q` | `ctrl+x q` | 退出 OpenCode |
| `/export` | | `ctrl+x x` | 导出对话为 Markdown |
| `/help` | | `ctrl+x h` | 显示帮助对话框 |
| `/init` | | `ctrl+x i` | 创建/更新 `AGENTS.md` |
| `/models` | | `ctrl+x m` | 列出可用模型 |
| `/new` | `/clear` | `ctrl+x n` | 开启新会话 |
| `/redo` | | `ctrl+x r` | 重做已撤销的消息 |
| `/sessions` | `/resume` `/continue` | `ctrl+x l` | 查看并切换会话 |
| `/share` | | `ctrl+x s` | 分享当前会话 |
| `/themes` | | `ctrl+x t` | 列出可用主题 |
| `/thinking` | | | 切换思维链显示 |
| `/undo` | | `ctrl+x u` | 撤销上一条消息及文件改动 |
| `/unshare` | | | 取消分享当前会话 |

---

## ⌨️ TUI 快捷键速查

### Leader 键（默认 `ctrl+x`）

> 大多数操作需先按 Leader 键，再按对应字母。

| 快捷键 | 功能 |
|--------|------|
| `ctrl+x h` | 帮助 / 命令列表 |
| `ctrl+x n` | 新建会话 |
| `ctrl+x l` | 会话列表 |
| `ctrl+x m` | 模型选择 |
| `ctrl+x a` | Agent 选择 |
| `ctrl+x c` | 压缩上下文 |
| `ctrl+x s` | 状态视图 / 分享会话 |
| `ctrl+x u` | 撤销 |
| `ctrl+x r` | 重做 |
| `ctrl+x e` | 打开外部编辑器 |
| `ctrl+x x` | 导出对话 |
| `ctrl+x t` | 主题列表 |
| `ctrl+x b` | 切换侧边栏 |
| `ctrl+x d` | 切换工具详情 |
| `ctrl+x q` | 退出 |
| `ctrl+x y` | 复制消息 |
| `ctrl+x g` | 会话时间线 |
| `ctrl+x i` | 初始化 AGENTS.md |

### 消息导航

| 快捷键 | 功能 |
|--------|------|
| `pageup` / `ctrl+alt+b` | 向上翻页 |
| `pagedown` / `ctrl+alt+f` | 向下翻页 |
| `ctrl+alt+y` | 向上滚动一行 |
| `ctrl+alt+e` | 向下滚动一行 |
| `ctrl+alt+u` | 向上滚动半页 |
| `ctrl+alt+d` | 向下滚动半页 |
| `ctrl+g` / `home` | 跳到顶部 |
| `ctrl+alt+g` / `end` | 跳到底部 |

### 输入框操作

| 快捷键 | 功能 |
|--------|------|
| `return` | 发送消息 |
| `shift+return` / `ctrl+j` | 输入换行 |
| `ctrl+a` | 移到行首 |
| `ctrl+e` | 移到行尾 |
| `ctrl+k` | 删除到行尾 |
| `ctrl+u` | 删除到行首 |
| `ctrl+w` / `ctrl+backspace` | 删除前一个单词 |
| `alt+d` | 删除后一个单词 |
| `alt+f` / `ctrl+right` | 前进一个单词 |
| `alt+b` / `ctrl+left` | 后退一个单词 |
| `ctrl+c` | 清空输入 / 中断响应 |
| `ctrl+v` | 粘贴 |
| `ctrl+-` / `super+z` | 输入框撤销 |
| `ctrl+.` / `super+shift+z` | 输入框重做 |

### 模型与 Agent

| 快捷键 | 功能 |
|--------|------|
| `tab` | 切换 Agent（Build ↔ Plan） |
| `shift+tab` | 反向切换 Agent |
| `f2` | 循环切换最近使用的模型 |
| `shift+f2` | 反向循环切换模型 |
| `ctrl+t` | 循环切换模型变体（含推理模式） |
| `ctrl+p` | 打开命令面板 |
| `escape` | 中断当前响应 |

---

##  TUI 特殊输入语法

| 语法 | 说明 |
|------|------|
| `@filename` | 引用文件（模糊搜索项目内文件，内容自动加入上下文） |
| `!ls -la` | 执行 shell 命令，输出作为工具结果加入上下文 |

---

##  配置文件

### 文件位置与优先级（低 → 高）

| 优先级 | 位置 | 说明 |
|--------|------|------|
| 1 | `.well-known/opencode`（远程） | 组织级默认配置 |
| 2 | `~/.config/opencode/opencode.json` | 全局用户配置 |
| 3 | `OPENCODE_CONFIG` 指向的文件 | 自定义路径配置 |
| 4 | 项目根目录 `opencode.json` | 项目级配置（最高优先级） |
| 5 | `.opencode/` 目录 | agents/commands/plugins 等 |
| 6 | `OPENCODE_CONFIG_CONTENT` 环境变量 | 运行时内联配置 |

> 所有配置文件**合并**生效，后者覆盖前者的冲突键，非冲突键全部保留。

### 目录结构

```
~/.config/opencode/
├── opencode.json       # 全局运行时配置
├── tui.json            # 全局 TUI 配置
├── auth.json           # API Key 存储（自动管理）
├── agents/             # 自定义 Agent 定义
├── commands/           # 自定义 slash 命令
├── plugins/            # 自定义插件
├── skills/             # Agent 技能
├── tools/              # 自定义工具
└── themes/             # 自定义主题

项目根目录/
├── opencode.json       # 项目级配置
├── tui.json            # 项目级 TUI 配置
├── AGENTS.md           # Agent 规则文件（建议提交到 Git）
└── .opencode/
    ├── agents/
    ├── commands/
    └── plugins/
```

### 常用配置片段

```jsonc
// opencode.json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-5",
  "small_model": "anthropic/claude-haiku-4-5",
  "default_agent": "build",        // 默认 Agent：build 或 plan
  "autoupdate": true,              // 自动更新（"notify" 仅提醒，false 禁用）
  "share": "manual",               // manual | auto | disabled

  // 服务器配置
  "server": {
    "port": 4096,
    "hostname": "0.0.0.0",
    "mdns": true
  },

  // 权限配置
  "permission": {
    "edit": "ask",
    "bash": "ask"
  },

  // 禁用/启用 Provider
  "disabled_providers": ["openai"],
  "enabled_providers": ["anthropic"],

  // 上下文压缩
  "compaction": {
    "auto": true,
    "prune": true,
    "reserved": 10000
  },

  // 关闭某些工具
  "tools": {
    "write": false,
    "bash": false
  },

  // 加载说明文件（支持 glob）
  "instructions": ["CONTRIBUTING.md", "docs/guidelines.md"]
}
```

```jsonc
// tui.json
{
  "$schema": "https://opencode.ai/tui.json",
  "theme": "opencode",
  "scroll_speed": 3,
  "scroll_acceleration": { "enabled": true },
  "diff_style": "auto",            // auto | stacked
  "keybinds": {
    "leader": "ctrl+x"
  }
}
```

### 配置变量替换

```jsonc
{
  // 引用环境变量
  "model": "{env:OPENCODE_MODEL}",
  "provider": {
    "anthropic": {
      "options": { "apiKey": "{env:ANTHROPIC_API_KEY}" }
    }
  },
  // 引用文件内容
  "provider": {
    "openai": {
      "options": { "apiKey": "{file:~/.secrets/openai-key}" }
    }
  }
}
```

---

##  环境变量

| 变量 | 类型 | 说明 |
|------|------|------|
| `OPENCODE_AUTO_SHARE` | bool | 自动分享会话 |
| `OPENCODE_CONFIG` | string | 自定义配置文件路径 |
| `OPENCODE_CONFIG_DIR` | string | 自定义配置目录路径 |
| `OPENCODE_CONFIG_CONTENT` | string | 内联 JSON 配置内容 |
| `OPENCODE_TUI_CONFIG` | string | 自定义 TUI 配置路径 |
| `OPENCODE_PERMISSION` | string | 内联权限配置 JSON |
| `OPENCODE_SERVER_PASSWORD` | string | 启用 HTTP Basic Auth |
| `OPENCODE_SERVER_USERNAME` | string | 覆盖 Basic Auth 用户名（默认 `opencode`） |
| `OPENCODE_DISABLE_AUTOUPDATE` | bool | 禁用自动更新检查 |
| `OPENCODE_DISABLE_AUTOCOMPACT` | bool | 禁用自动上下文压缩 |
| `OPENCODE_DISABLE_PRUNE` | bool | 禁用旧数据清理 |
| `OPENCODE_DISABLE_TERMINAL_TITLE` | bool | 禁用终端标题自动更新 |
| `OPENCODE_DISABLE_LSP_DOWNLOAD` | bool | 禁用 LSP 服务器自动下载 |
| `OPENCODE_DISABLE_MODELS_FETCH` | bool | 禁用从远程获取模型列表 |
| `OPENCODE_DISABLE_DEFAULT_PLUGINS` | bool | 禁用默认插件 |
| `OPENCODE_DISABLE_CLAUDE_CODE` | bool | 禁用读取 `.claude` 目录 |
| `OPENCODE_ENABLE_EXA` | bool | 启用 Exa 网络搜索工具 |
| `OPENCODE_ENABLE_EXPERIMENTAL_MODELS` | bool | 启用实验性模型 |
| `OPENCODE_GIT_BASH_PATH` | string | Windows 上 Git Bash 路径 |
| `OPENCODE_MODELS_URL` | string | 自定义模型配置来源 URL |
| `OPENCODE_CLIENT` | string | 客户端标识（默认 `cli`） |

### 实验性环境变量

| 变量 | 说明 |
|------|------|
| `OPENCODE_EXPERIMENTAL` | 启用所有实验性功能 |
| `OPENCODE_EXPERIMENTAL_PLAN_MODE` | 启用 Plan 模式 |
| `OPENCODE_EXPERIMENTAL_LSP_TOOL` | 启用实验性 LSP 工具 |
| `OPENCODE_EXPERIMENTAL_LSP_TY` | 启用实验性 LSP 类型检查 |
| `OPENCODE_EXPERIMENTAL_BASH_DEFAULT_TIMEOUT_MS` | Bash 命令默认超时（毫秒） |
| `OPENCODE_EXPERIMENTAL_OUTPUT_TOKEN_MAX` | LLM 响应最大 output token 数 |
| `OPENCODE_EXPERIMENTAL_FILEWATCHER` | 启用全目录文件监听 |
| `OPENCODE_EXPERIMENTAL_DISABLE_FILEWATCHER` | 禁用文件监听 |
| `OPENCODE_EXPERIMENTAL_MARKDOWN` | 启用实验性 Markdown 渲染 |
| `OPENCODE_EXPERIMENTAL_OXFMT` | 启用 oxfmt 格式化器 |
| `OPENCODE_EXPERIMENTAL_ICON_DISCOVERY` | 启用图标发现 |
| `OPENCODE_EXPERIMENTAL_DISABLE_COPY_ON_SELECT` | 禁用选中自动复制 |

---

##  实用工作流示例

### 启动无头服务器 + 本地 TUI 连接

```bash
# 终端 1：启动服务器（供 Web/移动端访问）
opencode web --port 4096 --hostname 0.0.0.0

# 终端 2：附加 TUI 到远程服务器
opencode attach http://10.20.30.40:4096
```

### 批量执行任务（脚本化，复用服务端避免 MCP 冷启动）

```bash
opencode serve &
opencode run --attach http://localhost:4096 "帮我写单元测试"
opencode run --attach http://localhost:4096 "检查代码风格"
```

### 分享会话

```bash
opencode run --share "解释这段代码"  # 运行后自动分享
# TUI 中：/share → 链接自动复制到剪贴板
# 取消分享：/unshare
```

---

##  常用场景速查

| 目标 | 方式 |
|------|------|
| 项目初始化 | TUI 中输入 `/init` |
| 撤销 AI 改动（需 Git） | `/undo` 或 `ctrl+x u` |
| 重做 | `/redo` 或 `ctrl+x r` |
| 切换 Plan/Build 模式 | `Tab` 键 |
| 引用文件加入上下文 | `@文件名`（模糊搜索） |
| 执行 shell 命令 | `!命令` |
| 压缩上下文节省 token | `/compact` 或 `ctrl+x c` |
| 查看帮助 | `/help` 或 `ctrl+x h` |
| 切换模型 | `/models` 或 `ctrl+x m` |
| 多行输入 | `shift+return` 或 `ctrl+j` |
| 中断 AI 响应 | `escape` |

---
