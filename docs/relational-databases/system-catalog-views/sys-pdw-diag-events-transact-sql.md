---
description: 'sys.pdw_diag_events (Transact-sql) '
title: sys.pdw_diag_events (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 68cdc1013969dde85bbdc0bded31610a1673b91d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461609"
---
# <a name="syspdw_diag_events-transact-sql"></a>sys.pdw_diag_events (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  保存有關可包含在系統上診斷會話中之事件的資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|特定診斷事件的名稱。||  
|**source**|**nvarchar(255)**|事件 (引擎、一般、dms 等 ) 的來源||  
|**is_enabled**|**bit**|是否正在發佈事件。||  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
