# Changelog

## V1.1.2 - 核心规则补丁（已应用，待验收）

状态：补丁已应用到main分支；尚未完成独立行为测试和最终验收。版本号保持V1.1.2。

### 修订
- 强化学习进度、实验验证和知识掌握三维状态的原始名称约束
- 明确用户自述完成、部分证据和实际验证的区别
- 强化GitHub只读检查、工作区修改、本地提交和远程推送的独立授权
- 明确模糊指令不能扩大已有授权范围
- 细化本地网络状态读取与主动网络查询的边界
- 补充DHCP租约变更的网络影响和恢复检查
- 区分ICMPv4与ICMPv6的Echo报文Type编号
- 区分Wireshark捕获过滤器和显示过滤器

### 涉及文件
- skills/network-engineer-tutor/SKILL.md
- skills/network-engineer-tutor/references/vmware-labs.md
- skills/network-engineer-tutor/references/wireshark.md
- skills/network-engineer-tutor/references/learning-progress.md
- skills/network-engineer-tutor/references/github-learning.md
- skills/network-engineer-tutor/CHANGELOG.md

### 待验收
- 核心状态用例
- GitHub四阶段授权用例
- 网络操作分类和协议说明
- 原有教学功能回归检查

## V1.1.2 - 修正候选包

状态：待审核，未安装、未进行运行测试。

### 修复
- 明确错题模板相对Skill根目录的assets/wrong-answers-template.md路径
- 区分本地状态读取与主动DNS查询，后者遵循SKILL.md的L2授权及目标范围
- 明确实验环境服务配置变更通常按L2，生产环境及其他高风险变更按L3
- 每日目标保持30–45分钟：理论8–10、实验12–18、验证5–10、总结5分钟，合计30–43分钟

## V1.1.1 - 设计审核稿

状态：待审核，未安装，未完成运行测试。

### 修复
- 统一L0至L3操作授权规则
- 明确单次授权范围
- 分离学习进度、实验验证和知识掌握
- 将GitHub操作拆分为四个独立阶段
- 明确11份参考资料的职责
- 加强抓包、日志、拓扑和凭据保护
- 为学习、实验、错题和周报增加唯一ID
- 为记录增加来源、证据和更新时间

### 保留
- 网络理论教学
- VMware与Windows Server实验
- Ubuntu网络实验
- Wireshark抓包
- Python网络工具开发
- 网络工程师考试辅导
- IP规划
- 故障诊断
- GitHub学习成果管理

### 未实现
- 自动执行脚本
- 自动持久化学习数据
- 自动Git提交或推送
- 自动邮件和定时提醒
- Codex实际加载测试

## V1.1 - 扩展设计
增加6个功能模块和3个学习管理模板。

## V1.0 - 初始设计
建立基础网络教学、实验和报告规范。
