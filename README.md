# DSH Motion UI

简体中文 | [English](README.en.md)

让 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 的回答按需变成**可交互界面、图解与动画**：从对比表、测验和参数计算，到 HTML/SVG 画布、机械演示与本地视频制作。模型仍可正常使用文字回答；是否生成界面取决于任务、模型和设置。

## 能做什么？

| 场景 | 能力 |
| --- | --- |
| 日常说明 | 卡片、对比、流程、时间线、代码、公式与选项卡 |
| 数据探索 | 表格筛选 / 排序、CSV 导出、图表和可调参数 |
| 学习与收集信息 | 本地测验、表单、函数图和结构图解 |
| 自由表达 | 模型生成的 HTML/SVG、动画、基础 3D 和交互画布 |
| 机械演示 | 装配拆解、齿轮和曲柄连杆等可调示意 |
| 视频制作 | 动效时间轴、分镜预览、MP4 导出、剪辑，以及可选的配音和字幕 |

生成的界面可以在正文和 **智能 UI** 侧栏查看；兼容的参数与部分视图状态可保存，后续也可让模型修改已有界面。控件变化在本地响应，只有明确提交后续请求时才会把参数发送给 Agent。

## 实际生成示例

下图来自开发期的真实 DSH 会话。第一张由 DeepSeek V4.1 Flash Fast 在电路问题中主动生成；第二张由 DeepSeek V4.1 Flash 按动画需求生成，展示的是静态截图。效果随模型与提示词变化，示意图不等同于精确仿真。

![串并联电路的交互讲解：电路、参数和对比曲线](https://raw.githubusercontent.com/Scorp1o117/dsh-motion-ui/main/docs/screenshots/fast-circuits.png)

![可调节振幅和频率的单摆动画示意](https://raw.githubusercontent.com/Scorp1o117/dsh-motion-ui/main/docs/screenshots/flash-pendulum.png)

[查看全部截图及来源](docs/screenshots/README.md)。

## 兼容性与安装

- 支持 DSH **Web / Desktop**；当前仓库明确声明兼容 `0.2.0-rc.2`、`0.2.1-rc.1`、`0.2.1-rc.2` 和 `0.2.1-rc.3`，以 [package.json](package.json) 为准。
- 要求 Node.js `>=22.19`。日常界面不需要视频工具链；视频制作的额外要求见下文。

Desktop 先在 **应用 → 管理 dsh 命令** 安装桌面版 `dsh`：

```sh
dsh plugin --profile desktop add dsh-motion-ui
```

Web 将 `desktop` 改为 `web`。安装后重启 DSH；Web 还需刷新浏览器页面。插件设置位于 **插件 → 已安装 → dsh-motion-ui**，也可通过 [Enhancement Suite](https://github.com/Scorp1o117/dsh-enhancement-suite) 安装。

如果安装过开发版 `dsh-generative-ui`，请先卸载旧插件，再安装 Motion UI；两者注册相同工具，不应同时启用。旧界面文档保留兼容读取，但需要在新插件入口重新选择设置。

## 快速开始

直接提出适合可视化的需求，例如：

- “用可调参数的界面解释电压、电流和功率的关系。”
- “把这两个方案做成对比表，让我调整预算。”
- “做一个带答案解析的本地小测验。”
- “用动画展示齿轮传动，提供转速和暂停控件。”

在插件设置中可选择**引导模式**或**自由模式**。引导模式提供设计指导、风格和示例；自由模式让模型自主设计，不注入这套风格与案例。模型是否主动调用工具，以及界面质量和准确性，取决于模型及请求。

## 工具与工作方式

| 工具 | 用途 |
| --- | --- |
| `render_text` / `render_scene` | 快速文字排版或常见流程、对比、分配和预算场景 |
| `render_ui` | 经校验的原生组件、图表、测验和表单 |
| `render_canvas` | 自由 HTML / SVG 画布与动画 |
| `render_mechanism` | 装配、齿轮、曲柄连杆示意 |
| `ui_catalog` | 按需获取协议、字段和示例 |
| `inspect_ui` / `update_ui` / `patch_ui` | 查看和继续修改已有界面 |

生成过程中可渐进预览已完成的内容；正式交互在结果成功交付并恢复状态后启用。对 PTC / 组合工具调用，部分宿主路径可能只显示文本回退。卸载插件不会自动删除保存在本地的界面状态。

## 视频制作

明确要求制作视频时，模型可预览时间轴、渲染 MP4、检查视频或拼接片段；也可交付可编辑源码与工程文件。使用前请准备本机 **Chrome / Edge 或 Playwright Chromium、FFmpeg 和 FFprobe**，插件不会自动下载浏览器或编码器。可在插件设置中检查视频环境。

配音可选使用 MiniMax，需要单独配置认证并可能产生 API 费用；没有配音服务也可制作无声动效。普通对话不会自动导出视频。抽帧检查只覆盖采样画面，不等同于完整视觉、音频或内容审核。

## 限制与安全

- 图表、计算和示意图的正确性取决于输入数据、模型生成和具体实现；专业用途请核对结果。
- 自由画布运行于隔离 iframe，限制对宿主页面及网络的访问；隔离不提供硬性的 CPU / 内存上限，复杂或异常代码仍可能影响页面响应。
- 不要将无关的密钥或私密内容交给生成的画布。外部服务、模型和素材各有自己的使用条件。
- 本项目不声称实现 ChatGPT 的专有 UI 协议或编译器。

## 更多资料

- [更新记录](CHANGELOG.md) · [验证说明](VERIFICATION.md) · [历史详细文档](https://github.com/Scorp1o117/dsh-motion-ui/blob/52ad63919cd1b40b26f80a65102ca1459b4a7ec4/README.md)（包含协议与示例；旧安装和兼容性信息可能过时）
- 扩展组件核心复用 [dsh-genui](https://github.com/omdsh-dev/dsh-genui)；机械图解参考 Anatomy；动效技能来自 OpenDesign。具体版本、来源和许可见 [dsh-genui NOTICE](lib/third-party/dsh-genui-NOTICE.md)、[Anatomy NOTICE](lib/third-party/anatomy-NOTICE.md) 和 [motion-design NOTICE](skills/motion-design/NOTICE.md)。
- [npm](https://www.npmjs.com/package/dsh-motion-ui) · [问题反馈](https://github.com/Scorp1o117/dsh-motion-ui/issues) · [MIT License](LICENSE)
