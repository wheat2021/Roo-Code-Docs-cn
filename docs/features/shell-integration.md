# 终端 Shell 集成

终端 Shell 集成是一项关键功能，它使 Roo Code 能够在您的终端中执行命令并智能地处理其输出。AI 与您的开发环境之间的这种双向通信开启了强大的自动化功能。

---

## 什么是 Shell 集成？

Shell 集成在 Roo Code 中自动启用，并直接连接到您终端的命令执行生命周期，无需您进行任何设置。此内置功能允许 Roo：

- 通过 [`execute_command`](/advanced-usage/available-tools/execute-command) 工具代表您执行命令
- 实时读取命令输出，无需手动复制粘贴
- 自动检测并修复正在运行的应用程序中的错误
- 观察命令退出代码以确定成功或失败
- 在您浏览项目时跟踪工作目录的更改
- 无需用户干预即可智能地对终端输出做出反应
- 使用命令执行消息旁边出现的停止按钮，直接从聊天界面停止正在运行的命令。

<img src="/img/v3.15/v3.15.png" alt="聊天界面中的停止命令按钮" width="600" />

当您要求 Roo 执行安装依赖项、启动开发服务器或分析构建错误等任务时，Shell 集成会在幕后工作，使这些交互顺畅有效。

---

## Shell 集成故障排除

Shell 集成内置于 Roo Code 中，在大多数情况下可自动工作。如果您看到“Shell 集成不可用”消息或在命令执行时遇到问题，请尝试以下解决方案：

1.  **更新 VSCode/Cursor** 至最新版本（需要 VSCode 1.93+）
2.  **确保选择了兼容的 shell**：命令面板（`Ctrl+Shift+P` 或 `Cmd+Shift+P`）→“终端：选择默认配置文件”→ 选择 bash、zsh、PowerShell 或 fish
3.  **Windows PowerShell 用户**：运行 `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` 然后重新启动 VSCode
4.  **WSL 用户**：将 `. "$(code --locate-shell-integration-path bash)"` 添加到您的 `~/.bashrc`

---

## 命令执行回退

Roo Code 具有执行命令的回退机制。如果您选择使用 VS Code 的终端集成（通过取消选中 [`禁用终端 shell 集成`](#disable-terminal-shell-integration) 设置）并且该集成失败，则此功能最为相关。

- **工作原理**：如果 Roo Code 配置为使用 VS Code 的终端集成但无法连接或遇到问题，它可能会自动尝试直接使用后台进程执行命令。这是一种回退机制，以确保命令仍然会尝试运行。
- **通知**：如果使用此回退，您可能会在聊天中看到一条通知，指示该命令正在运行，但没有 Roo 的内联终端或 VS Code 的 shell 集成的全部功能（例如，实时输出流或精确的退出代码检测可能会受到限制）。
<img src="/img/v3.15.0/v3.15.0.png" alt="命令执行回退通知示例" width="600" />

- **解决方法**：如果您遇到此回退，通常表示您的 VS Code shell 集成设置存在问题。请查看本文档中的故障排除步骤，或考虑通过确保选中 [`禁用终端 shell 集成`](#disable-terminal-shell-integration) 设置来使用 Roo Code 推荐的内联终端。

<img src="/img/shell-integration/shell-integration-12.png" alt="Roo Code 推荐的内联终端正在运行" width="600" />
*Roo Code 推荐的内联终端示例。*


---

## 终端集成设置

Roo Code 提供了一些设置来微调它与终端的交互方式。要访问这些设置：
1.  单击 Roo Code 侧边栏右上角的 <Codicon name="gear" /> 图标。
2.  在打开的设置窗格中，从左侧菜单中选择“终端”组。

### 基本设置

#### 终端输出限制
<img src="/img/shell-integration/shell-integration.png" alt="终端输出限制滑块设置为 500" width="600" />
此设置控制 Roo Code 从您的命令中捕获多少输出。如果您担心令牌使用量，或者如果 Roo 处理非常长的输出时似乎很慢（您仍然会得到开头和结尾），请考虑降低它。如果您经常需要直接在 Roo 的上下文中获取长命令的更多中间内容，请考虑增加它，但要注意潜在的令牌成本。默认值：500 行。

#### 压缩进度条输出
<img src="/img/shell-integration/shell-integration-10.png" alt="压缩进度条输出复选框" width="600" />
保持启用此项（默认）以获得更清晰的输出并节省令牌。它使 Roo Code 处理动态输出（如进度条或旋转器）更像一个真实的终端，只显示最终状态。仅在极少数情况下禁用此项，即您特别需要调试进度条或类似动态显示的中间原始输出时。

### 高级设置

:::info 重要提示
**这些设置需要重新启动终端**

对高级终端设置的更改只有在重新启动终端后才会生效。要重新启动终端：

1.  单击终端面板中的垃圾桶图标以关闭当前终端
2.  使用“终端”→“新建终端”或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（反引号）打开一个新终端

更改任何这些设置后，请务必重新启动所有打开的终端。
:::

#### 继承环境变量
<img src="/img/shell-integration/shell-integration-11.png" alt="继承环境变量复选框" width="600" />
此设置控制 Roo Code 的终端会话是否使用与您的主 VSCode/Cursor 环境相同的环境变量（如 `PATH`、API 密钥等）。它直接镜像 VSCode 全局设置 [`terminal.integrated.inheritEnv`](https://code.visualstudio.com/docs/editor/integrated-terminal#_inherit-environment-variables)。如果您希望 Roo 命令在与常规 VSCode 终端中可用的相同上下文和工具下运行，请保持启用此项（VSCode 的默认设置）。仅当您需要一个完全干净、隔离的环境来执行 Roo 的终端任务或正在排查复杂的环境变量冲突时，才考虑禁用它。

### 运行时环境
在 macOS（以及可能的其他操作系统）上，提供给 VSCode 并因此提供给 Roo Code 的环境可能会因 VSCode 的启动方式而异。
如果从命令行 `vscode` 命令启动，VSCode 和 Roo Code 将继承启动它的 shell 的环境，并且一切（通常）都会正常。
如果从访达、程序坞或聚焦搜索启动，从 `.zshrc` 或 `.zprofile` 导出的环境可能会丢失。如果您在其中一个文件中设置了环境变量，并且在运行 VSCode 时发现它们丢失了，请将它们移动到 .zshenv，然后注销并重新登录，以便窗口管理器获取新的环境设置。

#### 禁用终端 shell 集成
<img src="/img/shell-integration/shell-integration-9.png" alt="禁用终端 shell 集成复选框" width="600" />
此设置决定了 Roo Code 如何执行终端命令。
-   **保持此复选框为选中状态（推荐）：** Roo Code 将使用其内置的内联终端执行命令，直接在聊天界面中显示输出。此方法通常很健壮，提供清晰的输出，是大多数用户通过 Roo Code 与终端命令交互的首选方式。它确保命令在由 Roo Code 管理的一致环境中运行。

    <img src="/img/shell-integration/shell-integration-12.png" alt="选中“禁用终端 shell 集成”时 Roo Code 的内联终端" width="600" />
    *当“禁用终端 shell 集成”被选中时，Roo Code 的内联终端处于活动状态。*

-   **取消选中此复选框（以使用 VS Code 的终端集成）：** Roo Code 将尝试直接在您活动的 VS Code 终端面板中运行命令。在您明确需要命令在您完全自定义的 VS Code shell 环境中运行或需要与 VS Code 终端的特定功能进行交互的特定边缘情况下，此替代方法可能很有用。但是，根据您的 shell 设置和 VS Code 版本，这有时可能不太可靠。

以下设置是高级选项，**仅当您取消选中“禁用终端 shell 集成”**（选择使用 VS Code 的终端集成而不是 Roo Code 推荐的内联终端）时才适用：

##### 终端 shell 集成超时
<img src="/img/shell-integration/shell-integration-1.png" alt="终端 shell 集成超时滑块设置为 15 秒" width="600" />
如果启用了 shell 集成但您仍然看到“Shell 集成不可用”，尤其是在复杂的 shell 设置（例如，带有许多插件的 Zsh 或加载缓慢的公司环境）下，您的 shell 可能需要太长时间来初始化。增加此值可为您的 shell 提供更多时间向 Roo Code 发出准备就绪的信号。尝试以 5-10 秒为增量。默认值：15 秒（如 UI 中所示）。

##### 终端命令延迟
<img src="/img/shell-integration/shell-integration-2.png" alt="终端命令延迟滑块设置为 0 毫秒" width="600" />
如果命令输出看起来不完整或 Roo 似乎错过了命令输出的结尾（即使启用了 shell 集成），小小的延迟可能会有所帮助。引入一个小的延迟（例如，50 毫秒或 100 毫秒）。这给了终端更多的时间来刷新所有输出，然后 Roo Code 才认为命令已完成。这是针对 VSCode 终端或某些 shell 中潜在时序问题的解决方法（请参阅 VSCode 错误 [#237208](https://github.com/microsoft/vscode/issues/237208)）。默认值：0 毫秒。

##### 启用 PowerShell 计数器解决方法
<img src="/img/shell-integration/shell-integration-3.png" alt="启用 PowerShell 计数器解决方法复选框" width="600" />
特定于 PowerShell 用户。如果您发现 Roo Code 难以*连续多次运行完全相同的 PowerShell 命令*，或者从 PowerShell 命令捕获的输出不可靠，请启用此项。这会向命令添加一个唯一的计数器，以帮助 PowerShell 区分它们。

##### 清除 ZSH EOL 标记
<img src="/img/shell-integration/shell-integration-4.png" alt="清除 ZSH EOL 标记复选框" width="600" />
特定于 Zsh 用户。如果行尾没有换行符，Zsh 有时会在行尾添加一个特殊字符（通常是 `%`）。如果 Roo Code 似乎误解或被 Zsh 命令的输出所迷惑，特别是如果输出的最后一行似乎包含意外字符，请启用此项。这将尝试删除该标记 (`PROMPT_EOL_MARK=''`)。

##### 启用 Oh My Zsh 集成
<img src="/img/shell-integration/shell-integration-5.png" alt="启用 Oh My Zsh 集成复选框" width="600" />
适用于流行的 Zsh 框架 Oh My Zsh 的用户。如果您使用 Oh My Zsh 并遇到其他设置无法解决的终端命令执行或输出呈现的一般性问题，请启用此项。这通过设置 `ITERM_SHELL_INTEGRATION_INSTALLED=Yes` 帮助 Roo Code 与 Oh My Zsh 的特定 shell 集成机制保持一致。可能需要重新启动 IDE。

##### 启用 Powerlevel10k 集成
<img src="/img/shell-integration/shell-integration-6.png" alt="启用 Powerlevel10k 集成复选框" width="600" />
适用于 Zsh 的 Powerlevel10k 主题的用户。如果您的 Powerlevel10k 提示（可能非常复杂）似乎干扰了 Roo Code 正确检测命令边界、解析输出或跟踪当前工作目录的能力，请启用此项。这将设置 `POWERLEVEL9K_TERM_SHELL_INTEGRATION=true`。

##### 启用 ZDOTDIR 处理
<img src="/img/shell-integration/shell-integration-7.png" alt="启用 ZDOTDIR 处理复选框" width="600" />
一个为具有自定义 Zsh 启动文件位置的 Zsh 用户准备的高级选项。如果您使用 `ZDOTDIR` 为您的 Zsh 配置文件（如 `.zshrc`）指定一个自定义目录，请启用此项。此设置通过为其自身的集成脚本创建一个隔离的、临时的 `ZDOTDIR`，帮助 Roo Code 在此类设置下正常工作，从而防止与您的个人 Zsh 环境发生冲突。

---

## Shell 集成如何工作

Shell 集成将 Roo 实时连接到您终端的命令执行过程：

1.  **连接**：当您打开终端时，VS Code 会与您的 shell 建立一个特殊的连接。

2.  **命令跟踪**：VS Code 通过检测以下内容来监视您的终端活动：
    -   何时出现新提示
    -   何时输入命令
    -   命令何时开始运行
    -   命令何时完成（以及是成功还是失败）
    -   您当前所在的目录

3.  **不同的 Shell，相同的结果**：每种 shell 类型（Bash、Zsh、PowerShell、Fish）在幕后的实现略有不同，但它们都为 Roo 提供了相同的功能。

4.  **信息收集**：Roo 可以看到正在运行的命令、它们在哪里运行、花费多长时间、是否成功以及它们的完整输出——所有这些都无需您复制和粘贴任何内容。

---

## Shell 集成故障排除

### PowerShell 执行策略 (Windows)

默认情况下，PowerShell 限制脚本执行。要进行配置：

1.  以管理员身份打开 PowerShell
2.  检查当前策略：`Get-ExecutionPolicy`
3.  设置适当的策略：`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

常用策略：
- `Restricted`：不允许任何脚本（默认）
- `RemoteSigned`：本地脚本可以运行；下载的脚本需要签名
- `Unrestricted`：所有脚本在出现警告的情况下运行
- `AllSigned`：所有脚本都必须签名

### 手动安装 Shell 集成

如果自动集成失败，请将相应的行添加到您的 shell 配置中：

**Bash** (`~/.bashrc`):
```bash
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path bash)"
```

**Zsh** (`~/.zshrc`):
```bash
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path zsh)"
```

**PowerShell** (`$Profile`):
```powershell
if ($env:TERM_PROGRAM -eq "vscode") { . "$(code --locate-shell-integration-path pwsh)" }
```

**Fish** (`~/.config/fish/config.fish`):
```fish
string match -q "$TERM_PROGRAM" "vscode"; and . (code --locate-shell-integration-path fish)
```

### 终端自定义问题

如果您使用终端自定义工具：

**Powerlevel10k**:
```bash
# 在 ~/.zshrc 中加载 powerlevel10k 之前添加
typeset -g POWERLEVEL9K_TERM_SHELL_INTEGRATION=true
```

**替代方案**：在 Roo Code 中启用 Powerlevel10k 集成设置。

### 验证 Shell 集成状态

使用以下命令确认 shell 集成是否处于活动状态：

**Bash**:
```bash
set | grep -i '[16]33;'
echo "$PROMPT_COMMAND" | grep vsc
trap -p DEBUG | grep vsc
```

**Zsh**:
```zsh
functions | grep -i vsc
typeset -p precmd_functions preexec_functions
```

**PowerShell**:
```powershell
Get-Command -Name "*VSC*" -CommandType Function
Get-Content Function:\Prompt | Select-String "VSCode"
```

**Fish**:
```fish
functions | grep -i vsc
functions fish_prompt | grep -i vsc
```

活动 shell 集成的视觉指示器：
1.  终端标题栏中的 shell 集成指示器
2.  命令检测高亮显示
3.  终端标题中工作目录的更新
4.  命令持续时间和退出代码报告

---

## WSL 终端集成方法

使用 Windows Subsystem for Linux (WSL) 时，有两种不同的方式可以将 VSCode 与 WSL 结合使用，每种方式对 shell 集成都有不同的影响：

### 方法 1：带有 WSL 终端的 VSCode Windows

在此设置中：
- VSCode 在 Windows 中本机运行
- 您在 VSCode 中使用 WSL 终端集成功能
- Shell 命令通过 WSL 桥执行
- 由于 Windows-WSL 通信，可能会遇到额外的延迟
- Shell 集成标记可能会受到 WSL-Windows 边界的影响：您必须确保为 WSL 环境中的 shell 加载了 `source "$(code --locate-shell-integration-path <shell>)"`，因为它可能不会自动加载；请参见上文。

### 方法 2：在 WSL 中运行的 VSCode

在此设置中：
- 您直接从 WSL 中使用 `code .` 启动 VSCode
- VSCode 服务器在 Linux 环境中本机运行
- 直接访问 Linux 文件系统和工具
- 更好的 shell 集成性能和可靠性
- Shell 集成会自动加载，因为 VSCode 在 Linux 环境中本机运行
- WSL 开发的推荐方法

为了与 WSL 实现最佳的 shell 集成，我们建议：
1.  打开您的 WSL 发行版
2.  导航到您的项目目录
3.  使用 `code .` 启动 VSCode
4.  在 VSCode 中使用集成终端

---

## 已知问题和解决方法

### Cygwin (bash, zsh)

Cygwin 在 Windows 系统上提供了一个类 Unix 的环境。要在 VS Code 中将 Cygwin 配置为您的终端：

1.  从 [https://www.cygwin.com/](https://www.cygwin.com/) 安装 Cygwin

2.  打开 VS Code 设置：
    -   选择文件 > 首选项 > 设置
    -   单击右上角的“打开设置 (JSON)”图标

3.  将以下配置添加到您的 `settings.json`（在顶层花括号 `{}` 内）：
    ```json
    {
      "terminal.integrated.profiles.windows": {
        "Cygwin": {
          "path": "C:\\cygwin64\\bin\\bash.exe",
          "args": ["--login"],
          "env": {"CHERE_INVOKING": "1"}
        }
      },
      "terminal.integrated.defaultProfile.windows": "Cygwin"
    }
    ```

    > 注意：如果您安装了 32 位 Cygwin，请使用 `"C:\\cygwin\\bin\\bash.exe"` 作为路径。

4.  理解配置：
    - `path`：指向您 Cygwin 安装中的 Bash 可执行文件
    - `args`：`--login` 标志确保 shell 读取配置文件
    - `env`：`CHERE_INVOKING` 环境变量告诉 Cygwin 使用当前目录作为工作目录
    - `terminal.integrated.defaultProfile.windows`：将 Cygwin 设置为默认终端配置文件

5.  要打开一个新的 Cygwin 终端：
    -   按 Ctrl+Shift+`（反引号）` 打开一个新终端，或者
    -   按 `F1`，键入“终端：创建新终端（使用配置文件）”，然后选择“Cygwin”

虽然我们的测试表明这可以开箱即用，但如果您在 Cygwin 中遇到 shell 集成问题，请确保您已按照“手动安装 Shell 集成”部分中的说明将适当的 shell 集成挂钩添加到您的 Cygwin bash 配置文件中。

### Windows 上 Fish + Cygwin 的 VS Code Shell 集成

对于在 Cygwin 环境中运行 Fish 终端的 Windows 用户，以下是 VS Code shell 集成的工作方式：

1.  **（可选）定位 Shell 集成脚本：**
    在 *VS Code 内* 打开您的 Fish 终端并运行以下命令：
    ```bash
    code --locate-shell-integration-path fish
    ```
    这将输出 `shellIntegration.fish` 脚本的路径。记下此路径。

2.  **更新您的 Fish 配置：**
    编辑您的 `config.fish` 文件（通常位于 Cygwin 主目录中的 `~/.config/fish/config.fish`）。添加以下行，最好在 `if status is-interactive` 块内或文件的最末尾：

    ```fish
    # 示例 config.fish 结构
    if status is-interactive
        # 您的其他交互式 shell 配置...
        # 自动定位集成脚本：
        string match -q "$TERM_PROGRAM" "vscode"; and . (code --locate-shell-integration-path fish)

        # 或者如果上述方法对您无效：
        # 加载 VS Code shell 集成脚本
        # 重要提示：请将下面的示例路径替换为您在步骤 1 中找到的实际路径。
        # 确保路径是 Cygwin 可以理解的格式（例如，使用 /cygdrive/c/...）。
        # source "/cygdrive/c/Users/YourUser/.vscode/extensions/..../shellIntegration.fish"
    end
    ```
    *请记住将示例路径替换为步骤 1 中的实际路径，并正确格式化以供 Cygwin 使用。*

3.  **配置 VS Code 终端配置文件：**
    打开您的 VS Code `settings.json` 文件（Ctrl+Shift+P -> “首选项：打开用户设置 (JSON)”）。在 `terminal.integrated.profiles.windows` 下更新或添加 Fish 配置文件，如下所示：

    ```json
    {
      // ... 其他设置 ...

      "terminal.integrated.profiles.windows": {
        // ... 其他配置文件 ...

        // 推荐：使用 bash.exe 作为登录 shell 启动 fish
        "fish": {
          "path": "C:\\cygwin64\\bin\\bash.exe", // 或您的 Cygwin bash 路径
          "args": [
            "--login", // 确保登录脚本运行（对 Cygwin 环境很重要）
            "-i",      // 确保 bash 以交互方式运行
            "-c",
            "exec fish" // 用 fish 替换 bash 进程
          ],
          "icon": "terminal-bash" // 可选：使用可识别的图标
        }
        // 备选方案（如果上述方法失败）：直接启动 fish
        "fish-direct": {
          "path": "C:\\cygwin64\\bin\\fish.exe", // 确保此路径在您的 Windows PATH 中或提供完整路径
          // 在这里使用 'options' 而不是 'args'；否则，您可能会遇到错误“终端进程已终止，退出代码为 1”。
          "options": ["-l", "-c"], // 示例：登录和交互式标志。
          "icon": "terminal-fish" // 可选：使用 fish 图标
        }
      },

      // 可选：如果需要，将 fish 设置为默认值
---

## 已知问题和解决方法
      // "terminal.integrated.defaultProfile.windows": "fish", // 或 "fish-direct"，取决于您使用的那个。

      // ... 其他设置 ...
    }
    ```
    *注意：在 Cygwin 环境中，使用 `bash.exe --login -i -c "exec fish"` 通常更可靠，以确保在 `fish` 启动前设置正确的环境。但是，如果该方法不起作用，请尝试 `fish-direct` 配置文件配置。*

4.  **重新启动 VS Code：**
    完全关闭并重新打开 Visual Studio Code 以应用更改。

5.  **验证：**
    在 VS Code 中打开一个新的 Fish 终端。shell 集成功能（如命令装饰、更好的命令历史导航等）现在应该处于活动状态。您可以通过运行简单的命令（如 `echo "Hello from integrated Fish!"`）来测试基本功能。<img src="/img/shell-integration/shell-integration-8.png" alt="Fish Cygwin 集成示例" width="600" />

此设置在使​​用 Cygwin、Fish 和 Starship 提示的 Windows 系统上可靠地工作，并应能帮助具有类似配置的用户。


### VSCode 1.98 之后 Shell 集成失败

**问题**：在 VSCode 更新到 1.98 版本之后，shell 集成可能会失败，并出现错误“未收到 VSCE 输出开始转义序列（]633;C 或 ]133;C）”。

**解决方案**：
1.  **设置终端命令延迟**：
    -   在 Roo Code 设置中将终端命令延迟设置为 50 毫秒
    -   更改此设置后重新启动所有终端
    -   这与旧的默认行为相匹配，可能会解决问题，但一些用户报告说 0 毫秒的值效果更好。这是针对上游 VSCode 问题的解决方法。

2.  **回滚 VSCode 版本**：
    -   从 [VSCode 更新](https://code.visualstudio.com/updates/v1_98) 下载 VSCode v1.98
    -   替换您当前的 VSCode 安装
    -   无需备份 Roo 设置

3.  **WSL 特定解决方法**：
    -   如果使用 WSL，请确保您从 WSL 内部使用 `code .` 启动 VSCode

4.  **ZSH 用户**：
    -   尝试在 Roo 设置中启用部分或全部 ZSH 相关的解决方法
    -   无论您的操作系统如何，这些设置都可以提供帮助


### Ctrl+C 行为

**问题**：当 Roo 尝试运行命令时，如果终端中已经输入了文本，Roo 会先按 Ctrl+C 清除该行，这可能会中断正在运行的进程。

**解决方法**：在要求 Roo 执行终端命令之前，请确保您的终端提示符为空（没有键入部分命令）。

### 多行命令问题

**问题**：跨多行的命令可能会使 Roo 感到困惑，并可能显示先前命令的输出与当前输出混合在一起。

**解决方法**：不要使用多行命令，而是使用 `&&` 进行命令链接，将所有内容保持在一行上（例如，`echo a && echo b`，而不是在单独的行上键入每个命令）。

### PowerShell 特定问题

1.  **过早完成**：PowerShell 有时会告诉 Roo 命令已完成，但此时尚未显示所有输出。
2.  **重复命令**：PowerShell 可能会拒绝连续两次运行相同的命令。

**解决方法**：启用“PowerShell 计数器解决方法”设置，并在设置中将终端命令延迟设置为 150 毫秒，以便为命令提供更多完成时间。

### 终端输出不完整

**问题**：有时 VS Code 不会显示或捕获命令的所有输出。

**解决方法**：如果您发现输出丢失，请尝试关闭并重新打开终端选项卡，然后再次运行命令。这将刷新终端连接。
---

## 故障排除资源

### 检查调试日志
当出现 shell 集成问题时，请检查调试日志：
1.  打开“帮助”→“切换开发人员工具”→“控制台”
2.  设置“显示所有级别”以查看所有日志消息
3.  查找包含 `[Terminal Process]` 的消息
4.  检查错误消息中的 `preOutput` 内容：
    -   空的 preOutput (`''`) 表示 VSCode 未发送任何数据
    -   这表明可能存在 VSCode shell 集成问题，或者是我们无法控制的上游错误
    -   缺少 shell 集成标记可能需要调整设置，以解决与 shell 初始化和 VSCode 加载特殊 shell 集成挂钩相关的可能的上游错误或本地工作站配置问题

### 使用 VSCode 终端集成测试扩展
[VSCode 终端集成测试扩展](https://github.com/KJ7LNW/vsce-test-terminal-integration) 通过测试不同的设置组合来帮助诊断 shell 集成问题：


1.  **当命令停滞时**：
    -   如果您看到“命令已在运行”的警告，请单击“重置统计信息”以重置终端状态
    -   这些警告表明 shell 集成不起作用
    -   尝试不同的设置组合，直到找到一个可行的组合
    -   如果它真的卡住了，请关闭窗口并按 F5 重新启动扩展

2.  **测试设置**：
    -   系统地尝试以下不同的组合：
        *   终端命令延迟
        *   Shell 集成设置
    -   记录哪些组合成功或失败
    -   这有助于识别 shell 集成问题的模式

3.  **报告问题**：
    -   一旦找到有问题的配置
    -   记录确切的设置组合
    -   记下您的环境（操作系统、VSCode 版本、shell 以及任何 shell 提示自定义）
    -   提交一个包含这些详细信息的问题，以帮助改进 shell 集成

### 其他资源

- [VSCode 终端输出问题 #237208](https://github.com/microsoft/vscode/issues/237208)
- [VSCode 终端集成测试存储库](https://github.com/KJ7LNW/vsce-test-terminal-integration)
- [Roo Code Shell 集成架构 PR](https://github.com/RooCodeInc/Roo-Code/pull/1365)

---

## 支持

如果您仍有问题：

1.  查看 [Roo Code GitHub Issues](https://github.com/RooCodeInc/Roo-Code/issues)
2.  创建一个新问题，并提供：
    -   操作系统和 VSCode 版本
    -   Shell 类型
    -   重现步骤
    -   错误消息

如需其他帮助，请加入我们的 [Discord](https://discord.gg/roocode)。
