## uv 

用途

- python 版本管理
- 脚本运行
- 初始化项目
- 项目依赖管理

应用安装方式

win 上：

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Mac 或 Linux 

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
# 或者是
wget -qO- https://astral.sh/uv/install.sh | sh
```

### 版本管理

- `uv python install 3.12` 安装 python 版本
- `uv python list` 查看可用的 python 版本
- `uv python uninstall` 移除指定版本的 python

### 项目管理

使用 `pyproject.toml` 创建以及运行项目

- `uv run` 运行脚本
- `uv init` 初始化项目
- `uv add` 添加依赖
- `uv remove` 移除依赖
- `uv sync` 使用 environment 同步项目依赖
- `uv lock` 为依赖创建一个 lock file









