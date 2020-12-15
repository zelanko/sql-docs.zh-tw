---
description: 'sys.pdw_health_components (Transact-sql) '
title: sys.pdw_health_components (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 84c5d002a357dd8780596d61d27b32088e659914
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479009"
---
# <a name="syspdw_health_components-transact-sql"></a>sys.pdw_health_components (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存存在於系統中的所有元件和裝置的相關資訊。 這些包括硬體、存放裝置和網路裝置。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|元件或裝置的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|group_id|**整數**|此元件所屬的邏輯元件群組。 請參閱 [sys.pdw_health_components (平行資料倉儲) ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|元件的名稱。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
