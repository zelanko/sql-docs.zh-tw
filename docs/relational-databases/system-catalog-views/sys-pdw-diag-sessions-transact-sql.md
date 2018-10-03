---
title: sys.pdw_diag_sessions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a61d85c607824420f69c48fa1a84e5d8435a1f85
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662756"
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
  
  
