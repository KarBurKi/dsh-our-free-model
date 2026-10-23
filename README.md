# dsh-our-free-model（OFM）

给 DSH（DeepSeek Harness）的**模型车道聚合插件**：装上即用，无需在插件里填 API Key，就能走匿名免费车道；
桌面端另有 EAC 协付渠道。2.0 起把 LobsterAI、Qoder（含中国版）、TRAE、Cline、Loomy、Raccoon、
MiniMax、ZCode、Gemini 十个账号渠道接进来，提供登录、账号池、积分领取、
模型黑名单与本地 OpenAI 网关、局域网转发、数据看板与运行日志，六页毛玻璃界面统一呈现。

> 个人自用 / 私有仓库。不是官方项目，不保证对他人可用。

## 安装

```sh
git clone <this-repo> ~/.dsh/plugins/dsh-our-free-model
```

再在 DSH profile 里以 `link:` 挂载：

- `dependencies`: `"dsh-our-free-model": "link:C:/Users/<you>/.dsh/plugins/dsh-our-free-model"`
- `dsh.profile.bundles`: 追加 `dsh-our-free-model`
- `pnpm-lock.yaml` 的 importers 段补 `specifier` / `version: link:../../plugins/dsh-our-free-model`
- `node_modules` 下建 junction 指向插件目录

改完**重启桌面端**。

## 结构

| 路径 | 说明 |
|---|---|
| `index.js` / `client.js` | Host 半 / Browser 半 |
| `src/` | 车道路由、账号池、EAC、转发、看板、更新器 |
| `adapter/` | 适配层 |
| `catalog/` | 模型目录 |
| `feed/` | 上游信息流 |
| `worker/` | 独立 Worker fiber |
| `locale/` | 多语言 |
| `scripts/` | 构建与测试脚本（110 个，测试用假 key，不含真实凭据） |
| `vendor/channel-pack/` | 十三渠道上游包（见下方致谢），运行时加载 `pack.js` |
| `docs/` | 发布、验证、issue 记录 |

## 数据

运行时状态写在 `~/.dsh/our-free-model/`（账号池、积分、日志），**不在本仓库**。

## 致谢与许可

- 本项目：MIT（见 `LICENSE`）。
- `vendor/channel-pack/` 是 [dsh-codearts-auth](https://gitee.com/iJetLi/deepseek-harness-codearts) 的完整拷贝
  （MIT），吸收了上游提交 `345f0a07`（2026-10-06），目录名与内部标识符改为 `channel-pack`；
  出处、许可证与 `NOTICE.md` 均保留在 `vendor/channel-pack/` 下。
