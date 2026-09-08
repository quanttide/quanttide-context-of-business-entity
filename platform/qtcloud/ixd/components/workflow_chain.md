# 流程链路

## 组件设计

```
WorkflowChain
└── Horizontal (节点 + 箭头布局)
    ├── EventNode (源事件)
    │   ├── DomainLabel (销售云)
    │   ├── EventLabel (deal.closed)
    │   └── Icon (事件图标)
    ├── Arrow (连接箭头)
    │   └── ConfigIcon (点击配置数据映射)
    └── ActionNode (目标动作)
        ├── DomainLabel (商务云)
        ├── ActionLabel (创建合同)
        └── Icon (动作图标)
```

## 状态

- **已启用**：实线箭头，绿色
- **未启用**：虚线箭头，灰色
- **异常**：箭头变红，右侧显示错误图标，悬停显示异常详情
