---
title: sys.dm_resource_governor_resource_pool_affinity & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_affinity_TSQL
- sys.dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_affinity
- sys.dm_resource_governor_resource_pool_affinity
ms.assetid: a197ec19-a2ba-44f5-a4f2-3eee33ebd77d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 547a1dd14eab2a5627dbd8e3b8b6e09a4c5143b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815316"
---
# <a name="sysdmresourcegovernorresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  追蹤資源集區相似性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|----------------|---------------|-----------------|  
|Pool_id|**int**|資源集區的識別碼。 不可為 Null。|  
|Processor_group|**smallint**|Windows 邏輯處理器群組的 ID。 不可為 Null。|  
|Scheduler_mask|**bigint**|二進位遮罩，表示與此集區相關聯的排程器。 不可為 Null。|  
  
## <a name="remarks"></a>備註  
 以 AUTO 相似性建立的集區不會出現在此檢視中，因為它們沒有相似性。 如需詳細資訊，請參閱[建立資源集區&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/create-resource-pool-transact-sql.md)並[ALTER RESOURCE POOL &#40;-&#41; ](../../t-sql/statements/alter-resource-pool-transact-sql.md)陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
