---
description: sys.syscharsets (Transact-SQL)
title: sys.sys字元集 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47e839f090a3a7420a3da01cb4d468d3da667314
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88399694"
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對每個定義給 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 使用的字元集和排序順序，各包含一個資料列。 其中一個排序次序會在 **sysconfigures** 中標示為預設排序次序。 這是實際使用的排序順序。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**type**|**smallint**|這個資料列所代表的實體類型：<br /><br /> 1001 = 字元集。<br /><br /> 2001 = 排序順序。|  
|**id**|**tinyint**|字元集或排序順序的唯一識別碼。 請注意，排序順序和字元集不能共用相同的識別碼。 1 至 240 的識別碼範圍保留給 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用。|  
|**csid**|**tinyint**|如果資料列代表字元集，就不會使用這個欄位。 如果資料列代表排序順序，這個欄位就是用來建置排序順序的字元集識別碼。 假設這份資料表有這個識別碼的字元集資料列存在。|  
|**status**|**smallint**|內部系統狀態資訊位元。|  
|**name**|**sysname**|字元集或排序順序的唯一名稱。 這個欄位只能包含字母 A-Z 或 a-z、數字 0 - 9 和底線 (_)；它的開頭必須是字母。|  
|**description**|**nvarchar(255)**|字元集或排序順序功能的選擇性描述。|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**definition**|**image**|字元集或排序順序的內部定義。 這個欄位的資料結構會隨著類型而不同。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;將系統資料表對應至系統檢視 ](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
