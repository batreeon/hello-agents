1. 开了vpn拉github仓库还是很慢
    需要配置代理，假设代理端口是7890:
    https:
    ```bash
    git config --global https.proxy http://127.0.0.1:7890
    ```
    ssh，在~/.ssh/config中新增：
    ```bash
    Host github.com
    User git
    ProxyCommand connect -S 127.0.0.1:7890 %h %p
    ```

2. uv初始化项目：
    ```bash
    uv init -p 3.14
    uv venv -p 3.14 这个相比上面的init不会创建pyproject.toml
    ```

    配置镜像源：
    全局，在~/.config/uv/uv.toml中添加：
    ```bash
    [[index]]
    url = "https://pypi.tuna.tsinghua.edu.cn/simple"
    default = true
    ```
    项目，在pyproject.toml中添加：
    ```bash
    [tool.uv]
    [[tool.uv.index]]
    url = "https://pypi.tuna.tsinghua.edu.cn/simple"
    default = true
    ```
    临时：
    ```bash
    uv add numpy --index-url https://pypi.tuna.tsinghua.edu.cn/simple
    ```