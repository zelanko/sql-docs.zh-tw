---
title: sys.pdw_diag_sessions (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bd48648719e04ca1eec15c4594b08cc1d40505b9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028629"
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  會保留在系統已建立的各種診斷工作階段的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|診斷工作階段的名稱。<br /><br /> 此檢視的索引鍵。||  
|**xml_data**|**nvarchar(4000)**|描述工作階段的 XML 承載。||  
|**is_active**|**bit**|旗標，指出是否為作用中的旗標。||  
|**host_address**|**nvarchar(255)**|裝載的工作階段定義 （位於 [控制] 節點） 的電腦位址。||  
|**principal_id**|**int**|建立資料庫層級的工作階段的使用者識別碼。||  
|**database_id**|**int**|診斷工作階段範圍的資料庫識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
