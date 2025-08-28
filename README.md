# HuMaZE · Rime 输入方案合集

*`安装小狼毫前先clone项目，再指定用户文件夹至clone目录即可。`*

---


基于 Rime 的输入方案与配置集合，重点包含：
- 虎码官方单字（`tiger`）与虎码官方词库（`tigress`）
- 拼音++（`PY_c`）与临时英文（`easy_english`）
- 笔画（`stroke`）反查/辅助
- 多种 Lua 过滤器与工具（Unicode 显示、字符集标注、简易计算器、数字大写、时间等）

适配 Rime 家族，尤其是 Windows 版 Weasel。仓库内已包含 OpenCC 配置与丰富的符号表。

---

## 方案一览
- `tiger`：虎码官方单字，反查拼音（按 ` 键开启）。
- `tigress`：虎码官方词库版，词为主，支持与 `tiger` 相同的功能开关。
- `PY_c`：拼音++，支持造词、用户词典与历史上屏；笔画反查（反引号 ` 开启，见 schema）。
- `easy_english`：临时英文词库，输入 `'word` 触发；候选量默认 5 个。
- `stroke`：五笔画方案，可独立使用，也用于反查场景。

辅助资源与功能：
- `opencc/` 简繁转换、拼音标注、拆分过滤、表情等配置（如 `st_tu.json`、`emoji.json`、`hu_cf.json`）。
- `lua/` 常用 Lua 插件：
  - `calculator_translator.lua`：以 `=` 开头计算表达式。
  - `unicode_display.lua`：在候选备注显示 Unicode 码位（U+XXXX）。
  - `charset_comment_filter.lua`：显示字符所属 Unicode 分区。
  - `number.lua`、`shijian2.lua` 等工具类翻译器。
- `symbols.yaml`：丰富的符号/表情库，支持以 `/` 前缀检索（如 `/bq` 表情）。

---

## 主要特性
- 一键简繁开关：OpenCC 多套配置，默认采用「简→繁·异体（`st_tu.json`）」。
- 拼音/拆分/Emoji 显示过滤：候选后注展示拼音、部件拆分、表情映射等。
- 反查与混输：
  - 虎码内按反引号 ` 进入拼音反查（`reverse_lookup`）。
  - `'` 前缀进入英文（`easy_english`）。
- Unicode 信息：可开关显示候选字符的 Unicode 分区与码位。
- 实用 Lua：
  - 计算器：输入 `=1+1` 直接得到 `2`；支持函数、链式处理、lambda 语法糖。
  - 数字转大写、时间等。
- 符号面板：输入 `/` 加缩写如 `/bq`（表情）、`/sx`（数学符号）、`/xz`（星座）等。

---

## 安装与部署（Windows · Weasel）
前置：Weasel 0.17.4+（Rime 1.13+）。

1) 备份现有用户目录：`%APPDATA%\Rime`
2) 将本仓库内容复制到 `%APPDATA%\Rime`（建议排除 `build/` 与 `*.userdb/` 目录，Rime 会自行编译字典）
3) 重新部署：在输入法状态菜单选择「重新部署」或触发部署
4) 方案切换：已在 `default.custom.yaml` 预置 `Ctrl+F8` 打开方案切换器，在列表中选择「虎码官方单字」或「虎码官方词库」

如在 macOS（Squirrel）或 Linux（ibus-rime），将仓库内容放入各自的 Rime 用户目录，步骤相同。

---

## 快捷键与常用操作（默认）
以下为 `tiger`/`tigress` 中常用快捷键（可在各自 schema 中调整）：
- 候选选择：`;` 选择 2，`'` 选择 3；`-`/`=` 翻页（向后/向前）
- 清码：Tab 清空当前编码
- 反查：在虎码中按反引号 ` 后输入拼音，可见注释或反查候选
- 英文：以 `'` 前缀进入临时英文（标签【En】）
- 简繁开关：`Ctrl+O`（`simplification`）
- 拼音注开关：`Ctrl+P`（`pinyin`）
- Emoji 注开关：`Ctrl+I`（`emoji_cn`）
- Unicode 分区开关：`Ctrl+U`（`charset_comment_filter`）
- Unicode 码位开关：`Ctrl+Y`（`udpf_switch`）
- 拆分显示开关：`Ctrl+J`（`chaifen`，仅虎码/tigress）
- 中英标点切换：`Ctrl+.`（`ascii_punct`）
- 全半角切换：可在 schema 中启用 `Shift+Space`（默认注释）

符号与表达式：
- 符号检索：以 `/` 开头，如 `/bq` 表情、`/sx` 数学、`/xz` 星座等（见 `symbols.yaml`）
- 计算器：输入 `=表达式`（如 `=max({1,7,2})`）直接得到结果；支持 `\\x.x^2|` 样式的 lambda 语法糖与 `$` 链式处理

---

## 自定义与扩展
- 词典扩展：
  - `tiger.custom.yaml` 默认引入 `tiger.extended` 扩展词典
  - `tigress.custom.yaml` 默认引入 `tigress.extended` 扩展词典
- 常用开关：
  - 打开四码自动上屏：在自定义文件中取消注释 `speller/auto_select_pattern: ^;\\w+|^\\w{4}$`
  - 开启编码补全提示：取消注释 `translator/enable_completion: true`
  - 关闭分号引导：可调整 `speller/alphabet`（见自定义文件内注释）
- 主题与样式：在 `weasel.custom.yaml` 中可切换 `style/color_scheme` 与布局、字体等参数（已预置多套主题）
- Lua 插件：在 `rime.lua` 统一加载；如需增删模块，按行注释/取消注释即可

修改任意配置后，请重新部署以生效。

---

## 目录结构速览
- 根目录：schema 与词典定义（`*.schema.yaml`、`*.dict.yaml`）、定制文件（`*.custom.yaml`）、`symbols.yaml`
- `lua/`：Lua 过滤器与翻译器
- `opencc/`：OpenCC 转换配置与词表
- `build/`：Rime 部署生成与缓存（可由 Rime 自动重建）

---

## 常见问题
- 看到的候选顺序与我预期不同？
  - 词库版（`tigress`）更偏向出词；单字版（`tiger`）更偏向出字
  - 试用历史上屏与用户词典（`PY_c`/英语方案开启了用户词典）
- 简繁/注解不符合需求？
  - 切换 `Ctrl+O/P/I` 等开关；或在 schema 中替换 `opencc_config`
- 反查没有反应？
  - 确保使用了反引号键 `，并处于对应方案；查看 `recognizer/patterns`
- 无法切换方案？
  - 检查 `default.custom.yaml` 的 `schema_list` 是否包含 `tiger` 与 `tigress`

---

## 致谢
- Rime / Weasel 项目与社区
- OpenCC 简繁转换
- Lua 插件参考：
  - 计算器（calculator_translator）：baopaau/rime-lua-collection
  - Unicode 显示过滤器：Shitlime 等

如有问题或建议，欢迎提交 Issue 或 PR。