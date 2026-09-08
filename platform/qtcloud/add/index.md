# 协作目录架构

## 定位

协作目录是跨域协作的**设计时系统**，不参与运行时事件传输。它管理三件事：事件注册、契约版本、流程编排。运行时由各域本地的事件总线和 Outbox 机制处理（参见主仓库 `docs/add/intro/domain_events.md`）。

## 核心抽象

```
Event  — 一个域发出的信号
  ├── type:        "com.qtcloud.sales.deal.closed"
  ├── source:      "qtcloud.sales"
  ├── schema:      CloudEvents 格式 + 字段定义
  └── status:      active | deprecated

Contract — Event + 订阅关系 + 版本
  ├── event:       关联 Event
  ├── subscribers: 订阅此事件的域列表
  ├── versions:    schema 版本历史
  └── status:      active | change_pending | superseded

Workflow — 跨域流程定义
  ├── steps:       事件 → 目标域 + 动作
  ├── template:    preset | custom
  └── status:      enabled | disabled
```

三者关系：一个 **Event** 被消费时产生一个 **Contract**（绑定事件和订阅方），多个 **Contract** 串联成一个 **Workflow**。

## 设计时 vs 运行时

协作目录只参与设计时：

```
设计时（协作目录）                         运行时（域平台）
                                
注册 Event                            发布 Event（Outbox → 事件总线）
订阅 Contract                         消费 Event（事件总线 → 本地处理）
编排 Workflow                         触发 Action（按 Workflow 映射）
管理版本变更                           稳定运行，不依赖目录
```

协作目录离线不影响任何正在运行的跨域流程。目录只负责"告诉你怎么连"，不负责"替你跑"。

## 关键流程

### 跨域工作流例子

一个典型的"签单→交付"流程涉及协作目录的哪些部分：

```
1. 销售云团队在协作目录注册 event: sales.deal.closed
2. 商务云团队发现该事件，订阅，形成 contract
3. 业务负责人在协作目录启用 preset workflow "成交转化"
4. 目录生成配置下发到各域：商务云订阅 sales.deal.closed，映射字段
5. 运行时：销售云发布事件 → 事件总线 → 商务云接收 → 创建合同
```

步骤 1-4 在协作目录完成（设计时），步骤 5 在各域完成（运行时）。

### 契约变更流程

```
1. 销售云提交 sales.deal.closed 的 schema 变更
2. 目录锁定当前版本，新建 pending 版本
3. 目录通知所有订阅方（商务云、资产云）
4. 订阅方确认或拒绝
5. 全部确认 → 新版本上线；任一拒绝 → 变更挂起，发起方协调
6. 变更期间运行时继续用旧版本，不断流
```

## 存储模型

```
events:
  id, type, source, schema_json, status, created_at

contracts:
  id, event_id, subscriber_domain, mapping_json, status, created_at

contract_versions:
  id, contract_id, schema_json, change_log, status, confirmed_by

workflows:
  id, name, type, steps_json, status, enabled_at
```

采用 document 视图存储 schema（JSON），不单独为字段建表。版本对比在前端 Diff 组件完成。
