# 量潮科技工作语境

量潮科技的**工作语境**——其他仓库的草稿箱：内容先在这里起草，定稿后归入真正归属的仓库与分层。

近期草稿的主线汇总见 [index.md](index.md)。

## 结构

按板块建目录，板块内按分层建子目录。

```
context/
├── default/      # 通用——面向所有业务线
├── qtadmin/      # 量潮管理
├── qtclass/      # 量潮课堂
├── qtcloud/      # 量潮云
├── qtconsult/    # 量潮咨询
└── qtdata/       # 量潮数据
```

分层子目录与归属仓库同名：`insight/` → `data/insight/`、`intention/` → `data/intention/`、`journal/`、`brochure/`。

## 归位

草稿按板块归拢，定稿按分层归位，两者的轴向相反：

```
草稿：context/{板块}/{分层}/…
定稿：data/{分层}/{板块}/…
```

## 边界

- **不是事实源**——查权威口径去归属仓库（`data/insight/`、`data/intention/` 或各领域/业务仓库），不在这里
- 默认板块为 `default`
