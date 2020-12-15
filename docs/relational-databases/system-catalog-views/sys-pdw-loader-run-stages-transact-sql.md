---
description: 'sys.pdw_loader_run_stages (Transact-sql) '
title: sys.pdw_loader_run_stages (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: ee8eb27964a7fc26d5af6c8f7a13293720ca7821
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475149"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  包含中進行中和已完成之載入作業的相關資訊 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。 此資訊在系統重新啟動之後會持續存留。  
  
| 資料行名稱 | 資料類型 | 描述 | 範圍 |
| ----------- | --------- | ----------- | ----- |
|run_id|**int**|載入器執行的唯一識別碼。||  
|stage (階段)|**nvarchar(30)**|執行的目前階段。|「CREATE_STAGING」、「DMS_LOAD」、「LOAD_INSERT」、「LOAD_CLEANUP」|  
|request_id|**nvarchar(32)**|執行此階段之要求的識別碼。||  
|status|**Nvarchar (16)**|此階段的狀態。||  
|start_time|**datetime**|階段的開始時間。||  
|end_time|**datetime**|階段結束的時間（如果有的話）。|如果未啟動或進行中，則為 Null。|  
|total_elapsed_time|**int**|這個階段花費在執行 (或花費到目前為止的總時間) 。|如果 total_elapsed_time 超過整數 (24.8 天（以毫秒為單位）的最大值) ，則會造成具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
