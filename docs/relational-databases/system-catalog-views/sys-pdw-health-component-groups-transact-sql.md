---
description: 'sys. pdw_health_component_groups (Transact-sql) '
title: sys. pdw_health_component_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a327506fbfe71aa7473669bd63f7c4aec147fd7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490266"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys. pdw_health_component_groups (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存元件和裝置邏輯群組的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|元件和裝置的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|group_name|**nvarchar(255)**|元件和裝置的邏輯組名稱。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
