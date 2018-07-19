---
title: sys.pdw_column_distribution_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f3c34825e8bdc8e1e1947575894596c3c1897ddb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000950"
---
# <a name="syspdwcolumndistributionproperties-transact-sql"></a>sys.pdw_column_distribution_properties & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留資料行的散發資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|資料行所屬的物件識別碼。||  
|**column_id**|**int**|資料行的識別碼。||  
|**distribution_ordinal**|**tinyint**|（以 1 為基礎） 組中的序數發佈。|0 = 不是散發資料行。 1 =[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]將父資料表中使用此資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
