---
title: MSmerge_dynamic_snapshots （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_dynamic_snapshots_TSQL
- MSmerge_dynamic_snapshots
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_dynamic_snapshots system table
ms.assetid: a5592b3c-731b-4fc9-ae4b-2602ed78248e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 36d16c7a23f2c586378136b6dd045231941708e8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736766"
---
# <a name="msmerge_dynamic_snapshots-transact-sql"></a>MSmerge_dynamic_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_dynamic_snapshots**資料表會使用參數化資料列篩選器，針對合併式發行集所定義的每個分割區，追蹤已篩選資料快照集的位置。 這份資料表儲存在**發行**集資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|合併資料分割的識別碼。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|資料分割的已篩選資料快照集位置。|  
|**last_updated**|**datetime**|重新整理已篩選資料快照集的日期。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
