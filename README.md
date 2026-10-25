# OpenNLP

小组用于 **记录与保存实验数据、保证可复现** 的 GitHub 仓库，服务于 NLP 课程大项目：参加 **SemEval-2027 Task 1 RETECO（Reasoning-Oriented Retrieval，推理导向检索）**，主攻 **Track 1a 时序检索**。

- 仓库地址：https://github.com/runlin1113/OpenNLP
- 任务指标：nDCG@10（pytrec_eval，13 领域宏平均）；官方 BM25 基线 dev = 0.0967
- 评测期：2027-01-10 ~ 2027-01-31（仅 21 天）

---

## 一、小组任务（三路并行，5 人 / 1+2+2）

| 分组 | 人数 | 核心交付 | 验收线 | 计划板 ID |
|---|---|---|---|---|
| 基线复现组 | 1 | 评测流水线（pytrec_eval, 13 领域宏平均）+ BM25 基线复现 + 数据统计表 | dev nDCG@10 与官方 0.0967 误差 ≤ 0.01 | `rkv89x` |
| 顶会复现组 | 2 | MRAG 复现 + ReasonIR 跑通 + ≥6 篇笔记 + 复现对比表 | 各出 1 个 dev 可复现数字，对齐基线流水线 | `r5fjUn` |
| 课内方法组 | 2 | 课内方法盘点表 + 从零 BM25 + 词向量检索对照 | 从零 BM25 与库实现误差 ≤ 0.01 | `rvB4KG` |

详细定义、通用流程、数据链接与文献范围见本仓库 **`方法手册.md`**。

---

## 二、目录结构（避免互相覆盖）

```
OpenNLP/
├── README.md          # 本说明
├── 方法手册.md         # 任务定义 / 流程 / 数据链接 / 文献范围 / 复现规范
├── showcase.html      # 文献调研静态网页（10 篇，卡片墙 + 单篇五问视图）
├── docs/              # 开题/结题报告源文件（ACL/ICLR 模板）
├── data/              # 数据校验脚本与统计表（不提交原始大语料）
├── baseline/          # 基线复现组：评测流水线 + BM25
├── reproduce/         # 顶会复现组：MRAG / ReasonIR / 笔记 / 对比表
├── inclass/           # 课内方法组：从零 BM25 / 词向量检索
├── results/           # 各方法 run 文件与 nDCG@10 评分结果
└── requirements.txt   # 统一依赖
```

> 每个子组**只在自己的目录内工作**，互不触碰他人目录，从根上避免覆盖。

---

## 三、协作与防冲突 / 防覆盖规范（强制）

1. **禁止直接 push 到 `main`**：在个人分支（如 `feat/baseline-张三`）开发，经 PR + 至少 1 人 review 后合并。
2. **提交前先 `git pull --rebase`**：保持与远端同步，避免非快进冲突。
3. **不 `force push`**：任何情况下不得 `--force`，历史不可覆盖。
4. **大文件外链**：原始语料（RETECO 约 116 万文档）**不入库**，改用 HF 下载脚本；图片/模型权重用 Git LFS 或对象存储外链。
5. **文件名加前缀**：实验产物命名带 `日期_作者_方法` 前缀（如 `20261101_lin_bm25_dev.json`），避免同名覆盖。
6. **可复现三件套**：每次结果提交附带 随机种子 / 配置文件 / 环境（`requirements.txt` + 提交哈希）。
7. **冲突处理**：出现冲突由相关子组协商解决，禁止"用自己版本直接覆盖对方"。

---

## 四、官方资源

- 任务主页（CFP / 规则）：https://datascienceuibk.github.io/RETECO/
- 官方数据集（HF）：https://huggingface.co/datasets/DataScience-UIBK/RETECO-SemEval2027
- 官方代码：https://github.com/DataScienceUIBK/RETECO
- 官方邮件组：https://groups.google.com/g/semeval-2027-reteco

---

## 五、文献调研静态网页

`showcase.html` 为本项目 10 篇关键文献的调研展示（卡片墙 + 单篇五问阅读视图，单文件零依赖）。
- 本地：双击打开即可。
- 在线：在仓库 **Settings → Pages** 选择 `main` 分支根目录，开启 GitHub Pages 后获得公开 URL。

---

## 六、如何复现（速览）

```bash
# 1. 安装依赖
pip install -r requirements.txt
# 2. 拉取官方数据（见 data/ 下载脚本，不入库大语料）
# 3. 跑评测流水线（基线组提供）
python baseline/eval_pipeline.py --run results/bm25_dev.json
# 4. 计算 nDCG@10（13 领域宏平均）
python baseline/score.py --qrels data/dev.qrels --run results/bm25_dev.json
```
