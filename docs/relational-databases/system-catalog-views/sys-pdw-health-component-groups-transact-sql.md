---
description: 'sys.pdw_health_component_groups (Transact-sql) '
title: sys.pdw_health_component_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 552a4b28187687c21312c5918788eaf85e799597
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464629"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys.pdw_health_component_groups (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存元件和裝置邏輯群組的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|元件和裝置的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|group_name|**nvarchar(255)**|元件和裝置的邏輯組名稱。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
