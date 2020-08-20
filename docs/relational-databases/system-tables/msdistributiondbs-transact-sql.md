---
description: MSdistributiondbs (Transact-SQL)
title: Msdb..msdistributiondbs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ccc4ea10d896a6422ca5b46f1bb4eb70bbc6ba0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480759"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Msdb..msdistributiondbs**資料表會針對本機散發者上定義的每個散發資料庫，各包含一個資料列。 此資料表儲存在 **msdb** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|散發資料庫的名稱。|  
|**min_distretention**|**int**|在刪除交易之前的最小保留期限 (以小時為單位)。|  
|**max_distretention**|**int**|在刪除交易之前的最大保留期限 (以小時為單位)。|  
|**history_retention**|**int**|保留記錄的時數。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
