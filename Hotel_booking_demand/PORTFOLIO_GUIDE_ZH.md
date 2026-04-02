# Hotel Booking Demand Portfolio 实战指南

## 1. 这个项目为什么适合你

你有酒店管理和电商运营背景，这个数据集非常适合作为你的 portfolio 项目，因为它同时包含：

- 酒店业务问题：取消预订、入住需求、客户类型、渠道表现
- 运营分析问题：转化质量、预订提前期、客户行为、需求波动
- 可展示的分析能力：数据清洗、EDA、特征构造、业务洞察、行动建议

这个项目不要只做成“画几个图”。你的目标应该是：

**像真实业务分析师一样，从业务问题出发，清洗数据，解释现象，提出建议，并把整个过程讲清楚。**

---

## 2. 建议你把项目目标定成什么

建议主问题：

**什么因素会影响酒店预订取消率，以及酒店应该如何优化预订质量和运营策略？**

你也可以增加两个副问题：

- 哪些客户和渠道带来的订单质量更高？
- 不同酒店类型（City Hotel vs Resort Hotel）的需求模式有什么差异？

这样你的项目就不只是描述数据，而是有明确业务目标。

---

## 3. 真实数据分析项目的完整流程

你可以按下面 8 个阶段做。

### 阶段 1：Business Understanding

先不要急着写代码，先写清楚这 4 件事：

- 业务背景是什么？
- 业务方真正关心什么？
- 成功的分析结果应该帮助谁做决定？
- 你最终想交付什么？

对于这个项目，你可以这样写：

- 场景：酒店存在预订取消和需求波动问题
- 业务影响：取消率高会影响入住率、收入预测、人员安排和营销投放
- 分析目标：识别取消预订的关键因素，找出高价值客户和高风险渠道
- 交付结果：数据清洗过程、探索性分析、核心洞察、业务建议、可视化结论

### 阶段 2：Data Understanding

这一阶段你要回答：

- 数据有多少行、多少列？
- 每列是什么意思？
- 哪些是数值变量，哪些是类别变量，哪些是日期变量？
- 哪些字段可能存在数据质量问题？

你当前的数据概况：

- 文件：`Hotel_booking_demand/data/hotel_bookings.csv`
- 行数：119,390
- 列数：32

你先重点理解这些字段：

- `is_canceled`：是否取消，是核心目标变量
- `lead_time`：预订提前期，通常和取消率强相关
- `hotel`：城市酒店还是度假酒店
- `market_segment`：客户来源细分
- `distribution_channel`：分销渠道
- `customer_type`：客户类型
- `adr`：平均日房价
- `deposit_type`：押金类型
- `previous_cancellations`：历史取消次数
- `total_of_special_requests`：特殊需求数量
- `reservation_status_date`：预订状态日期

### 阶段 3：Data Cleaning

真实项目里，这一步非常重要。

你要重点检查：

- 缺失值
- 异常值
- 重复值
- 数据类型错误
- 不合理记录
- 文本中的伪缺失值

这个数据集有一个常见问题：

- 一些字段会用字符串 `NULL` 表示缺失，而不是真正的空值

你要特别检查：

- `agent`
- `company`
- `country`
- `children`

还要检查明显不合理的业务记录，比如：

- `adults = 0` 但又有住宿记录
- `adr < 0`
- 总住店晚数等于 0

你需要在 notebook 里明确记录：

- 发现了什么问题
- 你如何处理
- 为什么这么处理

这会让你的 portfolio 看起来更像真实工作成果。

### 阶段 4：Exploratory Data Analysis

EDA 不要变成“想到什么画什么”，要围绕业务问题。

建议按这 4 个方向做：

#### 4.1 订单概况

- 总预订量
- 取消率
- City Hotel vs Resort Hotel 的订单量和取消率
- 年度 / 月度预订趋势

#### 4.2 客户与渠道

- 不同 `market_segment` 的取消率
- 不同 `distribution_channel` 的取消率
- 不同 `customer_type` 的表现
- 重复客户 vs 新客户 的差异

#### 4.3 预订行为

- `lead_time` 与取消率关系
- `deposit_type` 与取消率关系
- `booking_changes` 与取消率关系
- `total_of_special_requests` 与取消率关系

#### 4.4 收入与入住质量

- `adr` 在不同酒店类型中的分布
- 已取消订单和未取消订单的 ADR 差异
- 不同渠道带来的高价值订单情况

### 阶段 5：Feature Engineering

这一阶段是你从“会画图”走向“更高级分析”的关键。

你可以自己构造一些新字段：

- `total_nights = stays_in_weekend_nights + stays_in_week_nights`
- `total_guests = adults + children + babies`
- `is_family`：是否家庭出行
- `arrival_date`：把年月日组合成真正日期
- `booking_month`：提取月份，方便看季节性
- `same_room_assigned`：预订房型是否和实际分配一致

这些特征会让你的分析更有深度，也更像真实业务分析。

### 阶段 6：Insight Generation

这一步不是重复图表，而是回答：

**“所以呢？”**

每个洞察都建议按这个结构写：

1. 观察到了什么
2. 为什么重要
3. 可能的业务解释
4. 建议采取什么动作

例如：

- 提前期越长的订单取消率更高
- 这意味着远期订单虽然增加了看起来的 demand，但实际入住不稳定
- 酒店应对远期订单做更谨慎的入住预测
- 对高风险远期订单可考虑更严格的取消政策或押金策略

### 阶段 7：Business Recommendations

你的结论不能停在“发现某某相关”。

建议最后至少给出 3 到 5 条业务建议，例如：

- 对高取消风险渠道建立更严格的取消政策
- 针对长提前期订单优化 forecasting 逻辑
- 优先加大低取消率客户群和渠道的营销预算
- 针对不同酒店类型使用不同运营策略
- 将特殊需求较多但取消率低的客群识别为高价值客群

### 阶段 8：Communication / Portfolio Packaging

最后要把成果整理成 portfolio 作品。

至少要有这 4 个部分：

- 项目背景
- 分析流程
- 核心洞察
- 业务建议

如果你要放在 GitHub 或求职作品里，建议再补：

- 数据字典摘要
- 清洗说明
- 局限性
- 下一步可以做的模型分析

---

## 4. 你应该如何组织这个项目文件

建议你把项目整理成下面这样：

```text
Hotel_booking_demand/
├── data/
│   └── hotel_bookings.csv
├── notebooks/
│   └── Xi_hotel.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
├── README.md
└── PORTFOLIO_GUIDE_ZH.md
```

如果你愿意，后面还可以加：

```text
├── src/
│   └── data_cleaning.py
└── requirements.txt
```

---

## 5. 你的 notebook 最好按这个顺序写

建议你在 notebook 中按下面结构分节：

### Section 1. Project Overview

- 业务背景
- 分析目标
- 核心问题

### Section 2. Data Loading

- 读取数据
- 查看 shape
- 查看字段
- 检查数据类型

### Section 3. Data Quality Check

- 缺失值检查
- `NULL` 字符串检查
- 重复值检查
- 异常值检查

### Section 4. Data Cleaning

- 替换伪缺失值
- 修正数据类型
- 删除或标记异常记录
- 构造新字段

### Section 5. Exploratory Analysis

- 总体取消率
- 酒店类型对比
- 渠道对比
- 客户类型对比
- 提前期分析
- ADR 分析

### Section 6. Key Insights

- 用短句总结 5 个左右核心发现

### Section 7. Recommendations

- 给出可执行建议

### Section 8. Limitations

- 数据是历史数据，不代表当前市场
- 没有利润成本字段
- 相关关系不等于因果关系

---

## 6. 新手最容易犯的 6 个问题

- 一上来就画图，没有先定义业务问题
- 只描述现象，没有解释业务意义
- 清洗过程没记录，别人不知道你做了什么
- 图很多，但没有结论
- 只会按变量逐个分析，没有形成故事线
- 最后没有转成建议，portfolio 就会显得像课堂作业

---

## 7. 这个项目最值得你重点练习的能力

结合你的背景，我建议你重点练这几项：

- `pandas`：数据清洗、分组聚合、特征构造
- `seaborn/matplotlib`：业务可视化
- 分析表达：把图表翻译成业务语言
- 假设思维：为什么会这样，是否符合业务逻辑
- 结构化汇报：从背景到建议形成完整叙事

如果你想进一步升级，这个项目后续还可以扩展：

- 用 `SQL` 重写部分分析
- 做一个 cancellation risk 的分类模型
- 用 `Tableau` 或 `Power BI` 做 dashboard
- 写成一份面试可讲的 case study

---

## 8. 你现在就可以开始做的顺序

### 第一步

先把环境装好，至少需要：

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install pandas numpy matplotlib seaborn jupyter
```

### 第二步

打开 `Hotel_booking_demand/notebooks/Xi_hotel.ipynb`，先完成：

- 项目背景
- 分析目标
- 读取数据
- 初步数据检查

### 第三步

专门做一节 Data Cleaning，不要跳过。

### 第四步

围绕“取消率”做第一轮 EDA，不要一次分析全部字段。

### 第五步

从 EDA 中提炼 3 到 5 个 strongest insights。

### 第六步

把 insight 写成业务建议。

### 第七步

最后再整理 notebook 排版和 README。

---

## 9. 一个适合你当前水平的项目定位

你的目标不是一开始就做得像资深数据科学家，而是做到：

**有清晰业务问题 + 有规范清洗流程 + 有可信分析结论 + 有业务建议**

如果你把这 4 件事做好，这已经是一个合格的初中级数据分析 portfolio 项目。

---

## 10. 建议你的下一步

下一步最合理的顺序是：

1. 先把 Python 分析环境装好
2. 修正 notebook 的基础导入代码
3. 完成数据读取和数据质量检查
4. 再开始第一轮 EDA

你现在这个项目已经选对方向了。后面最重要的不是“多做”，而是“按真实流程做完整”。 
