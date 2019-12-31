---
title: sys.databases pdw_table_distribution_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 43974e2ae8becb5ad24daf0c52246a71c890bce2
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822159"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>sys.databases pdw_table_distribution_properties （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存資料表的散發資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|已指定三個屬性之資料表的識別碼。||  
|**distribution_policy**|**Tinyint**|0 = 未定義<br /><br /> 1 = 無<br /><br /> 2 = 雜湊<br /><br /> 3 = 複寫<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**Nvarchar （60）**|未定義、無、雜湊、複寫、ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]傳回雜湊、ROUND_ROBIN 或複寫。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
