---
title: "MSsnapshotdeliveryprogress (TRANSACT-SQL) |Microsoft 文件"
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
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7fbb80963679858339cc1df9206f101968f4f8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshotdeliveryprogress**資料表用來追蹤已經順利傳遞給訂閱者在套用快照集時的檔案。 這項資料用來繼續傳遞檔案，萬一合併代理程式在工作階段無法傳遞所有的檔案，那麼下次再執行合併代理程式時，不會再重複傳遞相同的檔案。 這份資料表儲存在訂閱資料庫的訂閱者端。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar （260)**|識別通往順利傳遞檔案之快照集資料夾的路徑。 發行集使用參數化的篩選，字串**dynsnap**會附加至的值。|  
|**progress_token_hash**|**int**|產生的雜湊值的值為基礎*progress_token*用來改善查詢效能的給定*progress_token*值。|  
|**progress_token**|**nvarchar （500)**|識別已經順利傳遞的檔案，該值是檔案名稱和路徑的組合。|  
|**progress_timestamp**|**datetime**|**Datetime**指出快照集檔案已成功傳遞的值。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
