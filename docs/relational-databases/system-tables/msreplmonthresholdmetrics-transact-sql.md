---
title: MSreplmonthresholdmetrics （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ad67ea6744256e3bcc041c736fbe6fe516773b11
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889416"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSreplmonthresholdmetrics**資料表會定義針對監視複寫所提供的計量。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|識別複寫效能標準，而且它可以是下列其中一個值：<br /><br /> **1** = 到期<br /><br /> **2** = 延遲<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration 利用<br /><br /> **7** = mergefastrunspeed 利用<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|複寫效能標準的名稱。|  
|**warningbitstatus**|**int**|用來提供下列標準的臨界違規警告之位元識別碼：<br /><br /> **1** = 到期-交易式發行集的訂閱已超出保留期限，超過允許的閾值，以保留期限的百分比表示。<br /><br /> **2** = 延遲-將交易式發行者的資料複寫到訂閱者所花費的時間超過臨界值（以秒為單位）。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱已超出保留期限，超過允許的臨界值，以保留期限的百分比表示。<br /><br /> **8** = mergefastrunduration 利用-完成合併訂閱同步處理所花費的時間超過閾值（以秒為單位），透過快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱同步處理所花費的時間超過慢速或撥號網路連接的閾值（以秒為單位）。<br /><br /> **32** = mergefastrunspeed 利用-合併訂閱同步處理期間的資料列傳遞速率無法以快速網路連接維持閾值速率（以每秒資料列數為單位）。<br /><br /> **64** = mergeslowrunspeed-合併訂閱同步處理期間的資料列傳遞速率無法以速度較慢或撥號網路連接的速率，以每秒資料列數來維持閾值。|  
|**alertmessageid**|**int**|當發生臨界值警告狀況時，所顯示之錯誤訊息的識別碼。|  
|**description**|**Nvarchar （3000）**|複寫效能標準的描述|  
|**default_value**|**sql_variant**|複寫效能標準的預設值。|  
|**min_value**|**sql_variant**|繫結的複寫效能標準的最小值。|  
|**max_value**|**sql_variant**|繫結的複寫效能標準的最大值。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
