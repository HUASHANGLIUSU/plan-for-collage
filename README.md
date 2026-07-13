# 大学生成长规划

> 本地优先的大学生成长规划桌面应用：在一个界面中管理目标、周计划、课程笔记、竞赛信息与成长复盘。

`大学生成长规划` 是一个使用 **Python + PySide6 + SQLite** 构建的本地桌面应用。它将学习任务、长期目标、课程资料和竞赛安排连接起来，帮助学生持续记录、执行与复盘自己的成长计划。

## 功能一览

- **概览仪表盘**：集中查看今日任务、本周完成率、重点目标、今日课程及待确认的竞赛更新。
- **目标树**：按“长期目标 → 阶段目标 → 任务”维护可编辑的层级目标，支持搜索、编辑与删除。
- **周计划**：以 ISO 周为单位生成七天任务板，记录任务状态与执行备注。
- **课程笔记**：维护固定周课表，为每门课保存课程汇总和按日期归档的 Markdown 课堂笔记。
- **竞赛库**：内置竞赛种子数据；可在后台检查官网日期，人工确认后将竞赛加入目标树。
- **成长报告**：生成并保存周报、月报，支持预览和复制飞书兼容 Markdown。

## 技术栈

- Python 3.11+
- PySide6
- SQLite
- Requests + Beautiful Soup 4（竞赛官网信息检查）
- Pytest

## 快速开始

### 1. 获取代码

```powershell
git clone <你的仓库地址>
cd 计划软件实现
```

### 2. 安装依赖

建议先创建虚拟环境：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
```

### 3. 启动应用

```powershell
python -m student_planner.main
```

首次运行会自动在当前工作目录创建本地数据库：`data/student_planner.db`。

## 测试

```powershell
# 运行全部测试
python -m pytest -q

# 运行界面冒烟测试
python -m pytest tests/ui/test_layout_smoke.py -q

# 静态编译检查
python -m compileall src tests
```

## 项目结构

```text
src/student_planner/
├── main.py              # 应用入口
├── db.py                # SQLite 初始化
├── repositories.py      # 数据访问层
├── services.py          # 目标、周计划、报告等业务服务
├── competitions.py      # 竞赛数据与官网检查服务
└── ui/
    ├── main_window.py   # 主窗口与页面导航
    ├── theme.py         # 全局视觉主题
    └── pages/           # 概览、目标树、周计划等页面
tests/                   # 单元测试与 UI 测试
```

## 数据与隐私

- 所有计划、课程与报告数据默认仅保存在本机 SQLite 数据库中。
- 应用不需要账号，也不包含云同步功能。
- 只有在用户主动检查竞赛官网时，应用才会发起网络请求。

## 当前限制

- 课程表采用固定周课表，暂不处理教学周、单双周和调休。
- 竞赛日期检查结果需人工确认后才会写入正式数据。
- 目前不提供多设备同步与移动端支持。


