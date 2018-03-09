---
title: "M (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7453274dee183a0222d6a0e6ae43f052a628c9aa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplmonthresholdmetrics**資料表定義專用來監視複寫的標準。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|識別複寫效能標準，而且它可以是下列其中一個值：<br /><br /> **1** = 到期日<br /><br /> **2** = 延遲<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|複寫效能標準的名稱。|  
|**warningbitstatus**|**int**|用來提供下列標準的臨界違規警告之位元識別碼：<br /><br /> **1** = expiration – 交易式發行集的訂閱已超過所允許的臨界值，保留週期的保留期限的百分比。<br /><br /> **2** = latency-將交易式發行者的資料複寫到訂閱者所花費的時間超過臨界值，以秒為單位。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱已超過所允許的臨界值，保留週期的保留期限的百分比。<br /><br /> **8** = mergefastrunduration-完成合併訂閱的同步處理所花的時間超出臨界值，以秒為單位，快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱的同步處理所花的時間超出臨界值，以秒為單位，慢速或撥號網路連線。<br /><br /> **32** = mergefastrunspeed – 利用的傳遞速率無法維持臨界速率，以每秒資料列，透過快速網路連接合併訂閱同步處理期間，資料列。<br /><br /> **64** = mergeslowrunspeed – 傳遞速率合併訂閱同步處理期間，資料列無法維持臨界速率，以每秒資料列，透過慢速或撥號網路連線。|  
|**alertmessageid**|**int**|當發生臨界值警告狀況時，所顯示之錯誤訊息的識別碼。|  
|**描述**|**nvarchar （3000)**|複寫效能標準的描述|  
|**預設值**|**sql_variant**|複寫效能標準的預設值。|  
|**min_value**|**sql_variant**|繫結的複寫效能標準的最小值。|  
|**max_value**|**sql_variant**|繫結的複寫效能標準的最大值。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
