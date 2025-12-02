# YukiHook-md

## 项目概览（快速了解项目）
YukiHook-md 提供简洁的 Hook 配置示例，便于在文档中快速查阅常用字段与使用方式。所有标题均包含中文解释，确保阅读时一目了然。

## 基础信息（整体环境）
- **platformVersion（目标平台版本）**：指示 Hook 所面向的系统或框架版本，便于兼容性检查。
- **moduleVersion（当前模块版本）**：记录正在使用的 Hook 模块版本号，方便回溯与升级。
- **author（维护者信息）**：注明负责维护的开发者或团队，便于沟通与协作。

## Hook 配置（核心字段）
### packageName（当前 Hook 的 APP 包名）
用于指定需要注入 Hook 的目标应用包名，确保代码仅作用于正确的应用环境。

### entryClass（入口类名）
定义 Hook 逻辑的入口类全限定名，加载时会从此处开始执行自定义逻辑。

### enableLog（是否启用日志）
布尔值字段，控制 Hook 执行过程中的日志输出，便于调试与问题定位。

### features（功能开关列表）
以列表形式罗列可选功能，结合布尔开关灵活启用或关闭特性。

```kotlin
val hookConfig = HookConfig(
    packageName = "com.example.app",
    entryClass = "com.example.hook.Entry",
    enableLog = true,
    features = listOf("bypass-root-check", "inject-view-debugger")
)
```

## 分类结构（按用途组织）
1. **目标匹配类（定位目标）**：如 `packageName`、`entryClass`，用于明确 Hook 的作用范围。
2. **调试配置（辅助排查）**：如 `enableLog`，帮助在开发阶段快速捕捉执行细节。
3. **功能集（扩展能力）**：如 `features`，用于集中管理可选的 Hook 特性。

## 代码示例（调用方式）
以下示例展示如何在模块初始化时加载配置，并根据开关决定执行逻辑。

```kotlin
class HookInitializer {
    fun setup() {
        val config = hookConfig
        if (config.enableLog) {
            Logger.i("Hook 模块已加载: ${'$'}{config.packageName}")
        }
        FeatureManager.enable(config.features)
    }
}
```

## 使用提示（快速上手）
- 保持包名与入口类名与目标应用同步，避免注入失败。
- 调试阶段建议开启 `enableLog`，发布时视需要关闭以减少性能开销。
- 在 `features` 中集中添加或移除特性，保持配置文件整洁。
