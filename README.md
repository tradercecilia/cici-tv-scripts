# tv-pinescripts

TradingView Pine Script 指标合集

> 本仓库脚本为【交易员Cici】粉丝福利开源，仅供投研复盘、数据观测学习使用。
> **不构成任何投资建议，不承诺盈利，市场有风险，交易决策请自行负责。**

## 脚本清单

- `cici_euro_spread_monitor_v1.pine`：欧元利差监控指标 v1


CC France-Germany 10Y Spread Monitor tracks the yield spread between French and German 10-year government bonds. It combines short-term change detection, historical high/low comparisons, and yield-contribution analysis in one indicator.

Calculation

Spread in basis points = (French yield − German yield) × 100.

By default, the indicator compares the 60-minute spread change with the mean and standard deviation of the previous 240 valid change samples. A widening or narrowing alert requires both a directional deviation of at least 3 standard deviations and an absolute change of at least 1 basis point. These settings are adjustable.

Historical comparisons use daily envelope proxies:
High = (French daily high − German daily low) × 100.
Low = (French daily low − German daily high) × 100.

These are not synchronized spread OHLC values. They may overstate the historical range and delay or miss a breakout. Actual historical coverage depends on the available data.

Usage and alerts

Use standard EUR/USD candlestick charts. The recommended interval is 1 hour; supported intervals are 1–60 minutes. The observation window must be a multiple of the chart interval.

Enable real-time alerts in the indicator settings, then create a TradingView alert using “Any alert() function call.” Select notification channels in TradingView. Recreate the alert after changing the script or its inputs.

Real-time alerts can trigger intrabar. The table and markers use confirmed bar-close data, with timestamps corresponding to the source bar’s opening-time label. A temporary intrabar alert may therefore be absent from the table. Consult TradingView’s Alerts Log for actual alert timestamps and values.

Dashed lines across missing quotes are visual connections only and are excluded from calculations.

The indicator provides monitoring information, not trade instructions. Fundamental notes are research prompts, not confirmed explanations of market moves.

中文介绍

这个指标用于观察法国与德国10年期国债收益率之差，辅助识别欧元区债券市场的相对定价变化。

它将短期利差变化、长期历史高低位比较，以及法国和德国两端收益率的贡献放在同一个界面中，方便结合EUR/USD走势进行研究。

一、主要功能

1. 利差走势

法德利差＝法国10年期收益率－德国10年期收益率，统一换算为基点（bp）显示。

2. 异常扩大与异常收窄

默认观察60分钟变化，与此前240个有效变化样本比较。触发需要同时满足异常分数和最小绝对变化要求，默认分别为3倍标准差和1bp。

异常分数用于衡量本次变化相对近期分布的偏离程度，不代表固定的概率或交易胜率。

3. 历史高低位突破

检测利差是否严格突破符合历史间隔要求的高点或低点，并在记录中列出比较日期和数值。超过全部可用历史范围时，会单独标识。

历史高低值采用法国与德国日线高低值构成的区间代理，并非同一时刻的真实利差高低点。这一近似可能使历史区间偏宽，导致突破延后或遗漏。

4. 收益率贡献与基本面关注

区分法国收益率上升、德国收益率下降、两端共同变化等情形，帮助观察利差变化由哪一端推动。

“基本面关注”提供后续核对方向，不代表指标已经确认新闻原因，也不意味着利差变化一定导致欧元同向或反向波动。

二、表格记录与实时警报的区别

副图表格和标记以已收盘K线为准，时间使用该根K线的标签。

例如，1小时图上显示“18:00”，对应18:00开始的这根K线，数值按该根K线收盘计算，不表示18:00已经发生盘中触发。

实时警报可以在盘中即时发送。若盘中短暂满足条件、收盘时已经恢复，这条警报可能不会出现在收盘记录表中。

具体触发时间、当时数值和实际提醒历史，请查看TradingView警报日志。将鼠标移至表头ⓘ可查看说明。

三、使用方法

建议加载到EUR/USD普通K线图，使用1小时周期。支持1至60分钟周期，变化观察窗口必须是图表周期的整数倍。

主图状态表展示当前利差、变化、异常分数和收益率贡献；副图展示利差曲线、变化范围边界和最近3次或5次收盘记录。

默认同类同方向提醒间隔为8小时。突破更早的历史区间时，可新增历史跨度升级事件。收盘记录与实时警报分别计算去重状态。

四、设置警报

在指标参数中开启“允许发送实时提醒”，然后通过TradingView顶部工具栏创建警报：

选择本指标 → 任何alert()函数调用 → 设置通知渠道。

App通知、弹窗、邮件及Webhook等渠道在TradingView警报窗口中选择。更新代码或修改参数后，需要重新创建警报。

五、数据说明

默认收益率来源为TVC:FR10Y和TVC:DE10Y，可在参数中调整。历史目标起点与实际数据覆盖可能不同，实际起点显示在状态表中。

缺失报价之间的细虚线仅用于视觉连接，不代表该区间的真实走势，不参与异常计算。报价缺失、样本不足或时间未对齐时，部分字段会显示为空。

本指标用于市场观察与研究，不提供买卖指令。
