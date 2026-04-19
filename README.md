# action-setup-claude

用于在 CI 中安装 Claude CLI，并可选注入 Anthropic 相关环境变量。

## 功能

- 缓存 Claude CLI 二进制和数据目录，减少重复安装耗时
- 可选写入 `ANTHROPIC_*` 环境变量
- 将 `~/.local/bin` 加入 `PATH`
- 输出已安装的 Claude CLI 版本号
- 缓存用户侧 Claude 配置目录

## 输入参数

| 名称 | 必填 | 说明 |
| --- | --- | --- |
| `base-url` | 否 | Anthropic API 的 Base URL |
| `auth-token` | 否 | Claude 请求使用的鉴权 Token |
| `model` | 否 | Claude 请求使用的模型名 |

## 输出参数

| 名称 | 说明 |
| --- | --- |
| `version` | 安装后的 Claude CLI 版本号 |

## 使用示例

```yaml
name: ci

on:
  push:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Claude CLI
        uses: seepine/action-setup-claude@v1
        with:
          base-url: ${{ secrets.ANTHROPIC_BASE_URL }}
          auth-token: ${{ secrets.ANTHROPIC_AUTH_TOKEN }}
          model: ${{ secrets.ANTHROPIC_MODEL }}

      - name: Claude version
        run: claude -v
```
