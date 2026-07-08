# LangGraph Learning

目标：

系统学习 LangGraph。

架构图：
langgraph-learning/
│
├── app/                     ⭐ 最终项目（一直演进）
│   ├── __init__.py
│   ├── main.py              # 程序入口
│   ├── graph.py             # Graph 构建
│   ├── state.py             # State 定义
│   ├── nodes.py             # 所有 Node
│   ├── router.py            # Router（Demo3开始）
│   ├── tools.py             # Tool（Demo4开始）
│   ├── memory.py            # Memory（Demo7开始）
│   ├── prompts.py           # Prompt
│   └── config.py            # 项目配置
│
├── examples/                ⭐ 每个知识点最小示例
│   ├── graph_demo.py
│   ├── 02_state.py
│   ├── 03_router.py
│   ├── 04_tool.py
│   └── ...
│
├── shared/                  ⭐ 公共工具
│   ├── __init__.py
│   ├── llm.py
│   └── utils.py
│
├── docs/                    ⭐ 学习笔记
│   ├── 01-Graph.md
│   ├── 02-State.md
│   └── ...
│
├── tests/
│
├── .env
├── .gitignore
├── pyproject.toml
├── README.md
└── uv.lock

学习顺序：

- Demo01 Graph
- Demo02 State
- Demo03 Router
- Demo04 Tool
- Demo05 Messages
- Demo06 Stream
- Demo07 Checkpoint
- Demo08 Interrupt
- Demo09 Planner
- Demo10 Multi-Agent
- Demo11 Memory
- Demo12 Debug
