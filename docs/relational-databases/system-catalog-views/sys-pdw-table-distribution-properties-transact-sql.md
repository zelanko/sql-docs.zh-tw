---
title: sys.pdw_table_distribution_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f3d36e538777ba11ffdf66d0c9d9ff5271709802
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993840"
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  會保留資料表的散發資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|指定屬性的三個資料表的識別碼。||  
|**distribution_policy**|**tinyint**|0 = 未定義<br /><br /> 1 = 無<br /><br /> 2 = 雜湊<br /><br /> 3 = 複寫<br /><br /> 4 = ROUND_ROBIN|REPLICATE 只適用於[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|  
|**distribution_policy_desc**|**nvarchar(60)**|未定義，NONE、 雜湊，複寫，SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 傳回雜湊或複寫。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
