# Illustrator Isometric Architecture

面向 Codex 的建筑轴测与关系工作流 Skill：从照片、网页、地图到可编辑的 Illustrator 路径、节点组和建筑关系图。

![合成几何示例](assets/geometry-demo.svg)

上图仅展示投影、底座和连接带的合成几何，不是任何真实建筑的复原成果。

## 能做什么

- 单体系列：统一底座、真实形体、正等轴测、无阴影矢量插画。
- 多节点工作流：真实方位优先、完整节点成组、层级与材质配色、两行带上工作流。
- 几何校核：实际带宽交叠、走线方向、文字出带、字间碰撞与已声明方位约束。
- Illustrator 交付：原生 AI、可编辑 SVG、PNG；打印场景可加 PDF。

## 安装与使用

把本目录整体放到 Codex 的 skills 目录，保持目录名 `illustrator-isometric-architecture`，重启或刷新宿主的 Skill 发现机制。主入口为 [SKILL.md](SKILL.md)。

示例请求：

> 使用 $illustrator-isometric-architecture，把这些建筑照片画成统一底座的可编辑轴测图。形体保留，无阴影；不确定部分另列说明。

> 使用 $illustrator-isometric-architecture，在已打开的 Illustrator 中重排建筑关系图。保持核心四至，节点逐个成组，连接带不交叠，文字仅放 XY 斜向段，右侧列出颜色图例。

需要运行中的 Adobe Illustrator、可用且已获授权的 Illustrator MCP，以及资料查阅能力。此包不附带 Illustrator、MCP 服务、访问令牌或自动连接配置。实际工具名和参数以当前 MCP 提供的能力为准。

## 几何工具

校核工具使用 Python 3.10+ 与 Shapely，不需要 NumPy、字体文件或网络请求。

```bash
python -m pip install -r requirements.txt
python scripts/isometric_geometry.py demo --output assets/geometry-demo.svg --manifest examples/demo-manifest.json
python scripts/isometric_geometry.py audit examples/demo-manifest.json --report validation-report.json
python -m unittest discover -s tests -v
```

已有 Python 环境满足依赖时直接使用，无需重复安装。SVG 中的文本保持文字元素；字体使用宿主已有字体，不打包商业字体。

脚本只检查输入清单描述的几何，不能自动读取 AI 的全部内部结构、核实照片、识别真实地理位置或保证路由存在。交付前仍须按 Skill 在 Illustrator 中核验最终文件。

## 文件结构

```text
SKILL.md                         Skill 入口
agents/openai.yaml               Codex 显示信息
references/                     按模式读取的工作规则
assets/palette.json              可修改的配色预设
assets/geometry-demo.svg          自制合成示例
scripts/isometric_geometry.py    投影、带面构造与几何校核
examples/demo-manifest.json      合成示例几何清单
tests/test_geometry.py           几何行为测试
```

## 分享范围

本包将多轮建筑绘制和排版经验提炼为通用流程，未附带真实课程文件、原始对话、个人信息、来源照片、商业字体、API 密钥或项目专用坐标。配色参考建筑信息图的色彩方向，非 Sasaki 官方色卡。

本地打包不等于已上传 GitHub；仓库名称、公开范围和许可证由发布者选择。本包未预设开源许可证。
