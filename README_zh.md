# LuCI QFirehose 应用

QFirehose (v1.4.17) 的 LuCI 网页界面，为 OpenWrt 设备提供用户友好的移远（Quectel）模组高通固件烧写工具。

## 功能特点

- 全新自定义 DOM 布局，完美兼容 LuCI 主题
- 模组型号和当前固件版本显示（通过 AT 命令自动检测）
- 固件上传进度条
- 支持固件目录、`.zip` 和 `.7z` 压缩包（v1.4.17 内置解压）
- 自动 USB/PCIe 设备检测，支持一键刷新
- 终端风格实时日志监控
- 支持多个 USB 端口和设备
- 存储类型选择（NAND/eMMC/UFS）
- 可折叠高级选项：MD5 跳过、签名固件、USBMon 日志捕获、全擦除
- 固件路径支持手动编辑
- 烧写完成/失败后重置按钮
- 自动完成/失败检测与状态指示

## 支持的模组

QFirehose v1.4.17 支持众多移远模组，包括：

- EC20、EC25、EG25、EG06、EM05、EM06、EM12、EM20
- AG35、AG520R、AG525、AG550、AG590
- AG215S-GLR、AG215S-GLBA
- RM500Q、RM520N、RG500Q、RG520N
- SC600Y-EM、SC60-CE
- 以及更多...

## 依赖包

- luci-base
- cgi-io（固件文件上传）
- qfirehose（v1.4.17，自动包含 unzip 和 p7zip 依赖）
- socat（AT 命令通信，获取模组信息）

## 安装方法

1. 将此仓库添加到您的 OpenWrt 构建系统中

2. 编译软件包：

```bash
make package/luci-app-qfirehose/compile V=s
```

3. 在您的 OpenWrt 设备上安装生成的软件包：

```bash
opkg install luci-app-qfirehose_2.1.0_all.ipk
```

## 使用方法

1. 访问 OpenWrt 的 LuCI 网页界面
2. 导航到 调制解调器 -> QFirehose
3. 上传固件文件（目录、.zip 或 .7z）
4. 配置选项（端口、设备、存储类型等）
5. 点击"开始烧写"
6. 通过日志窗口监控进度

## 更新日志

### v2.1.0 (2026-02-15)

- **界面重写**：从 `form.Map` 改为自定义 DOM 布局，使用 LuCI 原生 `cbi-*` 类，完美兼容各种主题
- **模组信息**：通过 AT 命令（`ATI`、`AT+QGMR`）自动显示模组型号和当前固件版本
- **上传进度**：固件文件上传时显示实时进度条
- **刷新按钮**：「刷新设备」按钮同时刷新模组型号和固件版本信息
- **高级选项**：可折叠面板，包含 MD5 跳过、签名固件、USBMon 日志捕获（`-u`）、全擦除
- **可编辑路径**：固件路径输入框支持手动编辑
- **重置按钮**：烧写完成/失败后可一键重置状态
- **日志查看器**：终端风格暗色主题，带占位提示文字
- **实时日志**：直接重定向 stdout/stderr（移除 `tee` 管道），日志即时更新
- **状态脚本**：简化为纯文本输出，移除脆弱的 JSON 解析
- **ACL 权限**：更新所有脚本权限，包括 `qfirehose-modem-info`
- **翻译**：完整的中文（zh-Hans）翻译覆盖

### v2.0.0

- 将 QFirehose 从 v1.2 升级到 v1.4.17
- 新增 zip/7z 固件包支持（内置解压）
- 新增存储类型选择（NAND/eMMC/UFS）
- 新增签名固件支持（-v 参数）
- 新增 PCIe 设备检测（mhi/wwan）
- 修复烧写命令参数传递问题
- 简化启动脚本（移除手动解压逻辑）
- 改善日志轮询和状态检测
- 清理 ACL 权限和 init 脚本

## 许可证

本项目采用 GPLv3 许可证 - 详见 LICENSE 文件

## 作者

- Zag (<ntbowen2001@gmail.com>)
- 主页：<https://pcat.qsim.top>

## 贡献

欢迎提交贡献！请随时提交 Pull Request。
