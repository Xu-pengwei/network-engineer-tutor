# Packetlyra · Network Engineer Tutor

中文计算机网络学习与实验辅导 Skill。[English](README.en.md)

## 状态

V1.1.2 修正候选包，尚未完成独立环境验收。当前目录是独立发布准备副本，不代表已发布或已安装。

## 内容

提供网络理论、考试复习、VMware 与服务器实验、Wireshark 分析、IP 规划、故障诊断和 Python 网络项目学习指导。
包含主说明、11 份领域参考资料、4 份记录模板和变更记录。Python 项目清单是教学路线，不附带这些工具的实现。

## 目录

- `skills/network-engineer-tutor/SKILL.md`：主说明
- `skills/network-engineer-tutor/references/`：领域参考资料
- `skills/network-engineer-tutor/assets/`：空白记录模板
- `skills/network-engineer-tutor/CHANGELOG.md`：原始版本记录
- `docs/testing-plan.md`：隔离测试计划与验收标准
- `LICENSE`：MIT 许可证

## 使用与兼容性

先阅读主说明，并确认客户端支持相应 Skill 格式、参考资料加载及工具权限。安装路径、安装命令和支持客户端清单尚待隔离测试确认，暂不提供未经验证的安装命令。

示例请求：

- “解释 DNS 解析过程，并给我一道复习题。”
- “根据我提供的输出分析故障，先只读检查。”
- “生成实验报告草稿，缺少的证据标为待验证。”

## 授权和隐私

说明和草稿不代表操作已经执行。文件修改、环境配置、安装依赖、主动网络探测、本地提交和远程推送须分别按明确范围授权。只在拥有或明确获准测试的环境中操作。

模板用于生成草稿；真实学习记录应保存到用户批准的位置。不要公开凭据、私人记录、内部拓扑或未脱敏抓包。

## 未实现与未验证

尚未实现自动执行脚本、自动持久化学习数据、自动 Git 提交或推送、自动邮件和定时提醒。
已完成14项离线静态检查，并对用户提供的人工聊天回答进行了内容审阅。人工回答中发现状态命名与授权流程建议不一致；上传模板后的报告结构基本符合要求。这些结果不证明本地 Skill 已加载或工具操作已核验。实际本地加载、完整运行行为及跨客户端兼容性仍未验证。技能被列出或目录存在不代表测试通过。复习日期和提交说明只是建议或草稿。

详见[人工测试汇总](docs/manual-test-summary.md)、[离线检查报告](docs/offline-validation-report.md)、[启动尝试记录](docs/runtime-test-attempt.md)及[未应用的规则澄清草案](docs/proposed-rule-clarifications.md)。技能正文未修改，继续保持候选包状态。

现有材料为 Markdown 说明与模板，无随附执行程序或依赖安装器。实验可能需要自行准备操作系统、虚拟化软件、Python 或 Wireshark。第三方插件不是强制依赖。

## 来源与许可证

材料由维护者在 AI 协助下完成；此说明不代表对全部内容的可版权性或第三方权属作出保证。后续贡献应注明来源并确认再分发权限。

采用 [MIT 许可证](LICENSE)。Copyright (c) 2026 Packetlyra。
品牌名称不表示获得所提及第三方产品的官方认可。
