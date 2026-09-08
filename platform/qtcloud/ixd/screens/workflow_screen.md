# 流程编排页

```
WorkflowScreen
└── Vertical
    ├── Tab (预置 / 自定义)
    ├── Tab: 预置
    │   └── 模板列表
    │       ├── 成交转化 (销售云 deal.closed → 商务云 创建合同) [启用]
    │       ├── 订单交付 (商务云 contract.signed → 资产云 准备交付) [启用]
    │       └── 开票收款 (商务云 contract.invoiced → 财务云 创建应收) [未启用]
    └── Tab: 自定义
        └── Composer
            ├── 事件节点 (从左栏拖入)
            ├── 动作节点 (从左栏拖入)
            ├── 连线 (节点间箭头)
            └── Button [保存并启用]
```
