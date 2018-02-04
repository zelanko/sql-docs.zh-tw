---
title: "sys.pdw_table_distribution_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a192bc274c3d2bc6485c4642882809ee7f375035
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  儲存資料表的散發資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|指定屬性的三個資料表的識別碼。||  
|**distribution_policy**|**tinyint**|0 = 未定義<br /><br /> 1 = 無<br /><br /> 2 = HASH<br /><br /> 3 = 複寫<br /><br /> 4 = ROUND_ROBIN|REPLICATE 只適用於[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|  
|**distribution_policy_desc**|**nvarchar(60)**|未定義，無、 雜湊，複寫，SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 傳回雜湊或 REPLICATE。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
