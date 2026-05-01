# AI Travel Assistant

一个 **AI-first 的个人旅行助理 H5 项目**，使用 Vue 3 + TypeScript + Vite 构建。

项目定位不是传统的「景点展示 + 行程记录」，而是：

> 基于用户兴趣、当前位置、行程上下文和旅行记忆，持续推荐更合适的下一步选择。

## 技术栈

- Vue 3
- TypeScript
- Vite
- Vue Router
- Pinia
- SCSS
- 自研 UI 组件体系
- 自研 CSS Design Tokens
- Day.js
- lodash-es
- nanoid

不使用 Vant / Tailwind / Element Plus 等 UI 或 CSS 框架。

## 核心架构

```txt
src/
├─ app/                  # 应用入口、路由、Provider
├─ design/               # 自研设计系统：tokens、themes、mixins、reset
├─ ui/                   # 自研通用 UI 组件
├─ pages/                # 页面层
├─ modules/              # 业务模块 + AI 模块 + 推荐系统
├─ services/             # http、storage、ai-gateway 等基础服务
├─ workers/              # 推荐、地理、媒体等重计算任务
├─ config/               # app / ai / recommendation / map / upload 配置
└─ types/                # 全局类型
```

## AI-first 模块设计

```txt
modules/
├─ scenic                # 景点数据
├─ trip                  # 行程数据
├─ media                 # 图片 / 视频
├─ map                   # 地图 SDK 适配层
├─ location              # 浏览器定位能力
├─ user-profile          # 用户兴趣画像
├─ ai                    # AI 基础能力：Prompt、Gateway、任务
└─ recommendation        # 推荐系统：候选、评分、排序、理由、反馈
```

## 当前已内置的推荐场景

- 首页兴趣推荐：`home-interest`
- 景点详情相似推荐：`scenic-similar`
- 行程下一站推荐：`trip-next-stop`
- 附近推荐：`nearby`

当前 MVP 先使用 **规则评分 + 推荐理由生成**，后续再接入：

- AI Gateway
- Embedding
- 语义搜索
- 行程路线优化
- 多模态旅行记忆

## 开发命令

```bash
pnpm install
pnpm dev
pnpm build
pnpm preview
pnpm typecheck
```

## 推荐系统核心思想

不把所有数据一股脑丢给大模型，而是拆成：

```txt
候选集 Candidate
  ↓
特征评分 Feature Scoring
  ↓
排序 Ranking
  ↓
推荐理由 Explanation
  ↓
用户反馈 Feedback
  ↓
用户画像更新 Profile Update
```

这样推荐更稳定、更可解释，也更适合个人项目逐步演进。
