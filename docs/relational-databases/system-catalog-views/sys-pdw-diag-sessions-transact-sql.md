---
description: 'sys.pdw_diag_sessions (Transact-sql) '
title: sys.pdw_diag_sessions (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: e8fade6ec60ada411ee78027d01f9616e499f755
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036741"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  保存有關系統上已建立之各種診斷會話的資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|診斷會話的名稱。<br /><br /> 此視圖的索引鍵。||  
|**xml_data**|**nvarchar(4000)**|描述會話的 XML 裝載。||  
|**is_active**|**bit**|指出旗標是否為作用中的旗標。||  
|**host_address**|**nvarchar(255)**|裝載會話定義 (控制節點) 的電腦位址。||  
|**principal_id**|**int**|在資料庫層級建立會話之使用者的識別碼。||  
|**database_id**|**int**|屬於診斷會話範圍的資料庫識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
