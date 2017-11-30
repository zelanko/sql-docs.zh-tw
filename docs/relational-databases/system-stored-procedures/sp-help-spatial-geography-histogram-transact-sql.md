---
title: "sp_help_spatial_geography_histogram (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs: TSQL
helpviewer_keywords: sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c65b21ab76c3ca5880c709e09255ad083ad05def
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpspatialgeographyhistogram-transact-sql"></a>sp_help_spatial_geography_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  協助您輸入空間索引的方格參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@tabname =**] **'***tabname***'**  
 這是已指定空間索引之資料表的限定或非限定名稱。  
  
 只有在指定限定資料表時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *tabname*是**sysname**，沒有預設值。  
  
 [  **@colname =** ] **'***columnname***'**  
 這是所指定之空間資料行的名稱。 *columnname*是**sysname**，沒有預設值。  
  
 [  **@resolution =** ] **'***解析***'**  
 這是週框方塊的解析度。 有效的值是從 10 到 5000。 *解析*是**tinyint**，沒有預設值。  
  
 [  **@sample =** ] **'***範例***'**  
 這是所用之資料表的百分比。 有效值介於 0 到 100 之間。 *tablesample*是**float**。 預設值為 100。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 會傳回資料表值。 下列方格描述資料表的資料行內容。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|代表每一個資料格的唯一識別碼，從 1 開始計數。|  
|**資料格**|**地理位置**|這是表示每個資料格的矩形多邊形。 資料格形狀與空間索引所使用的資料格形狀相同。|  
|**row_count**|**bigint**|指出觸及或包含資料格之空間物件的數目。|  
  
## <a name="permissions"></a>Permissions  
 使用者必須是成員**公用**角色。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 SSMS 空間索引標籤會顯示結果的圖形化表示。 您可以對空間視窗查詢結果，以取得結果項目的近似數目。  
  
> [!NOTE]  
>  資料表中的物件可能涵蓋一個以上的資料格，所以資料格的加總可能大於實際的物件數目。  
  
 週框方塊**geography**型別是整個地球。  
  
## <a name="examples"></a>範例  
 下列範例會呼叫**sp_help_spatial_geography_histogram**上`Person.Address`資料表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>請參閱  
 [空間索引預存程序 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
