---
title: sys.databases pdw_health_components （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83bea79a009e25d54f9d0ae589936de7fed7d94a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396027"
---
# <a name="syspdw_health_components-transact-sql"></a>sys.databases pdw_health_components （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存存在於系統中之所有元件和裝置的相關資訊。 其中包括硬體、存放裝置和網路裝置。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|元件或裝置的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|group_id|**整數**|此元件所屬的邏輯元件群組。 請參閱[sys.databases pdw_health_components （平行處理資料倉儲）](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|元件的名稱。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
