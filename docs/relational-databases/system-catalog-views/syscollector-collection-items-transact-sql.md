---
title: syscollector_collection_items （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f775d96b0bc56217f1400021e6c51b62d2886e5f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899957"
---
# <a name="syscollector_collection_items-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回收集組中某個項目的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|識別收集組。 不可為 Null。|  
|**collection_item_id**|**int**|識別收集組中的項目。 不可為 Null。|  
|**collector_type_uid**|**uniqueidentifier**|用來識別收集器型別的 GUID。 不可為 Null。|  
|**name**|**nvarchar(4000)**|收集組的名稱。 可為 Null。|  
|**frequency**|**int**|收集項收集資料的頻率。 不可為 Null。|  
|**parameters**|**xml**|說明與收集項相關聯之收集器型別的參數化。 這個收集項的 XML 架構會使用儲存在**parameter_schema**中的 xml 架構（XSD）來進行驗證，以取得特定的收集器型別。 可為 Null。 如需詳細資訊，請參閱[syscollector_collector_types &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)。|  
  
## <a name="permissions"></a>權限  
 需要 SELECT for **dc_operator**， **dc_proxy**。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料收集器預存程式](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料收集器視圖](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
