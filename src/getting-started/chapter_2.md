# 安装

## 安装Web3.js

您可以使用一些库来开始在 Solana 上使用 javascript 或 typescript。

### Web3.js

`@solana/web3.js` 是一个库，其中包含许多用于交互、发送交易和从区块链读取的基本 Solana 工具。

您可以使用以下命令进行安装：

```bash
# using yarn
yarn add @solana/web3.js

# using npm
npm install --save @solana/web3.js

# using browser

<!-- Development (un-minified) -->
<script src="https://unpkg.com/@solana/web3.js@latest/lib/index.iife.js"></script>

<!-- Production (minified) -->
<script src="https://unpkg.com/@solana/web3.js@latest/lib/index.iife.min.js"></script>
```

### SPL-代币

`@solana/spl-token` 是一个库，其中包含与 SPL 令牌交互所需的许多 javascript/typescript 绑定。您可以使用此库铸造新的 SPL 代币、转移代币等。

您可以使用以下命令安装该库：

```bash
# using yarn
yarn add @solana/spl-token

# using npm
npm install --save @solana/spl-token

# using browser
<!-- Development (un-minified) -->
<script src="https://unpkg.com/@solana/spl-token@latest/lib/index.iife.js"></script>

<!-- Production (minified) -->
<script src="https://unpkg.com/@solana/spl-token@latest/lib/index.iife.min.js"></script>
```


### 钱包适配器

有一组库可以帮助在 Solana 内引导钱包连接，称为钱包适配器。目前该包支持在 Svelte、Angular、Vue.js 和 React 中使用。钱包适配器可以快速启动您的 dApp 与 [Phantom](https://phantom.app/)、[Solflare](https://solflare.com/) 等钱包的集成。

您可以使用以下命令安装该库：

```bash
# using yarn
yarn add @solana/wallet-adapter-wallets \
    @solana/wallet-adapter-base

# using npm
npm install --save @solana/wallet-adapter-wallets \
    @solana/wallet-adapter-base

```

## 安装 Rust


```bash

# macos
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# linux

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

对于 Windows，请访问 [Rust 安装站点](https://www.rust-lang.org/tools/install)。

## Install CLI

### macOS 和 Linux

打开您最喜欢的终端应用程序。

将 LATEST_RELEASE 替换为您所需的版本，并通过运行以下命令在您的计算机上安装[最新](https://github.com/solana-labs/solana/releases)的 Solana 版本：

```bash
sh -c "$(curl -sSfL https://release.solana.com/LATEST_RELEASE/install)"
```

您可以将 LATEST_RELEASE 替换为与所需版本的软件版本匹配的版本标记，或使用三个符号通道名称之一： stable 、 beta 或 edge 。要查找最新版本，请在[此处检查可用版本](https://github.com/solana-labs/solana/releases)。

以下输出表明更新成功：

```bash
downloading LATEST_RELEASE installer
Configuration: /home/solana/.config/solana/install/config.yml
Active release directory: /home/solana/.local/share/solana/install/active_release
* Release version: LATEST_RELEASE
* Release URL: https://github.com/solana-labs/solana/releases/download/LATEST_RELEASE/solana-release-x86_64-unknown-linux-gnu.tar.bz2
Update successful
```

根据您的系统，安装程序消息结束时可能会提示您

```bash
Please update your PATH environment variable to include the solana programs:
```

如果您收到上述消息，请复制并粘贴其下方的推荐命令来更新 PATH 。

通过运行以下命令确认您已安装所需版本的 solana ：

```bash
solana --version
```

成功安装后， `solana-install update` 可用于随时轻松地将 Solana 软件更新到新版本。

### 下载二进制文件 (Linux)

或者，您可以从二进制文件安装，而不是使用 solana-install。

导航到 [https://github.com/solana-labs/solana/releases/latest]https://github.com/solana-labs/solana/releases/latest() 下载二进制文件，下载 solana-release-x86_64-unknown-linux-msvc.tar.bz2，然后解压存档：

```bash
tar jxf solana-release-x86_64-unknown-linux-gnu.tar.bz2
cd solana-release/
export PATH=$PWD/bin:$PATH
```

### 下载二进制文件 (macOS)

或者，您可以从二进制文件安装，而不是使用 solana-install。

导航到 [https://github.com/solana-labs/solana/releases/latest](https://github.com/solana-labs/solana/releases/latest) 下载二进制文件，下载 solana-release-x86_64-apple-darwin.tar.bz2，然后解压存档：

```bash
tar jxf solana-release-x86_64-apple-darwin.tar.bz2
cd solana-release/
export PATH=$PWD/bin:$PATH
```

### Windows

以管理员身份打开命令提示符 ( cmd.exe )。

在 Windows 搜索栏中搜索命令提示符。当命令提示符应用程序出现时，右键单击并选择“以管理员身份打开”。如果弹出窗口提示您“是否允许此应用程序对您的设备进行更改？”，请单击“是”。

复制并粘贴以下命令，然后按 Enter 键将 Solana 安装程序下载到临时目录中：

```bash
curl https://release.solana.com/v1.9.16/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs
```

如果 v1.9.16 不是您想要的版本，请在[此处查找最新版本](https://github.com/solana-labs/solana/releases)。

复制并粘贴以下命令，然后按 Enter 键安装最新版本的 Solana。如果您看到系统弹出安全窗口，请选择允许该程序运行。

```bash
C:\solana-install-tmp\solana-install-init.exe v1.9.16
```

要查找最新版本，请在[此处检查可用版本](https://github.com/solana-labs/solana/releases)。

安装程序完成后，按 Enter 键。

关闭命令提示符窗口并以普通用户身份重新打开新的命令提示符窗口。

在搜索栏中搜索“命令提示符”，然后左键单击命令提示符应用程序图标（无需以管理员身份运行）。

通过输入以下内容确认您已安装所需版本的 solana ：

```bash
solana --version
```

成功安装后， solana-install update 可用于随时轻松地将 Solana 软件更新到新版本。


### 下载二进制文件

或者，您可以从二进制文件安装，而不是使用 solana-install。

通过导航到 [https://github.com/solana-labs/solana/releases/latest](https://github.com/solana-labs/solana/releases/latest) 下载二进制文件，下载 solana-release-x86_64-pc-windows-msvc.tar.bz2，然后使用 WinZip 或类似工具提取存档。

打开命令提示符并导航到您提取二进制文件的目录并运行：

```bash
cd solana-release/
set PATH=%cd%/bin;%PATH%
```

### 从源代码构建

如果您无法使用预构建的二进制文件或者更喜欢自己从源代码构建它，请导航到 [https://github.com/solana-labs/solana/releases/latest](https://github.com/solana-labs/solana/releases/latest)，然后下载源代码存档。提取代码并使用以下命令构建二进制文件：

```bash
./scripts/cargo-install-all.sh .
export PATH=$PWD/bin:$PATH
```

然后，您可以运行以下命令以获得与预构建二进制文件相同的结果：

```bash
solana-install init
```
