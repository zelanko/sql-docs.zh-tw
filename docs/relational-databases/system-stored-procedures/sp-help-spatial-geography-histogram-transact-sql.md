---
description: sp_help_spatial_geography_histogram (Transact-SQL)
title: sp_help_spatial_geography_histogram (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0c7368b8991fe442cab30b724532e8899502e18f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809381"
---
# <a name="sp_help_spatial_geography_histogram-transact-sql"></a>sp_help_spatial_geography_histogram (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  協助您輸入空間索引的方格參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tabname = ] 'tabname'` 這是已指定空間索引之資料表的限定或非限定名稱。  
  
 只有在指定限定資料表時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *tabname* 是 **sysname**，沒有預設值。  
  
`[ @colname = ] 'columnname'` 這是指定的空間資料行名稱。 *columnname* 是 **sysname**，沒有預設值。  
  
`[ @resolution = ] 'resolution'` 是周框方塊的解析度。 有效的值是從 10 到 5000。 *解析度* 是 **Tinyint**，沒有預設值。  
  
`[ @sample = ] 'sample'` 這是使用的資料表百分比。 有效的值是從0到100。 *tablesample* 是 **浮點數**。 預設值為 100。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 會傳回資料表值。 下列方格描述資料表的資料行內容。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|代表每一個資料格的唯一識別碼，從 1 開始計數。|  
|**細胞**|**地理位置**|這是表示每個資料格的矩形多邊形。 資料格形狀與空間索引所使用的資料格形狀相同。|  
|**row_count**|**bigint**|指出觸及或包含資料格之空間物件的數目。|  
  
## <a name="permissions"></a>權限  
 使用者必須是 **public** 角色的成員。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 SSMS 空間索引標籤會顯示結果的圖形化表示。 您可以對空間視窗查詢結果，以取得結果項目的近似數目。  
  
> [!NOTE]  
>  資料表中的物件可能涵蓋一個以上的資料格，所以資料格的加總可能大於實際的物件數目。  
  
 **Geography**類型的周框方塊是整個地球。  
  
## <a name="examples"></a>範例  
 下列範例會在資料庫的資料表上呼叫  **sp_help_spatial_geography_histogram** `Person.Address` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 。  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的空間索引預存程式 ](./spatial-index-stored-procedures-arguments-and-properties.md)  
  
