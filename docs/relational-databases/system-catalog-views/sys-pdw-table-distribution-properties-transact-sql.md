---
description: 'sys. pdw_table_distribution_properties (Transact-sql) '
title: sys. pdw_table_distribution_properties (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 580ce1c29f8c788e23cac3d2c78edf164118cb6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475323"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>sys. pdw_table_distribution_properties (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存資料表的散發資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|指定模型下列屬性之資料表的識別碼。||  
|**distribution_policy**|**tinyint**|0 = 未定義<br /><br /> 1 = 無<br /><br /> 2 = 雜湊<br /><br /> 3 = 複寫<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**nvarchar(60)**|未定義、無、雜湊、複寫、ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 傳回 HASH、ROUND_ROBIN 或複寫。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
