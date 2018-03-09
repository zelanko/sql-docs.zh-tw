---
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b8545cb5104122950869d3aa4975be403d06755
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含在進行中和已完成的載入作業的相關資訊[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 資訊會保留在系統重新啟動。  
  
|||||  
|-|-|-|-|  
|資料行名稱|資料類型|Description|範圍|  
|run_id|**int**|執行載入器的唯一識別碼。||  
|stage (階段)|**nvarchar(30)**|目前的執行階段。|'CREATE_STAGING'、 'DMS_LOAD'、 'LOAD_INSERT'、 'LOAD_CLEANUP'|  
|request_id|**nvarchar(32)**|執行這個階段的要求識別碼。||  
|status|**nvarchar(16)**|這個階段的狀態。||  
|start_time|**datetime**|階段開始時間。||  
|end_time|**datetime**|階段結束時間，如果有的話。|如果未啟動或正在進行中 NULL。|  
|total_elapsed_time|**int**|執行這個階段所花費的 （或花費為止） 的總時間。|如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會導致具體化失敗，因為發生溢位。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
