---
title: sys.databases pdw_diag_events （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 59bb3e9c-2829-49a0-b382-652ed1f54f88
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c103968698482c1d8845802173733b41f8ffede3
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87397138"
---
# <a name="syspdw_diag_events-transact-sql"></a>sys.databases pdw_diag_events （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  保存可包含在系統上診斷會話中之事件的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|特定診斷事件的名稱。||  
|**source**|**nvarchar(255)**|事件的來源（引擎、一般、dms 等等）||  
|**is_enabled**|**bit**|是否正在發行事件。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
