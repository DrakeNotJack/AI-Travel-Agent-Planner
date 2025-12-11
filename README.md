# Multi-Agent Trip Planner - Enhancement Roadmap / 多智能体旅行规划器 - 增强路线图

## 🚀 Project Overview / 项目概述

本项目为对 DataWhale 多智能体旅行规划项目的复现，并在此基础上完成了 API 替换与环境配置。本路线图展示我在复现过程中识别的系统限制，并基于实际需求设计的未来增强方向（这些为计划功能，并非当前能力）。

This project is a reproduction and extension of DataWhale’s multi-agent trip planner. I reconfigured the environment, replaced APIs (e.g., integrating Amap POI/hotel search), and successfully deployed a functional multi-agent itinerary planner. Below is the enhancement roadmap based on limitations observed during reproduction. These features represent future possibilities rather than current capabilities.


---
## 1. 🧰 Tool Expansion / 工具扩展

### ✅ Completed / 已完成

- 集成 高德地图 POI + 酒店 API

- Integrated Amap POI + hotel search API as replacement data source

### 🔧 Planned / 计划增强

- 

  - 

- Flight search API (Skyscanner / Kiwi) / 航班搜索（集成Skyscanner/Kiwi等API）

- Transportation time estimation / 交通时间预估

  - 当前高德 POI API 不提供两个景点间的交通时间

    - Amap POI API lacks travel-time data between attractions

  - 可通过高德路线规划 API 或 Google Distance Matrix 实现

    - Implementation via Amap Route-Planning API or Google Distance Matrix


---
## 2. 🧭 Constraint-Aware Planning / 约束感知规划（部分支持）

### ✅ Currently supported / 当前支持

- 用户可删除不喜欢的景点 / Users can delete disliked POIs

- 景点顺序可手动调整 / Manual reordering supported

- 景点游览时长可编辑 / Visit duration editable

### 🔧 Planned Enhancements / 计划增强

- 删除后自动重新平衡行程（补充景点、调节节奏） / Dynamic rebalancing after POI deletion (replace or adjust pacing)

- 支持预算（budget）约束 / Budget constraints

- 支持时间窗口（time window）约束 / Time-window constraints

- 支持旅行节奏（slow / balanced / packed） / Travel pace control

- 考虑每日天气自动安排 / Integrate daily weather into planning


---
## 3. 🔍 Critic Agent (Self-Evaluation Loop) / 自检智能体

引入一个 reviewer agent 对行程进行合理性校验。 / Introduce a reviewer agent that checks itinerary validity.

### 📋 Planned capabilities / 计划功能

- 行程可行性检查 / Feasibility check

- 地理位置排序合理性 / Geographic coherence

- 时间冲突检测 / Time conflict detection

- 预算超支检查 / Budget violation detection

- 基于交通时间的现实性判断 / Realism check based on travel-time estimation


---
## 4. 🔄 Interactive Re-planning / 交互式再规划

让用户的反馈触发自动调整。 / Enable users to refine itinerary through feedback-driven updates.

### 📋 Core Features / 核心功能

The agent supports dynamic re-planning based on natural-language feedback or user edits. Users mainly interact through a simple text input box, with optional shortcut buttons to pre-fill common feedback phrases.

智能体支持基于自然语言反馈或用户编辑的动态再规划。用户主要通过一个对话框输入反馈，并可选地使用一些快捷按钮来快速填充常见反馈内容。

智能体支持基于自然语言反馈或用户编辑的动态再规划。
 用户主要通过一个对话框输入反馈，并可选地使用一些快捷按钮来快速填充常见反馈内容。

#### Feedback-driven adjustments / 基于反馈的自动调整

Examples / 示例：

Examples 示例：

- "Too expensive." → suggest cheaper hotels/POIs

- "太贵了" → 推荐更便宜的酒店或景点

- "Too rushed." → reduce POIs / add buffer time

- "太赶了" → 减少景点或增加缓冲时间

- "I don’t want so many museums." → shift categories

- "不想看那么多博物馆" → 自动调整类别比例

Mechanism / 机制：

Natural-language feedback → LLM intent extraction → update constraints → regenerate itinerary.

自然语言反馈 → LLM 解析 → 更新约束 → 自动再规划。

 Natural-language feedback → LLM intent extraction → update constraints → regenerate itinerary.

 自然语言反馈 → LLM 解析 → 更新约束 → 自动再规划。

#### User edits (Delete / Modify / Add) / 用户编辑（删除 / 修改 / 新增）

All edit actions trigger automatic re-planning.

所有编辑行为都会触发自动再规划。

All edit actions trigger automatic re-planning.

 所有编辑行为都会触发自动再规划。

- ✔ Delete / 删除

  Remove a POI → system rebalances the day's plan.

  删除景点 → 系统自动调整当日行程。

Remove a POI → system rebalances the day's plan.

 删除景点 → 系统自动调整当日行程。

- ✔ Modify / 修改

  Change order or duration → system recalculates the timeline.

  调整顺序或停留时间 → 系统重新计算时间轴。

Change order or duration → system recalculates the timeline.

 调整顺序或停留时间 → 系统重新计算时间轴。

- ✔ Add / 新增

  Triggered via natural-language ("I want to visit X", "Add more food places").

  通过自然语言触发（如“我想去某某地方”“多加一些吃的地方”）。

Triggered via natural-language (“I want to visit X”, “Add more food places”).

通过自然语言触发（如“我想去某某地方”“多加一些吃的地方”）。

Mechanism / 机制：

Intent extraction → POI search → optimal insertion → recalc route & timing

解析新增意图 → 搜索 POI → 插入最佳位置 → 重算路线与时间。

 Intent extraction → POI search → optimal insertion → recalc route & timing

 解析新增意图 → 搜索 POI → 插入最佳位置 → 重算路线与时间。


---
## 5. 💾 Persistent Memory (Optional) / 持久化偏好记忆（可选）

虽然非原项目能力，但可作为未来增强方向。 / Not part of the original project, but a valuable optional enhancement.

### 📋 Future possibilities / 未来可能功能

- 记住用户偏好的旅行节奏、预算范围 / Remember travel pace + budget preferences

- 记录用户不喜欢的景点类别 / Track disliked categories

- 跨会话个性化推荐 / Enable cross-session personalization


---
---

📅 Last Updated / 最后更新: 2025-12-11
