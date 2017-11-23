---
title: "sys.resource_usage (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs: TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
caps.latest.revision: "15"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48a5b1046abf347c5a1239bbcd07c96da4476d98
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourceusage-azure-sql-database"></a>sys.resource_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  這項功能處於預覽狀態。 不要採用此功能的特定實作的相依性，因為在未來的版本中可能會變更或移除此功能。  
>   
>  處於預覽狀態時，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 作業小組可能會針對這個 DMV 關閉及開啟資料收集功能。  
>   
>  -   當開啟時，DMV 會傳回目前彙總的資料。  
> -   當關閉時，DMV 會傳回可能已過時的歷程記錄資料。  
  
 提供目前伺服器中使用者資料庫的資源使用狀況資料的每小時摘要。 歷程記錄資料會保留 90 天。  
  
 針對每個使用者資料庫，連續每個小時都會有一個資料列。 即使資料庫在某一小時期間是處於閒置狀態，還是會有一個資料列，而該資料庫的 usage_in_seconds 值將會是 0。 該小時的儲存使用量和 SKU 資訊則會適當地縮合起來。  
  
|資料行|資料類型|Description|  
|-------------|---------------|-----------------|  
|time|**datetime**|以每小時增加的時間 (UTC)。|  
|database_name|**nvarchar**|使用者資料庫的名稱。|  
|sku|**nvarchar**|SKU 的名稱。 以下是可能的值：<br /><br /> Web<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|某一小時內所使用的 CPU 時間總和。<br /><br /> 請注意： 此資料行 v11 已被取代，並不會套用至 V12。 **值一律設定為 0。**|  
|storage_in_megabytes|**decimal**|某一小時的最大儲存體大小，包括資料庫資料、索引、預存程序和中繼資料。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
  
