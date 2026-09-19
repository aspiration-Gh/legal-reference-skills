<div align="center">

# Legal Reference Skills

**面向合同审查、数据合规与劳动社保的三个按需加载技能**

简体中文 · [English](README.en.md)

[技能](#skills) · [安装](#install) · [使用](#usage) · [实现原理](#how-it-works) · [来源与边界](#sources)

</div>

将三部法律参考书整理成可供智能助手按问题查阅的知识结构：判断步骤、条件与例外、证据提示、来源页码和章节索引。适合先建立分析框架，再核验适用的官方法条。

<a id="skills"></a>
## 三个技能

| 技能 | 内容 | 结构 |
|---|---|---|
| [`civil-code-contracts`](skills/civil-code-contracts/SKILL.md) | 合同订立与效力、履行、解除、违约救济及典型合同 | 绪论＋29章，共30篇 |
| [`cyber-data-law`](skills/cyber-data-law/SKILL.md) | 网络安全、数据处理、个人信息、附录规则与交叉分析 | 28个模块 |
| [`labor-social-security`](skills/labor-social-security/SKILL.md) | 劳动合同、工资工时、人事争议、社会保险与救助 | 30个模块 |

每个技能均包含 `SKILL.md`、`chapters/`、`glossary.md`、`patterns.md`、`cheatsheet.md`、`sources.md` 和公开覆盖清单 `coverage.json`。三个技能可在数据处理协议、技术外包、招聘与用工等场景下联合使用。

正文以中文编写；双语 README 不代表全部技能正文已经翻译。

<a id="install"></a>
## 安装

### Hermes Agent

将 `skills/` 中的三个目录复制到**当前配置档**的 `${HERMES_HOME}/skills/law/` 下。若未设置 `HERMES_HOME`，默认路径为 `~/.hermes/skills/law/`。遇到同名技能先备份或比较，不直接覆盖。

```text
<HERMES_HOME>/skills/law/
├── civil-code-contracts/
│   ├── SKILL.md
│   └── ...
├── cyber-data-law/
│   ├── SKILL.md
│   └── ...
└── labor-social-security/
    ├── SKILL.md
    └── ...
```

可使用以下 Bash 命令；脚本遇到同名目录会停止：

```bash
git clone https://github.com/aspiration-Gh/legal-reference-skills.git
python - <<'PY'
import os
import shutil
from pathlib import Path

source = Path('legal-reference-skills/skills')
home = Path(os.environ.get('HERMES_HOME', str(Path.home() / '.hermes')))
target = home / 'skills' / 'law'
names = ('civil-code-contracts', 'cyber-data-law', 'labor-social-security')
for name in names:
    if (target / name).exists():
        raise SystemExit(f'Already exists: {target / name}')
for name in names:
    shutil.copytree(source / name, target / name)
print('Installed all three skills.')
PY
```

Windows 也可通过文件管理器完成复制。新会话中让助手列出 `law` 分类技能并读取一个章节，确认发现与加载成功。

### 其他技能宿主

将各技能的整个目录复制到宿主支持的技能目录，保留相对路径。文件采用 `SKILL.md` 入口；自动发现方式由宿主决定，未对所有宿主逐一验收。

<a id="usage"></a>
## 使用示例

英文标识保持稳定，直接用以下中文名称即可触发对应技能（自然语言匹配，不是另建同名技能）：

| 调用名称 | 英文标识 | 范围 |
|---|---|---|
| 民法典 | `civil-code-contracts` | 当前覆盖合同编，不代表整部法典 |
| 网安相关法律 | `cyber-data-law` | 网络安全、数据与个人信息 |
| 劳动法 | `labor-social-security` | 劳动、人事及社会保障 |

例如：“调用劳动法，分析这份解除劳动合同通知；先列事实缺口和证据，再核验适用法条。”

```text
用 civil-code-contracts 审查这份服务合同：先列事实缺口，
再检查验收、解除和违约责任，区分书中解释与已核验的适用法条。
```

```text
用 cyber-data-law 分析这个 SDK 采集场景：
列出主体、目的、字段、接收方和保存期限，再判断需要补充哪些事实。
```

```text
联合两个技能检查数据处理协议：
分别分析合同责任和数据行为的合法性，不把合同授权当作全部依据。
```

建议提供法域、关键日期、主体角色、相关条款和事实；提交前自行隐去不必要的个人信息。未联网核验时，助手应明确只提供条件化书籍分析。

<a id="how-it-works"></a>
## 实现原理

```mermaid
flowchart LR
    A[问题与事实] --> B[技能入口与主题路由]
    B --> C[按需读取章节及配套文件]
    C --> D[区分书载规则、编者解释和应用推演]
    D --> E[核验官方适用文本]
    E --> F[条件结论、证据缺口与下一步]
```

| 效果 | 机制 | 当前边界 |
|---|---|---|
| 按问题查阅 | 入口索引、章节拆分、术语与速查 | 依赖助手遵循路由，不是独立搜索服务 |
| 交叉分析 | 主题路由与技能联动 | 需要宿主可发现相关技能 |
| 回查依据 | 章节及构建来源的 PDF 页码 | 原书未分发，其他版本页码可能不同 |
| 避免把旧书当现行法 | 适用时点与官方核验指引 | 是工作流要求，不是自动更新数据库 |

本仓库没有后台服务、账户绑定或 API 密钥配置。官方来源检索依赖宿主具备联网工具；技能本身不调用外部 API。构建使用了 [book-to-skill](https://github.com/virgiliojr94/book-to-skill) 工作流，并补充了法律来源分层、例外和核验边界。

## 验证

公开版检查包括文件完整性、相对链接、88篇章节/模块清单、公开文件哈希、隐私模式筛查、入口格式及已知注入模式扫描。原始安装版已在 Hermes 上确认发现与配套文件加载；公开版调整了技能标识和来源说明。

这些检查不等于逐字 OCR 校对或法律正确性认证。制作日志、安装记录、机器路径、账户凭据与原始提取文本均不分发。

<a id="sources"></a>
## 来源与边界

**书籍来源暗号：`Z-library`**

以下书名、格式和大小为提供者指定的书目检索标记，原样列示；未核验平台条目或可下载性，不代表实际转换输入格式。三个技能均基于所提供的 PDF 副本构建，EPUB 的分页可能不同。

| 对应技能 | 书籍名称 | 格式 | 标注大小 |
|---|---|---|---|
| 劳动法 | 中华人民共和国劳动和社会保障法律法规全书：含全部规章及法律解释：2022年版 | EPUB | 14.22MB |
| 网安相关法律 | 网络安全法、数据安全法、个人信息保护法一本通 | EPUB | 603KB |
| 民法典 | 中华人民共和国民法典合同编理解与适用 | PDF | 370.19MB |

来源标记不附下载链接，也不构成版权或再分发许可声明。请核实所用副本的合法获取与使用范围。

- 劳动社保全书：2022年版，2021年12月第8版，ISBN `978-7-5216-1794-8`；见[劳动法来源说明](skills/labor-social-security/sources.md)。

- 《民法典合同编理解与适用》（书名简称）：人民法院出版社；后记署2020-07-15，具体版次未确认。见[合同来源说明](skills/civil-code-contracts/sources.md)。
- 《网络安全法、数据安全法、个人信息保护法一本通》：2021年10月第1版，ISBN `978-7-5216-2233-1`。见[数据合规来源说明](skills/cyber-data-law/sources.md)。

本仓库当前不提供原书文件或下载链接。除下列按要求保留的完整书名外，技能正文继续采用中性简称；这不改变规则的地域适用范围。引用和实际应用前须确认完整名称、版本和适用法域。

保留旧版规则、解释争议与 OCR 疑点，不做全量现行法更新。实际事项须核验当时适用的法律、司法解释、施行废止和过渡安排；本资料不构成个案法律意见。

公开可访问不等于为原书及第三方材料授予再许可；本次发布未指定额外开源许可证。详见 [RIGHTS.md](RIGHTS.md)。
