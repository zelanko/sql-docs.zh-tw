---
title: syscollector_collector_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41ae978e31db70f0cc49469d5ec14ae6f075ab7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760238"
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供收集項之收集器類型的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|集合類型的 GUID。 不可為 Null。|  
|**name**|**sysname**|集合類型的名稱。 不可為 Null。|  
|**parameter_schema**|**xml**|XML 結構描述，其中描述指定之收集器類型的組態內容。 這個 XML 結構描述是用來驗證與特定收集項執行個體相關聯的實際 XML 組態。 可為 Null。|  
|**parameter_formatter**|**xml**|判斷用來轉換 XML 的範本，以便能夠在收集組屬性頁中使用。 可為 Null。|  
|**collection_package_id**|**uniqueidentifer**|收集封裝的 GUID。 不可為 Null。|  
|**collection_package_path**|**nvarchar(4000)**|提供收集封裝的路徑。 可為 Null。|  
|**collection_package_name**|**sysname**|收集封裝的名稱。 不可為 Null。|  
|**upload_package_id**|**uniqueidentifer**|上傳封裝的 GUID。 不可為 Null。|  
|**upload_package_path**|**nvarchar(4000)**|提供上傳封裝的路徑。 可為 Null。|  
|**upload_package_name**|**sysname**|上傳封裝的名稱。 不可為 Null。|  
|**is_system**|**bit**|開啟 (1) 或關閉 (0) 表示如果收集器型別已隨附於資料收集器，或稍後藉由加入**dc_admin**。 這可能是本廠開發或由協力廠商開發的自訂類型。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要 SELECT **dc_operator**， **dc_proxy**。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|更新**collection_type_uid**資料行名稱**collector_type_uid&lt**。|  
|已更正的描述**parameter_schema**指出此值可為 null 的資料行。|  
|新增**parameter_formatter**資料行。|  
|已更正的資料類型**collection_package_path**資料行，並更新描述，指出此值可為 null。|  
|已更正的資料類型**upload_package_path**資料行，並更新描述，指出此值可為 null。|  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集器檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
