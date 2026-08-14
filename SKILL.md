---
name: 进化-升仙
description: "全资源自进化引擎: 千面启动 -> 全盘扫描(8域+凝魂材料) -> 水桶分析 -> 化神评分门控(≥7.0跳过) -> 委托修复 -> 凝魂结晶复盘。双模式: 进化(渐进) + 升仙(质变)"
tags: [META, evolution, self-optimization, upgrade, 升仙, 凝魂]
platform: windows
version: "1.4"
domain: META
tier: core
triggers:
  - 进化
  - 升仙
  - 全盘优化
  - 系统体检
  - 自进化
  - 全面分析
  - 全资源体检
last_updated: 2026-07-25
changelog:
  v1.4: 2026-07-25, frontmatter补全+last_updated注入
---

# 进化·升仙 — 全资源自进化引擎 v1.4

> 千面启动 -> 全盘扫描(8域+凝魂材料) -> 水桶分析 -> 化神评分门控(≥7.0跳过) -> 委托修复 -> 凝魂结晶复盘
> v1.4 | 2026-06-28 | 域: META > ORCHESTRATE
> 域路由注册: v7.8 L0
> 变更: v1.4新增Step 2.5化神评分门控(决策点) + Ollama统一模型策略 + 评分门控执行规范

## 触发词 (已注册到域路由 v7.8 L0)

进化 / 升仙 / 全盘优化 / 系统体检 / 自进化 / 全面分析 / 全资源体检

**子触发**:
- `进化: 启动词` — 审计启动词系统HTML vs 域路由一致性，补入缺失路由，进化SKILL.md
- `进化: {SKILL名}` — 定向优化指定SKILL.md（化神分析->水桶->委托->焚诀执行->凝魂）
- `进化: 全盘` — 默认全8域水桶分析

## 执行管线 (7步骤)

```
Step 0: 千面启动 -> 千面诊断(Bloom+Fuller问题类型) + 域路由匹配
Step 1: 全盘映射 -> 八大域现状清单
Step 1.5: 凝魂材料集成 -> KG结晶/研究报告/会话记忆可复用模式提取
Step 2: 水桶分析 -> 逐域快速扫描 -> 短板排行(TOP3) -> 归因
Step 2.5: 化神评分门控 ← 决策点
  → 加载化神rubric.md 9维评分框架
  → 对TOP3短板域做正式化神评分(composite = Σ(维度分×权重)/100×10)
  → composite ≥ 7.0 → 跳过进化(系统健康,输出健康报告)
  → composite < 7.0 → 进入Step 3执行进化
Step 3: 委托化神引擎 -> 化神评分 + 结果回写 + 触发焚诀批量执行
Step 4: 凝魂复盘 -> 进化前后对比 + 归墟收尾 + 注册表更新 -> 模式自进化
```

## 反模式 (P0优先)

- **P0: 进化目标选择铁律** - 优化目标是**SKILL.md**(技能实现),不是HTML/部署词文档。正确顺序: 化神分析SKILL.md -> 对比HTML -> 优化SKILL.md -> 同步HTML
- **P0: 模块化优先** - SKILL.md > 20KB时先拆模块化(评分驱动加载),再做内容优化。参考: 化神52KB→9KB入口+6子模块
- **P0: 执行顺序纪律** - 当任务有多阶段时(如集成→写脚本),必须先完成前置阶段再进入后置。用户说"先完成集成再写"→ 化神分析→集成→验证→再写,不是同时推进
- **P0: 引用模式优先** - 创建新功能模块时,优先用引用模式(参考文献清单.md指向外部源路径),不复制已有资源。指令库200+文件只引用不存储,模块保持轻量
- **P0: 角色智库内置** - 新建功能模块应包含角色智库/子目录(INDEX+动态推荐矩阵),按输出类型×场景参数动态推荐最佳角色组合,对接千面全域适配引擎
- 不跳过Step 1.5凝魂集成 - 缺失KG结晶/研究报告/会话记忆中的可复用模式
- **P0: 化神评分门控必经** - Step 2.5是决策点,不可跳过。先评分再决定是否进化,避免无谓优化。composite≥7.0直接输出健康报告,<7.0才进入Step 3
- 不跳过Step 1.5凝魂集成 - 缺失KG结晶/研究报告/会话记忆中的可复用模式
- 不跳过Step 2直接委托 - 水桶分析是委托前提
- 不一次性全部域 - P0优先<=3并行
- 委托化神前检查经验库 - APPENDIX/META_LEARNING停更>7天先维护
- **F:盘写入用PowerShell + C:盘中转** — write_file工具全盘幽灵写入(声称成功但文件实际不存在)。**可靠写入方法**:
  - 小文件: `@'内容'@ | Set-Content -Path "<F盘路径>.ext" -Encoding UTF8`
  - Python脚本: `@'代码'@ | Set-Content "$env:TEMP\t.py" -Encoding UTF8; python "$env:TEMP\t.py"`
  - **大文件(推荐)**: Python写C:盘 → Copy-Item到F:盘。Python `open()` 对C:盘(Desktop/TEMP)写入可靠。
  - **验证**: 始终用 `Test-Path` 确认文件真实存在。
- 不自循环 - 完成后不自动触发第二次
- 输出不替代归墟 - 结束后必须走归墟收尾

## 归一工作流 (SSoT同步)

> 当进化涉及多端(Hermes/Trae/技能库)的同一技能时，执行归一:

```
1. 确定SSoT = 技能库 (唯一源)
2. 修改只在SSoT执行
3. 同步到Hermes skills/ + Trae skills/
4. hash验证: Get-FileHash 三端SKILL.md对比
5. 清理旧副本(备份→删除)
```

**规则**: SSoT = `<技能库>\{技能名}\SKILL.md`。Hermes/Trae是镜像，不直接编辑。

## Stale检测门控

> 每次凝魂Step 1后自动执行stale检测:

```powershell
# 门控脚本: <技能库>\_规则\stale-check.ps1
# 或Python版: <技能库>\_规则\stale检测报告.md
# 阈值: >7天 = stale
# 门控: stale>80%=CRITICAL / >50%=WARNING / <50%=HEALTHY
```

**stale处理**: CRITICAL→批量更新最老域 / WARNING→定向更新TOP3 / HEALTHY→跳过

## 模块化拆分模式

> SKILL.md > 20KB时执行模块化:

```
Step 1: 分析内容结构(段落标题/代码块/表格分布)
Step 2: 按功能域拆子模块(每个≤10KB)
  ├── SKILL.md (入口+路由+骨架, ≤10KB)
  └── modules/{功能域}.md (按需加载)
Step 3: 建立评分驱动加载策略
  composite ≥ 7.0 → 只读入口
  5.0-6.9 → +rubric模块
  3.0-4.9 → +domains+skillopt
  < 3.0 → 全量加载
Step 4: 同步三端 + hash验证
```

**已验证案例**: 化神 52KB → 9KB入口+6子模块(25KB), 日常加载降84%

## Pitfalls

- **指令库深度扫描** — `Get-ChildItem "<记忆中枢路径>/指令库/" -Directory` 只返回顶层目录,遗漏子目录内大量脚本/分镜文件(实际200+文件)。**解法**: Step 1全盘扫描时递归`-Recurse -Filter "*.md"`并按关键字二次过滤(`Select-String -Pattern "脚本|分镜|口播|文案"`),确保不遗漏子目录资源
- **PS5.1 数组追加** — `$results = @()` 报 `无法识别`，`$results += [PSCustomObject]@{...}` 报 `op_Addition`。**解法**: 用 Python 代替 PS5.1 做数据聚合。写法: `$script = @'...'@; Set-Content -Path "$env:TEMP\analysis.py" -Value $script -Encoding UTF8; python "$env:TEMP\analysis.py"`
- **PS5.1 Python format()** — `"text {:.1f}".format(val)` 在 PS5.1 中 `.format()` 被解释为 PS方法而非 Python方法。**解法**: Python脚本内用 `"{:.1f}".format(val)` 正常；PS直接输出用 `"{0}" -f $val` 格式化
- **PS5.1 `&` 运算符** — `& $scriptPath` 在 PS5.1 中被解释为后台调用而非脚本执行。**解法**: 直接内联执行脚本逻辑，不用 `&` 调用外部 .ps1
- **化神命名冲突** — `skill_view('化神')` 匹配到 2 个技能（新版 huashen + 旧版 cheat-darwin），需要传完整路径。加载前先 `skills_list` 检查重名
- **Step 2水桶分析用Python** — PS5.1的`$results=@()`和f-字符串转义极易出错，批量扫描SKILL.md元数据用Python yaml+pathlib更可靠
- **Step 2.5评分门控执行** — 化神评分必须用rubric.md的9维框架，composite公式: `Σ(维度分×权重)/100×10` (总权重为100，具体值以加载的rubric为准: Cheat产出物Rubric=100, Darwin SKILL.md Rubric=99)。**已纠正**: 旧版pitfall误写为/90，实际化神rubric总权重为100。
- **Ollama统一模型策略** — qwen3.5:9b(6.5GB)=文本理解/生成类, lfm2.5(5.2GB,208tok/s)=轻量快速类, minicpm-v4.6(1.9GB)=视觉专用。三模型总VRAM≈13.4GB, RTX 4080S 16GB够用
- **Hermes文件锁** — Hermes进程运行时`skills/`目录下的SKILL.md被锁,无法Copy-Item覆盖。**解法**: 等重启时自然生效,或改写源文件而非目标
- **后台进程环境不兼容** — `terminal(background=true)` 实际运行在Linux环境而非Windows PowerShell。表现: `python`命令不存在(需`python3`), Playwright/browser-use等Windows包不可用。**影响**: 所有Python+Playwright/browser-use/FireCrawl CLI的长时间任务必须用前台模式。**安全模式**: foreground + timeout=300-600s, 中间有条目的搜索任务完全够用。
- **路径引用审计** — SKILL.md中本地路径引用经常过时(目录重构后)。**解法**: 用Python脚本批量扫描所有SKILL.md的本地路径引用,检查`os.path.exists()`,输出断裂路径清单。批量修复用`content.replace(old_path, new_path)`。参考: references/path-audit-script.md
- **安全目录迁移** — 合并/重组目录时,禁止直接Move。**解法**: ①创建暂存目录 `_staging-merge` ②Copy原目录到暂存区 ③从暂存区Copy到目标 ④验证文件数一致 ⑤删除原目录 ⑥清理暂存区。全程保留备份,验证后再删
- **Ollama统一模型策略** — RTX 4080S 16GB下,qwen3.5:9b(6.6GB)是唯一同时支持Vision+Tools+Thinking的本地模型。可统一用于Vision/Delegation/Compression三个辅助任务,减少模型切换开销。配置: auxiliary.vision+compression+delegation全部指向ollama/qwen3.5:9b
- **启动词HTML卡片修复** — 常见问题: ①重复卡片(凝魂/千面出现2次) ②域标签错误(成音标work应为media) ③版本号过时。修复方法: Python正则提取keyword+domain, 检查重复, 修正标签。用`re.findall(r'class="keyword">([^<]+)<', content)`提取所有卡片

## references

- references/ningsao-scan-paths.md - 凝魂材料扫描路径和命令
- references/evolution-fenjue-loop.md - 焚诀批量循环执行模式
- references/startup-word-audit.md - 启动词系统HTML vs 域路由审计协议
- references/delegation-pattern.md - 并行化神分析子Agent委托模式
- references/cheat-darwin-modularization-analysis.md - 化神引擎52K SKILL.md模块化拆分分析(结构分布/目标模块/加载策略/拆分优先级)
- references/path-audit-script.md - SKILL.md路径引用审计+批量修复Python脚本(旧路径映射表)
- references/frontmatter-backfill-script.md - SKILL.md frontmatter回填Python脚本+检验方法
- references/error-handling-templates.md - Error Handling批量补丁模板(3种模板+域适配表+执行统计)
- references/codex-distillation-pipeline.md - 外部Agent能力蒸馏→Skill进化管线(Codex/OpenDesign蒸馏指令→三阶段产出→化神评分→差距分析→Skill进化, 含产出模板+评分维度+差距分析模板)


# ============================================================
# 
## 子模块

| 模块 | 功能 |
|------|------|
| 功能-指令自优化 | 核心指令/路由文件受控迭代 |
| 功能-用量自优化 | 角色-指令使用频率/成功率追踪 |
| 功能-库重组 | 指令词库内部碎片归位/层级扁平 |
APPENDIX: 淬炼v1.0 Legacy Patterns (已合并)
# ============================================================
# 来源: META-淬炼 v1.0 (2026-06-23) → 已合并入进化-升仙 v1.4
# 淬炼 = 淬火+冶炼。8域扫描→水桶短板→化神评分→SKILLOPT→自闭环→复盘
# 以下为淬炼v1.0独有模式，补充进化-升仙主流程

## A1. 淬炼命名来源
"淬炼"——淬火+冶炼。将整个系统投入火中烧红、锤打去杂质、冷水淬火定型。
对应：扫描全盘(看)→水桶效应(找缺陷)→优化(锤打)→定型(进化)，一气呵成。
比"进化"更中式——进化是日制汉语/西式概念，淬炼是传统锻造工艺意象。

## A2. 自检清单 (淬炼v1.0)
- [ ] Phase 0：千面专家是否已加载？
- [ ] Phase 1：8大域是否全部扫描？
- [ ] Phase 2：每个域的7层指标是否都打了分？
- [ ] Phase 3：8维评分是否都有具体evidence？
- [ ] Phase 4：composite < 7.0 的skill是否全部修复？
- [ ] Phase 5：三通道记忆是否全部写入？
- [ ] Phase 6：复盘报告是否完整输出？
- [ ] 不存在路径硬编码
- [ ] 输出不依赖对话上下文（可独立使用）

## A3. 依赖工具链
- 千面(SKILL:千面) — 专家匹配
- 化神(SKILL:化神) — 评分/复盘
- SKILLOPT(DEV-SkillOpt) — skill进化
- 熔锻(SKILL:熔锻) — 知识蒸馏/归档（Phase 5用）
- 归墟(SKILL:归墟) — 会话结束同步
- 凝魂(SKILL:凝魂) — 记忆三通道写入

## A4. 常见陷阱 (淬炼v1.0补充)
1. **遗漏资源域** — 只扫描了5-6个域就以为完整。必须检查全部8域
2. **水桶打分无证据** — 给域打分时只说"不太好"没有具体文件级的evidence
3. **化神评分和Phase 2脱节** — 化神评分不引用水桶效应的结果
4. **跳过SKILLOPT** — 发现了低分skill但手动修复不走ReflACT管线
5. **不更新rubric** — 进化完不更新化神评估标准，下次还按旧标准评

## A5. 独立使用约束
淬炼不依赖对话上下文，可独立使用。每次淬炼后不自动触发第二次。
淬炼输出不替代归墟流程——淬炼结束后必须走归墟收尾。

## 边界说明：进化 vs 化神

| 技能 | 职责 | 何时用 |
|------|------|--------|
| **进化/升仙** (本文件) | **系统体检+短板修复** — 8域全量扫描→水桶分析→分派修复→凝魂复盘 | 定期（每周）全盘体检，发现短板分配修复 |
| **化神** | **质量评分** — 对单个产出物/SKILL.md打分（9维rubric） | 日常评分：产出后立即评分，≥7.0放过，<7.0触发修复 |

**协作**: 进化Step3调用化神作为评分门控(≥7.0跳过); 化神诊断出系统性问题时触发进化进行全盘体检。

## OM集成 — 多Agent协作记忆

升仙的进化结果需写入OM供编排器/化神/归一读取。

### 进化完成时写入
```powershell
$summary = "[升仙] {轮次} | 扫描域: {域清单} | 短板: {TOP3短板} | 修复: {已修复/待跟进} | $(Get-Date -Format 'yyyy-MM-dd')"
$body = @{content=$summary; tags=@("domain:elevation", "source:升仙", "scope:global")} | ConvertTo-Json
Invoke-RestMethod -Uri "http://localhost:8080/memory/add" -Method Post -Body $body -ContentType "application/json" -Headers @{"x-api-key"=$env:OM_API_KEY}
```

### 启动时读取 (了解上次进化状态)
```powershell
$body = @{query="升仙 进化 短板"; tags=@("domain:elevation"); limit=3}
$history = Invoke-RestMethod -Uri "http://localhost:8080/memory/query" -Method Post -Body $body -ContentType "application/json" -Headers @{"x-api-key"=$env:OM_API_KEY}
```

# ============================================================
# 结束 APPENDIX: 淬炼v1.0 Legacy Patterns
# ============================================================

