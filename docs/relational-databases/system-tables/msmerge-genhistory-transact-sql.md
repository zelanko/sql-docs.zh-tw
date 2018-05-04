---
title: MSmerge_genhistory (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c7b3958fa0774d524f439b1dd58e9d83af2c07ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_genhistory**資料表包含一個資料列的每個訂閱者知道 （在保留期限內） 的層代。 其目的是防止在交換時傳送共用層代 (Generation)，並且重新同步處理從備份還原的訂閱者。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|由訂閱者的層代 (Generation) 所識別之變更的全域識別碼。|  
|**pubid**|**uniqueidentifier**|發行集識別碼。|  
|**產生**|**bigint**|層代 (Generation) 值。|  
|**art_nick**|**int**|發行項的暱稱。|  
|**別名**|**varbinary(1001)**|這個層代 (Generation) 已經知道的其他訂閱者的暱稱清單。 其目的是避免將層代 (Generation) 傳送給已經看過那些變更的訂閱者。 為了提高搜尋的效率，暱稱清單中的暱稱都是依序維護的。 如果暱稱太多，超過這個欄位的容量，它們就無法達到最佳化的效果。|  
|**coldate**|**datetime**|將目前層代 (Generation) 加入資料表中的日期。|  
|**層代狀態**|**tinyint**|層代 (Generation) 狀態如下：<br /><br /> **0** = 已開啟。<br /><br /> **1** = 關閉。<br /><br /> **2** = 已關閉，而且是源自於另一個訂閱者。|  
|**changecount**|**int**|在給定層代 (Generation) 反映的變更數目|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
