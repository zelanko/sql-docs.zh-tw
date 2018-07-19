---
title: syscollector_collection_items (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e1113453ebe83221fb8dd8b9de92113bcb346c3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220569"
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回收集組中某個項目的相關資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|識別收集組。 不可為 Null。|  
|**collection_item_id**|**int**|識別收集組中的項目。 不可為 Null。|  
|**collector_type_uid**|**uniqueidentifier**|用來識別收集器型別的 GUID。 不可為 Null。|  
|**name**|**nvarchar(4000)**|收集組的名稱。 可為 Null。|  
|**frequency**|**int**|收集項收集資料的頻率。 不可為 Null。|  
|**parameters**|**xml**|說明與收集項相關聯之收集器型別的參數化。 此收集項的 XML 結構描述驗證與 XML 結構描述 (XSD) 儲存在**parameter_schema**特定收集器類型。 可為 Null。 如需詳細資訊，請參閱[syscollector_collector_types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)。|  
  
## <a name="permissions"></a>Permissions  
 需要 SELECT **dc_operator**， **dc_proxy**。  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集器檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
