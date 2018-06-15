---
title: sys.pdw_diag_sessions (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fa98b2980f226b515c5ae202eea0972326d998bc
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
ms.locfileid: "33698231"
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  會保留在系統建立的各種診斷工作階段的相關資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|在診斷工作階段的名稱。<br /><br /> 此檢視的索引鍵。||  
|**xml_data**|**nvarchar(4000)**|描述工作階段的 XML 裝載。||  
|**is_active**|**bit**|旗標，指出是否為作用中的旗標。||  
|**host_address**|**nvarchar(255)**|裝載工作階段定義 （控制節點） 的電腦的位址。||  
|**principal_id**|**int**|建立資料庫層級的工作階段的使用者識別碼。||  
|**database_id**|**int**|診斷工作階段範圍的資料庫識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
