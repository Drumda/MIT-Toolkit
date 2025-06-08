## 提示
此容器中所容纳的皆为 MIT Toolkit 的源代码，旨在为各位提供学习用途。

# MIT Toolkit LocalServer API 文档

## 远程控制指令列表

| 命令名称 | 作用 | 参数格式 | 参数数量 | 返回值 |
|---------|------|---------|---------|-------|
| `RegisterLinkCert` | 注册新链接并生成LinkID | `"name":"链接名称"` | 1 | 返回格式：`"ip=IP地址@ name=名称! linkid=ID;"` |
| `TestLinkIDFunction` | 验证LinkID有效性 | `"linkid":"链接ID"` | 1 | `"successful"` 或 `"cert error"` |
| `Refresh` | 刷新指定类型数据 | `"type":int` (0=重启插件，1=刷新网络，2=刷新插件列表) | 1 | `"successful"` 或 `"cancel"` |
| `Prompt` | 弹出提示窗口 | `"title":"标题"`, `"text":"内容"`, `"type":int` (1=信息，2=警告，3=错误，4=盾牌) | 3 | `"successful"` 或 `"API call failed"` |
| `RunCommand` | 执行系统命令 | `"Command":"命令"`, `"Wait":"true/false"` | 2 | `"successful"` 或 `"Task execution failed"` |
| `RunDLLCommand` | 调用DLL函数 | `"DLL_Path":"路径"`, `"Command":"指令"`, `"arg1-15":int` | 最多16 | 返回DLL执行结果或错误码 |
| `ToastNotice` | 弹出Toast通知 | `"Title":"标题"`, `"Text":"内容"`, `"HintIcon":int`, `"NotificationTime":int` | 4 | `"successful"` |

## 下载源管理指令

| 命令名称 | 作用 | 参数格式 | 参数数量 | 返回值 |
|---------|------|---------|---------|-------|
| `SetupCustomDownloadSourceState` | 启用/禁用自定义下载源 | `"State":"true/false"` | 1 | `"Successful"` |
| `SetupCustomDownloadSourceLink` | 设置下载源URL | `"State":"URL地址"` | 1 | `"Successful"` |
| `GetCustomDownloadLink` | 获取当前下载源 | 无 | 0 | 返回URL或`"error"` |
| `GetCustomDownloadState` | 检查下载源状态 | 无 | 0 | `"CustomDownloadSource:true/false"` |

## 系统配置指令

| 命令名称 | 作用 | 参数格式 | 参数数量 | 返回值 |
|---------|------|---------|---------|-------|
| `SetToUseUWPStyles` | 切换UWP风格 | `"State":"true/false"` | 1 | `"Successful"` |
| `SetAccentColor` | 设置主题色 | `"Color":int` (ARGB值) | 1 | `"Successful"` 或 `"Unable to apply configuration"` |
| `HideWindow` | 隐藏/显示窗口 | `"Hide":"true/false"` | 1 | `"Successful"` |

## 网络信息指令

| 命令名称 | 作用 | 参数格式 | 参数数量 | 返回值 |
|---------|------|---------|---------|-------|
| `Getipconfig` | 获取网络配置 | 无 | 0 | 返回ipconfig信息 |

## 错误代码说明

- `cert error (403)`: LinkID验证失败
- `linkid error`: 未提供有效LinkID
- `unknown parameters`: 未知参数类型
- `RunDLLError`: DLL调用失败
- `API call failed`: API调用失败

> **注意**：所有指令都需要通过已认证的LinkID发起请求，除`RegisterLinkCert`外。
