# user-story-write

为产品经理、开发者和方案负责人，把一个需求写成可向领导或客户讲述的精简用户故事。

输入：需求、角色、现有做法、已确认能力和约束。输出：默认中文约 500–700 字，按 S 用户背景、C 痛点与现有方案局限、Q 需要解决的问题、A 方案如何解决、最终价值与边界呈现。默认只在会话输出，不写业务文件。

故事包含公平的替代方案比较和相关代表产品；涉及当前竞品事实时查官方资料。自托管是条件能力，不固定套用，不能等同于数据不出网或安全保证。资料不足时仅询问会改变故事的关键问题；不代替完整 PRD。

## 从 GitHub 获取

```sh
git clone https://github.com/score2021/user-story-write.git
cd user-story-write
```

随后执行下面的本地安装代码。仓库：[score2021/user-story-write](https://github.com/score2021/user-story-write)。

## 本地安装

需要支持 skills 的 Codex；不依赖额外 Python 包。进入本目录（包含 SKILL.md），在 shell 执行以下完整代码。默认安装到用户级发现目录 `~/.agents/skills/user-story-write`，也可设置 `SKILL_INSTALL_ROOT` 到隔离目录测试。已有同名目录或断链时停止，不覆盖。

```sh
set -eu
skill_source_dir="$(pwd -P)"
skill_install_root="${SKILL_INSTALL_ROOT:-${HOME}/.agents/skills}"
skill_target_dir="${skill_install_root}/user-story-write"
test -f "${skill_source_dir}/SKILL.md"
if [ -e "${skill_target_dir}" ] || [ -L "${skill_target_dir}" ]; then
  echo "目标已存在，停止安装：${skill_target_dir}" >&2
  exit 1
fi
mkdir -p "${skill_install_root}"
mkdir "${skill_target_dir}"
cp "${skill_source_dir}/SKILL.md" "${skill_source_dir}/LICENSE" "${skill_target_dir}/"
cp -R "${skill_source_dir}/references" "${skill_target_dir}/references"
echo "已安装：${skill_target_dir}"
```

打开一个新会话调用；若列表尚未刷新，再重启客户端。对话输入示例：

```text
$user-story-write 为资产管理系统写一个月报助手的用户故事。方案已支持自托管，原系统负责定时触发和权限，平台负责工具执行、会话状态和报告交付。比较模型 API、自部署 Agent 和现成企业助手，保持精简，只在会话呈现。
```

终端最小复现（单引号保留 `$`）：

```sh
codex exec --skip-git-repo-check '$user-story-write 为门店排班经理写临时替班建议需求的用户故事。方案仅支持 SaaS，可读授权班表、匹配可用员工，由经理确认。替代方案是手工表格和既有排班软件，不要假设自托管；只在会话输出。'
```

可观察结果：五个分层标签；先痛点和现有选择，再讲本方案；保留经理确认责任；不凭空出现自托管。不要求恰好复现某段措辞。

## 范围、来源与成本

源于用户在产品讨论中明确认可的 SCQA 结构、信息密度及价值边界要求；示例为假设案例，不代表客户访谈或第三方能力认证。未复制原始会话、账号、凭据或项目代码。

无运行脚本、无外部服务强依赖；客户端推理和按需联网调研可能消耗相应额度。其他客户端尚未验证。

## 文件与验证

- `SKILL.md`：工作流程与输出契约。
- `references/example.md`：按需阅读的资产月报示例。
- `evals/cases.md`：合成正常与边界任务，不安装到运行目录。
- `LICENSE`：原创技能内容的 MIT 许可证。
- `.gitignore`：忽略本地临时文件。

本地实测 Codex CLI 0.162.1：基础格式、隔离安装、重复安装与断链目标拒绝、三项独立会话行为验收通过；合成测试见 `evals/cases.md`。未将测试日志、机器路径或原始会话打包。结构检查不代表内容质量通过；独立调用仅作代表性测试，不承诺所有需求都能一次达标。

Codex 技能发现说明参考：[官方文档](https://learn.chatgpt.com/docs/build-skills)。
