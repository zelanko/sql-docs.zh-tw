---
title: sys.databases pdw_diag_sessions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fa06005679e31381f723b30b9f68e5ce0d89ae1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127693"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys.databases pdw_diag_sessions （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存有關系統上所建立之各種診斷會話的資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|診斷會話的名稱。<br /><br /> 此視圖的索引鍵。||  
|**xml_data**|**nvarchar(4000)**|描述會話的 XML 內容。||  
|**is_active**|**bit**|表示旗標是否作用中的旗標。||  
|**host_address**|**nvarchar(255)**|裝載會話定義之電腦的位址（控制節點）。||  
|**principal_id**|**int**|在資料庫層級建立會話之使用者的識別碼。||  
|**database_id**|**int**|屬於診斷會話範圍之資料庫的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
