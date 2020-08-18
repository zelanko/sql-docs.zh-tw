---
description: 'sys. pdw_health_components (Transact-sql) '
title: sys. pdw_health_components (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 74b741d94d5e9a10c4b657cfbe70ad69f9cbbfa1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400764"
---
# <a name="syspdw_health_components-transact-sql"></a>sys. pdw_health_components (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存存在於系統中的所有元件和裝置的相關資訊。 這些包括硬體、存放裝置和網路裝置。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|元件或裝置的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|group_id|**整數**|此元件所屬的邏輯元件群組。 請參閱 [sys. pdw_health_components (平行資料倉儲) ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|元件的名稱。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
