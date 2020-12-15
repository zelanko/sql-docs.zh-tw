---
title: 一般子運算式
description: 顯示在 Analytics Platform System CU 7.3 中引進的範例查詢改進
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7'
ms.openlocfilehash: 8dfadabcae27ff8705d86294b1c05851245d199c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97420197"
---
# <a name="common-subexpression-elimination-explained"></a>常見的子運算式清除已說明

AP CU 7.3 利用 SQL 查詢最佳化工具中常見的子運算式消除來改善查詢效能。 改進以兩種方式改善查詢。 第一個優點是識別並消除這類運算式有助於減少 SQL 編譯時間的能力。 第二個和更重要的優點是，這些多餘子運算式的資料移動作業已被刪除，因此查詢的執行時間會變得更快。

```sql
select top 100 asceding.rnk, i1.i_product_name best_performing, i2.i_product_name worst_performing
  from(select *
       from (select item_sk,rank() over (order by rank_col asc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V1)V11
       where rnk  < 11) asceding,
      (select *
       from (select item_sk,rank() over (order by rank_col desc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V2)V21
       where rnk  < 11) descending,
  item i1,
  item i2
  where asceding.rnk = descending.rnk
    and i1.i_item_sk=asceding.item_sk
    and i2.i_item_sk=descending.item_sk
  order by asceding.rnk
  ;
```
請考慮來自 TPC DS 基準測試工具的上述查詢。  在上述查詢中，子查詢相同，但 order by 子句的 rank ( # A1 over 函式是以兩種不同的方式排序。 在 CU 7.3 之前，此子查詢會進行評估並執行兩次，一次是遞增順序，而針對遞減順序，則會產生兩個數據移動作業。 在安裝了「AP CU 7.3」之後，子查詢部分將會被評估一次，藉此減少資料移動，並更快完成查詢。

我們引進了稱為「OptimizeCommonSubExpressions」的 [功能交換器](appliance-feature-switch.md) ，即使在升級至「ap cu 7.3」之後，也能讓您測試此功能。 此功能預設為開啟，但可以關閉。 

> [!NOTE] 
> 功能切換值的變更需要重新開機服務。

您可以藉由在測試環境中建立下列資料表來嘗試範例查詢，並評估上述查詢的說明計畫。 

```sql
CREATE TABLE [dbo].[store_sales] (
    [ss_sold_date_sk] int NULL, 
    [ss_sold_time_sk] int NULL, 
    [ss_item_sk] int NOT NULL, 
    [ss_customer_sk] int NULL, 
    [ss_cdemo_sk] int NULL, 
    [ss_hdemo_sk] int NULL, 
    [ss_addr_sk] int NULL, 
    [ss_store_sk] int NULL, 
    [ss_promo_sk] int NULL, 
    [ss_ticket_number] int NOT NULL, 
    [ss_quantity] int NULL, 
    [ss_wholesale_cost] decimal(7, 2) NULL, 
    [ss_list_price] decimal(7, 2) NULL, 
    [ss_sales_price] decimal(7, 2) NULL, 
    [ss_ext_discount_amt] decimal(7, 2) NULL, 
    [ss_ext_sales_price] decimal(7, 2) NULL, 
    [ss_ext_wholesale_cost] decimal(7, 2) NULL, 
    [ss_ext_list_price] decimal(7, 2) NULL, 
    [ss_ext_tax] decimal(7, 2) NULL, 
    [ss_coupon_amt] decimal(7, 2) NULL, 
    [ss_net_paid] decimal(7, 2) NULL, 
    [ss_net_paid_inc_tax] decimal(7, 2) NULL, 
    [ss_net_profit] decimal(7, 2) NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([ss_item_sk]),  PARTITION ([ss_sold_date_sk] RANGE RIGHT FOR VALUES (2450815, 2451180, 2451545, 2451911, 2452276, 2452641, 2453006)));

CREATE TABLE [dbo].[item] (
    [i_item_sk] int NOT NULL, 
    [i_item_id] char(16) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, 
    [i_rec_start_date] date NULL, 
    [i_rec_end_date] date NULL, 
    [i_item_desc] varchar(200) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_current_price] decimal(7, 2) NULL, 
    [i_wholesale_cost] decimal(7, 2) NULL, 
    [i_brand_id] int NULL, 
    [i_brand] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_class_id] int NULL, 
    [i_class] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_category_id] int NULL, 
    [i_category] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manufact_id] int NULL, 
    [i_manufact] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_size] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_formulation] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_color] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_units] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_container] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manager_id] int NULL, 
    [i_product_name] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL
)
WITH (CLUSTERED INDEX ( [i_item_sk] ASC ), DISTRIBUTION = REPLICATE);
```
如果您查看查詢的說明計畫，您將會看到在 CU 7.3 (或功能切換關閉) 查詢有17個作業總數，以及在 CU 7.3 (或已開啟功能切換之後) 相同的查詢顯示9個作業總數。 如果您只計算資料移動作業，您將會看到先前的方案有四個移動作業，以及新方案中的兩個移動作業。 新的查詢最佳化工具可以減少兩個數據移動作業，方法是重複使用已使用新方案建立的臨時表，從而減少查詢執行時間。 


