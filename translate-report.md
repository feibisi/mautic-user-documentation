# Mautic 用户文档翻译 — 全量完成报告

## 概况

- **项目**: Mautic User Documentation (branch 7.1)
- **阶段**: Phase 1 + Phase 2 — 全章节 (20 个目录 + index.rst)
- **总文件数**: 84 个 RST 文件
- **总词数**: ~79,400 词 (Phase 1: ~33,800 + Phase 2: ~45,600)
- **翻译引擎**: Claude (主线程 + 并行 subagent)
- **完成时间**: 2026-06-24

## 文件清单

### Phase 1 (23 文件) — 已完成

| 章节 | 文件 | 状态 |
|------|------|------|
| getting_started | how_to_install_mautic.rst | ✅ |
| getting_started | how_to_update_mautic.rst | ✅ |
| getting_started | switching_composer.rst | ✅ |
| contacts | contacts_overview.rst | ✅ |
| contacts | custom_fields.rst | ✅ |
| contacts | frequency_rules.rst | ✅ |
| contacts | import_contacts.rst | ✅ |
| contacts | manage_contacts.rst | ✅ |
| contacts | preference_center.rst | ✅ |
| contacts | tags.rst | ✅ |
| campaigns | campaign_builder.rst | ✅ |
| campaigns | campaigns_overview.rst | ✅ |
| campaigns | creating_campaigns.rst | ✅ |
| campaigns | managing_campaigns.rst | ✅ |
| campaigns | troubleshooting_campaigns.rst | ✅ |
| configuration | command_line_interface.rst | ✅ |
| configuration | cron_jobs.rst | ✅ |
| configuration | maxmind_license.rst | ✅ |
| configuration | settings.rst | ✅ |
| configuration | shortener.rst | ✅ |
| configuration | smime_email_signing.rst | ✅ |
| configuration | tracking_script.rst | ✅ |
| configuration | variables.rst | ✅ |

### Phase 2 (61 文件) — 本次完成

| 章节 | 文件数 | 状态 |
|------|--------|------|
| authentication | 1 | ✅ |
| builders | 2 | ✅ |
| categories | 1 | ✅ |
| channels | 8 | ✅ |
| companies | 1 | ✅ |
| components | 4 | ✅ |
| dashboard | 1 | ✅ |
| index.rst | 1 | ✅ |
| marketplace | 1 | ✅ |
| overview | 1 | ✅ |
| plugins | 21 | ✅ |
| points | 3 | ✅ |
| queue | 2 | ✅ |
| reports | 1 | ✅ |
| search | 1 | ✅ |
| segments | 1 | ✅ |
| stages | 1 | ✅ |
| themes | 4 | ✅ |
| translations | 1 | ✅ |
| troubleshooting | 3 | ✅ |
| users_roles | 2 | ✅ |

**总计: 84/84 文件 ✅**

## 词数统计

| 章节 | 文件数 | 原文词数 | 阶段 |
|------|--------|----------|------|
| getting_started | 3 | ~4,900 | Phase 1 |
| contacts | 7 | ~10,400 | Phase 1 |
| campaigns | 5 | ~5,400 | Phase 1 |
| configuration | 8 | ~13,200 | Phase 1 |
| components | 4 | ~9,300 | Phase 2 |
| channels | 8 | ~9,500 | Phase 2 |
| plugins | 21 | ~3,700 | Phase 2 |
| segments | 1 | ~3,700 | Phase 2 |
| reports | 1 | ~2,200 | Phase 2 |
| troubleshooting | 3 | ~3,000 | Phase 2 |
| themes | 4 | ~1,300 | Phase 2 |
| points | 3 | ~1,500 | Phase 2 |
| builders | 2 | ~1,700 | Phase 2 |
| users_roles | 2 | ~1,000 | Phase 2 |
| queue | 2 | ~800 | Phase 2 |
| 其他 (≤1 file/dir) | 10 | ~7,600 | Phase 2 |
| **总计** | **84** | **~79,400** | |

## 术语表

`term-mapping.jsonl` — 95 条 Mautic 专用术语覆盖

## 特殊 RST 指令处理

| 指令 | 处理方式 |
|------|----------|
| `.. vale on/off` | 保留不变 |
| `:ref:` | 保留不变 (Sphinx 交叉引用) |
| `:xref:` | 保留不变 |
| `:doc:` | 保留不变 |
| `.. image::` | 保留不变 (:alt: 文本也保留不变) |
| `.. note::` / `.. caution::` / `.. warning::` / `.. tip::` / `.. danger::` / `.. attention::` | 保留不变 |
| `.. code-block::` / `.. code::` | 保留不变 (代码内容也保留不变) |
| `.. list-table::` | 保留不变 |
| 标题标记 (`#####`, `******`, `~~~~~~`, `======`, `------`) | 保留不变 |
| 路径、URL、命令 | 保留不变 |
| `:width:` / `:height:` / `:align:` / `:header-rows:` / `:widths:` | 保留不变 |

## 交付物

- 翻译文件: `docs/` (84 个 RST 文件)
- 术语表: `term-mapping.jsonl` (95 条)
- 本报告: `translate-report.md`

---

*翻译自 Mautic User Documentation 7.1 分支 | 2026-06-24*
