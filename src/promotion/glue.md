# 通用抽奖工具(Glue万能胶)

## 抽奖需求分析

首先我们先来回顾下**营销体系**的组成：

|营销体系|
|---|
|活动营销系统|
|销售营销系统|

今天带来的是**活动营销系统**下的第一个独立子系统**通用抽奖工具**的介绍，本篇文章主要分为如下4部分：

- 常见抽奖场景与归类
- 抽奖需求配置
- 常见奖品类型
- 抽奖五要素

## 常见抽奖场景与归类

下面是我列出来的一些常见的抽奖场景，红包雨、糖果雨、打地鼠、大转盘(九宫格)、考眼力、答题闯关、游戏闯关、支付刮刮乐、积分刮刮乐等等活动营销场景。

|活动名称|描述|
|------|------|
|红包雨|每日整点抢红包🧧抽奖，每个整点一般可参与一次|
|糖果雨|每日整点抢糖果🍬抽奖，每个整点一般可参与一次|
|打地鼠|每日整点打地鼠抽奖，每个整点一般可参与一次|
|大转盘(九宫格)|某个时间段，转盘抽奖，每个场一般可参N次|
|考眼力|某个时间段，旋转杯子猜小球在哪个被子里，猜对可抽奖，一般每日可参与N次|
|答题闯关|每过一关，可参与抽奖，越到后面奖品越贵重|
|游戏闯关|每过一关，可参与抽奖，越到后面奖品越贵重|
|支付刮刮乐|支付订单后可刮奖，支付金额越大奖品越贵重|
|积分刮刮乐|积分刮奖，消费积分额度越大奖品越贵重|

通过上面的活动描述，我们把整个抽奖场景归为以下三类：

|类型|活动名称|维度|
|-|-|-|
|按时间抽奖|红包雨、糖果雨、打地鼠、幸运大转盘(九宫格)、考眼力|时间维度|
|按抽奖次数抽奖|答题闯关、游戏闯关|参与该活动次数维度|
|按数额范围区间抽奖|支付刮刮乐、积分刮刮乐|数额区间维度|

接着我们来看下每类抽奖活动具体的抽奖需求配置。

## 抽奖需求配置

本小节每类抽奖活动的需求配置，分为如下三个部分：

- 活动配置
- 场次配置
- 奖品配置

### 首先，第一类: `按时间抽奖`的需求配置

|类型|活动名称|特点|
|-|-|-|
|按时间抽奖|红包雨、糖果雨、打地鼠、幸运大转盘(九宫格)、考眼力|时间维度|

|按时间抽奖|是否多场次|单场次次数限制(次)|总场次次数限制(次)|
|-|-|-|-|
|红包雨|是|1|N|
|糖果雨|是|1|N|
|打地鼠|是|N|N|
|幸运大转盘(九宫格)|否|N|N|
|考眼力|否|N|N|

通过上面的分析我们得到了**活动**和**场次**的概念: 一个活动需要支持多场次的配置。

- 活动activity:配置活动的日期范围
- 场次session:配置每场的具体时间范围

**红包雨的需求配置示例：**

> 活动特征：红包雨需要支持多场次。

比如双十二期间三天、每天三场整点红包雨配置如下：

活动、场次配置：

|双十二红包雨|
|------|
|活动配置：|
|2019-12-10 至 2019-12-12|
|场次配置：|
|10:00:00 至 10:01:00|
|12:00:00 至 12:01:00|
|18:00:00 至 18:01:00|

奖品配置：

|场次|奖品1|奖品2|---|奖品N|
|------|------|------|---|------|
|场次10:00:00 至 10:01:00|优惠券2元|空奖|---|无|
|场次12:00:00 至 12:01:00|优惠券5元|空奖|---|无|
|场次18:00:00 至 18:01:00|优惠券10元|优惠券20元|---|空奖|

```md
上面配置的结果如下：

2019-12-10日三场整点红包雨：
2019-12-10 10:00:00 ~ 10:01:00
2019-12-10 12:00:00 ~ 12:01:00
2019-12-10 18:00:00 ~ 18:01:00

2019-12-11日三场整点红包雨：
2019-12-11 10:00:00 ~ 10:01:00
2019-12-11 12:00:00 ~ 12:01:00
2019-12-11 18:00:00 ~ 18:01:00

2019-12-12日三场整点红包雨：
2019-12-12 10:00:00 ~ 10:01:00
2019-12-12 12:00:00 ~ 12:01:00
2019-12-12 18:00:00 ~ 18:01:00
```

**幸运大转盘的需求配置示例：**

> 活动特征：幸运大转盘不需要多场次。

比如年货节2020-01-20 至 2020-02-10期间幸运大转盘配置如下：

活动、场次配置：

|双十二幸运大转盘|
|------|
|活动配置：|
|2019-12-10 至 2019-12-12|
|场次配置：|
|00:00:00 至 23:59:59|

奖品配置：

|场次|奖品1|奖品2|---|奖品N|
|------|------|------|---|------|
|场次00:00:00 至 23:59:59|优惠券2元|空奖|---|无|

```md
上面配置的结果如下：

幸运大转盘抽奖活动将于 2019-12-10 00:00:00 ~ 2019-12-12 23:59:59 进行
```

注意与思考：双十二幸运大转盘不需要多个场次，只配置一个场次即可，完全复用活动场次模型。

### 接着，第二类: `按抽奖次数抽奖`的需求配置

|类型|活动名称|特点|
|-|-|-|
|按抽奖次数抽奖|答题闯关、游戏闯关|(成功参与)当前活动次数维度|

**答题闯关的需求配置示例：**

> 活动特征：每一关的奖品不同，一般越到后面中大奖的几率越大。

活动、场次配置：

|双十二答题闯关|
|------|
|活动配置：|
|2019-12-10 至 2019-12-12|
|场次配置：|
|00:00:00 至 23:59:59|

奖品配置：

|双十二答题闯关|奖品|
|------|------|
|第一关|优惠券2元|
|第二关|优惠券5元|
|第三关|优惠券10元|
|第四关|优惠券20元|
|第五关|优惠券50元|
|第六关|优惠券100元|

注意与思考：同理活动&场次配置完全复用，同幸运大转盘配置(不需要支持多场次)。

### 最后，第三类: `按数额范围区间抽奖`的需求配置：

|类型|活动名称|特点|
|-|-|-|
|按数额范围区间抽奖|支付刮刮乐、积分刮刮乐|数额区间维度|

**支付刮刮乐的需求配置示例：**

> 活动特征：不同的订单金额，一般金额越大中大奖的几率越大。

活动、场次配置:

|双十二答题闯关|
|------|
|活动配置：|
|2019-12-10 至 2019-12-12|
|场次配置：|
|00:00:00 至 23:59:59|

奖品配置：

|订单金额|奖品1|奖品2|---|奖品N|
|------|------|------|---|------|
|0~100|优惠券2元|空奖|---|无|
|100~200|优惠券5元|空奖|---|无|
|200~1000|优惠券10元|优惠券20元|---|空奖|
|1000以上|优惠券50元|笔记本电脑|---|空奖|

注意与思考：同理活动&场次配置完全复用，同幸运大转盘配置(不需要支持多场次)。

> 总结: 通过上面的分析我们得到了抽奖工具的两个要素**活动**和**场次**。


## 常见奖品类型

> 抽奖抽什么？

|常见奖品类型|
|-|
|优惠券|
|积分|
|实物|
|空奖|

> 总结: 我们得到了抽奖工具的另一个要素**奖品**。

## 抽奖五要素

通过上面的分析我们已经得到了抽奖的**三要素**

- 活动 
- 场次 
- 奖品

> 那还有什么要素我们还没聊到呢？接下来来看。

### 第四要素：中奖概率

抽奖自然离不开奖品的中奖概率的设置。关于中奖概率我们支持如下灵活的配置：

1. 手动设置奖品中奖概率
2. 自动概率，根据当前奖品的数量、奖品的权重得到中奖概率

比如我们某次大促活动红包雨的配置如下：

活动配置|描述
------|------
活动时间|2019-12-10至2019-12-12
活动名称|2019双十二大促整点红包雨
活动描述|2019双十二大促全端整点红包雨活动
手动设置奖品概率|是

|场次|奖品类型|具体奖品|奖品数量|中奖概率
|-|-|-|-|-|
|10:00:00 ~ 10:01:00|优惠券|2元优惠券|2000|50%|
|-|优惠券|5元优惠券|1000|20%|
|-|空奖|-|5000|30%|
|12:00:00 ~ 12:01:00|优惠券|2元优惠券|2000|50%|
|-|优惠券|5元优惠券|1000|20%|
|-|空奖|-|5000|30%|
|18:00:00 ~ 18:01:00|优惠券|2元优惠券|2000|50%|
|-|优惠券|5元优惠券|1000|20%|
|-|空奖|-|5000|30%|

备注：每轮场次中奖概率之和必须为100%，否则剩余部分默认添加为空奖的中奖概率。

### 第五要素：均匀投奖

> 如何均匀的抽走奖品?

答案: 均匀投奖。

具体方式为拆分总奖品数量，到各个细致具体的时间段。以双十二幸运大转盘为例：

|场次|奖品类型|具体奖品|奖品数量|中奖概率|投奖时间(默认提前5分钟投奖)|投奖数量
|-|-|-|-|-|-|-|
|00:00:00 至 23:59:59|优惠券|2元优惠券|2000|50%|-|-|
|-|-|-|-|-|00:00:00|2000|
|-|-|-|-|-|06:00:00|2000|
|-|-|-|-|-|12:00:00|2000|
|-|-|-|-|-|18:00:00|2000|

这里我们就得到了抽奖的**第五个要素：均匀投奖**。

## 需求总结

通过上面的分析，我们得到抽奖五要素如下：

抽奖五要素|要素名称
------|------
第一要素|活动
第二要素|场次
第三要素|奖品
第四要素|中奖概率
第五要素|均匀投奖

同时我们通过**抽奖五要素**也得到了**通用抽奖工具**配置一场抽奖活动的5个基本步骤：

1. 活动配置
2. 场次配置
3. 奖品配置
4. 奖品中奖概率配置
5. 奖品投奖配置

## 通用抽奖工具系统设计

需求已经分析完了，今天我们就来看看这通用抽奖工具具体的设计，分为如下三个部分：

- DB设计
- 配置后台设计
- 接口设计

## DB设计

第一要素`活动配置`的`抽奖活动表`：

```sql
-- 通用抽奖工具(万能胶Glue) glue_activity 抽奖活动表
CREATE TABLE `glue_activity` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '活动ID',
    `serial_no` char(16) unsigned NOT NULL DEFAULT '' COMMENT '活动编号(md5值中间16位)',
    `name` varchar(255)  NOT NULL DEFAULT '' COMMENT '活动名称',
    `description` varchar(255)  NOT NULL DEFAULT '' COMMENT '活动描述',
    `activity_type` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '活动抽奖类型1: 按时间抽奖 2: 按抽奖次数抽奖 3:按数额范围区间抽奖',
    `probability_type` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '中奖概率类型1: static 2: dynamic',
    `times_limit` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '抽奖次数限制，0默认不限制',
    `start_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '活动开始时间',
    `end_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '活动结束时间',
    `create_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建时间',
    `create_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建人staff_id',
    `update_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '更新时间',
    `update_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '修改人staff_id',
    `status` tinyint(1)  NOT NULL DEFAULT '0' COMMENT '状态 -1:deleted, 0:disable, 1:enable',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='抽奖活动表';
```

第二要素`场次配置`的`抽奖场次表`：

```sql
-- 通用抽奖工具(万能胶Glue) glue_session 抽奖场次表
CREATE TABLE `glue_session` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '场次ID',
    `activity_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '活动ID',
    `times_limit` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '抽奖次数限制，0默认不限制',
    `start_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '场次开始时间',
    `end_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '场次结束时间',
    `create_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建时间',
    `create_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建人staff_id',
    `update_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '更新时间',
    `update_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '修改人staff_id',
    `status` tinyint(1)  NOT NULL DEFAULT '0' COMMENT '状态 -1:deleted, 0:disable, 1:enable',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='抽奖场次表';
```

第三、四要素`奖品配置`的`抽奖场次奖品表`：

```sql
-- 通用抽奖工具(万能胶Glue) glue_session_prizes 抽奖场次奖品表
CREATE TABLE `glue_session_prizes` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '自增ID',
    `session_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '场次ID',
    `node` varchar(255)  NOT NULL DEFAULT '' COMMENT '节点标识 按时间抽奖: 空值, 按抽奖次数抽奖: 第几次参与值, 按数额范围区间抽奖: 数额区间上限值',
    `prize_type` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '奖品类型 1:优惠券, 2:积分, 3:实物, 4:空奖 ...',
    `name` varchar(255)  NOT NULL DEFAULT '' COMMENT '奖品名称',
    `pic_url` varchar(255)  NOT NULL DEFAULT '' COMMENT '奖品图片',
    `value` varchar(255)  NOT NULL DEFAULT '' COMMENT '奖品抽象值 优惠券:优惠券ID, 积分:积分值, 实物: sku ID',
    `probability` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '中奖概率1~100',
    `create_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建时间',
    `create_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建人staff_id',
    `update_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '更新时间',
    `update_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '修改人staff_id',
    `status` tinyint(1)  NOT NULL DEFAULT '0' COMMENT '状态 -1:deleted, 0:disable, 1:enable',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='抽奖场次奖品表';

```

第五要素`均匀投奖`的`抽奖场次奖品定时投放器表`：

```sql
-- 通用抽奖工具(万能胶Glue) glue_session_prizes_timer 抽奖场次奖品定时投放器表
CREATE TABLE `glue_session_prizes_timer` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '自增ID',
    `session_prizes_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '抽奖场次奖品ID',
    `delivery_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '定时投放奖品数量的时间',
    `prize_quantity` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '奖品数量',
    `create_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建时间',
    `create_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建人staff_id',
    `update_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '更新时间',
    `update_by` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '修改人staff_id',
    `status` tinyint(1)  NOT NULL DEFAULT '0' COMMENT '状态 -1:deleted, 0:wait, 1:success',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='抽奖场次奖品定时投放器表';

```

其他表，抽奖记录&奖品发放记录表：

```sql
-- 通用抽奖工具(万能胶Glue) glue_user_draw_record 用户抽奖记录表
CREATE TABLE `glue_user_draw_record` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '自增ID',
    `activity_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '活动ID',
    `session_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '场次ID',
    `prize_type_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '奖品类型ID',
    `user_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建人user_id',
    `create_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '创建时间',
    `update_at` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '更新时间',
    `status` tinyint(1)  NOT NULL DEFAULT '0' COMMENT '状态 -1:未中奖, 1:已中奖 , 2: 发奖失败 , 3: 已发奖',
    `log` text COMMENT '操作信息等记录',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='用户抽奖记录表';
```

## 配置后台设计

### 创建活动

<p align="center">
    <a href="http://cdn.tigerb.cn/20191229224816.png?imageMogr2/thumbnail/1934x1567!/format/webp/blur/1x0/quality/75|imageslim" data-lightbox="roadtrip">
        <img src="http://cdn.tigerb.cn/20191229224816.png?imageMogr2/thumbnail/1934x1567!/format/webp/blur/1x0/quality/75|imageslim" width="66%">
    </a>
</p>

### 创建活动场次

<p align="center">
    <a href="http://cdn.tigerb.cn/20191230081157.png?imageMogr2/thumbnail/971x2069!/format/webp/blur/1x0/quality/75%7Cimageslim" data-lightbox="roadtrip">
        <img src="http://cdn.tigerb.cn/20191230081157.png?imageMogr2/thumbnail/971x2069!/format/webp/blur/1x0/quality/75%7Cimageslim" width="66%">
    </a>
</p>

<p align="center">
    <a href="http://cdn.tigerb.cn/20191229224543.png?imageMogr2/thumbnail/971x2214!/format/webp/blur/1x0/quality/75%7Cimageslim" data-lightbox="roadtrip">
        <img src="http://cdn.tigerb.cn/20191229224543.png?imageMogr2/thumbnail/971x2214!/format/webp/blur/1x0/quality/75%7Cimageslim" width="66%">
    </a>
</p>

<p align="center">
    <a href="http://cdn.tigerb.cn/20191229224834.png?imageMogr2/thumbnail/971x1693!/format/webp/blur/1x0/quality/75%7Cimageslim" data-lightbox="roadtrip">
        <img src="http://cdn.tigerb.cn/20191229224834.png?imageMogr2/thumbnail/971x1693!/format/webp/blur/1x0/quality/75%7Cimageslim" width="66%">
    </a>
</p>

### 活动列表

<p align="center">
    <a href="http://cdn.tigerb.cn/20191229223706.png?imageMogr2/thumbnail/1338x761!/format/webp/blur/1x0/quality/75%7Cimageslim" data-lightbox="roadtrip">
        <img src="http://cdn.tigerb.cn/20191229223706.png?imageMogr2/thumbnail/1338x761!/format/webp/blur/1x0/quality/75%7Cimageslim" width="66%">
    </a>
</p>


## 接口设计

1. 获取活动信息 GET {version}/glue/activity

请求参数：

字段|类型|是否必传|描述
------------|------------|------------|------------
serial_no|string|Y|活动编号

响应内容：
```json
{
    "code": "200",
    "msg": "OK",
    "result": {
        "serial_no": "string, 活动编号",
        "type": "number, 活动抽奖类型1: 按时间抽奖 2: 按抽奖次数抽奖 3:按数额范围区间抽奖",
        "name": "string, 活动名称",
        "description": "string, 活动描述",
        "start_time": "number, 活动开始时间",
        "end_time": "number, 活动开始时间",
        "remaining_times": "number, 活动抽奖次数限制，0不限制",
        "sessions_list":[
            {
                "start_time": "number, 场次开始时间",
                "end_time": "number, 场次开始时间",
                "remaining_times": "number, 场次抽奖次数限制，0不限制",
                "prizes_list": [
                    {
                        "name": "string, 奖品名称",
                        "pic_url": "string, 奖品图片"
                    }
                ]
            }
        ]
    }
}
```

2. 抽奖 POST {version}/glue/activity/draw

请求参数：

字段|类型|是否必传|描述
------------|------------|------------|------------
serial_no|string|Y|活动编号
uid|number|Y|用户ID

响应内容：
```json
// 中奖
{
    "code": "200",
    "msg": "OK",
    "result": {
        "serial_no": "string, spu id",
        "act_remaining_times": "number, 本活动抽奖剩余次数，0不限制",
        "session_remaining_times": "number, 本场次抽奖剩余次数，0不限制",
        "prizes_info": 
        {
            "name": "string, 奖品名称",
            "pic_url": "string, 奖品图片"
        }
    }
}

// 未中奖
{
    "code": "401",
    "msg": "",
    "result": {
        
    }
}
```

## 结语

活动营销系统中的第一个字系统**通用抽奖工具**今天讲完了，希望对大家有一定的帮助或启示。