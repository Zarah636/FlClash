# FlClash Android“按需运行”后台定位临时修复

## 项目定位

这是上游 [chen08209/FlClash](https://github.com/chen08209/FlClash) 的非官方临时兼容分支。

本分支只做一项功能改动：在 Android Manifest 中补充
`android.permission.ACCESS_BACKGROUND_LOCATION` 权限声明，使用户能够在系统设置中授予
“始终允许”位置权限，缓解 FlClash 退到后台后无法读取 Wi-Fi SSID、进而导致“按需运行”
不能按指定 Wi-Fi 正常切换的问题。

对应上游问题：[FlClash #2233](https://github.com/chen08209/FlClash/issues/2233)。

## 维护状态

- 本项目仅用于这一项临时修复，不计划跟随上游持续更新，也不增加其他功能。
- 不保证提供安全更新、依赖更新、系统兼容性更新或技术支持。
- 上游正式修复该问题后，本仓库将停止发布并归档。
- FlClash 的版权、商标、功能与后续维护均归原项目及其贡献者；本分支不是官方版本。

## APK 限制

- 当前 APK 仅包含 `arm64-v8a`，不适用于 32 位 ARM 或 x86/x86_64 Android 设备。
- 包名为 `com.follow.clash.dev`，使用 Android Debug 证书签名。
- 因包名和签名不同，它会与官方 FlClash 并存，不能覆盖安装官方版本。
- 官方版和本临时版的数据彼此独立；配置、订阅和设置需要自行重新导入或配置。
- 不提供应用内自动更新，也不会接收官方 APK 的覆盖升级。
- 当前构建显示 `PRE` 角标；它表示预览构建渠道，不影响代理和权限功能。
- APK 基于 FlClash `0.8.94` 主线源码，仅验证了 Manifest、签名和 ARM64 原生库，未覆盖所有 Android 厂商系统和机型。

## 使用条件

1. Android 10 及以上系统中，安装后进入系统的 FlClash 应用权限页面。
2. 将位置权限设为“始终允许”，并开启精确位置。
3. 建议将 FlClash 的电池使用策略设为“不限制”，并允许后台运行/自启动。
4. 在 FlClash 的“按需运行”设置中添加需要停止或启动代理的 Wi-Fi SSID。

仅声明后台位置权限不能保证所有系统上的后台切换都绝对及时。部分厂商系统仍可能冻结或
终止 FlClash 进程；进程被杀死时，应用无法接收网络变化并执行按需规则。此时还需要检查
省电策略、自启动、后台运行限制和系统管家设置。

## 构建产物校验

- 版本：`0.8.94`
- 包名：`com.follow.clash.dev`
- 最低 Android：7.0（API 24）
- 目标 SDK：36
- ABI：`arm64-v8a`
- APK 签名：Android Debug，APK Signature Scheme v2
- SHA-256：`4324AC3947249802C53412A49F4D90D4DE9541D4D4F6E2A40CFE5DE7777BD486`

请仅从本仓库的 GitHub Releases 下载，并自行核对 SHA-256。