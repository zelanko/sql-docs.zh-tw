---
title: sys.databases pdw_loader_run_stages （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b25a615f6b420b9cc08fe5d7600249cb0e5fb03
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394232"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>sys.databases pdw_loader_run_stages （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  包含在中進行中和已完成之載入作業的相關資訊 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。 此資訊在系統重新啟動之後會持續存留。  
  
| 資料行名稱 | 資料類型 | 描述 | 範圍 |
| ----------- | --------- | ----------- | ----- |
|run_id|**int**|載入器執行的唯一識別碼。||  
|stage (階段)|**nvarchar(30)**|執行的目前階段。|[CREATE_STAGING]、[DMS_LOAD]、[LOAD_INSERT]、[LOAD_CLEANUP]|  
|request_id|**nvarchar(32)**|執行此階段之要求的識別碼。||  
|status|**Nvarchar （16）**|此階段的狀態。||  
|start_time|**datetime**|階段啟動的時間。||  
|end_time|**datetime**|階段結束的時間（如果有的話）。|如果未啟動或進行中，則為 Null。|  
|total_elapsed_time|**int**|這個階段花費的總時間（或到目前為止）執行。|如果 total_elapsed_time 超過整數的最大值（以毫秒為單位的24.8 天），則會造成具體化失敗，因為溢位。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
