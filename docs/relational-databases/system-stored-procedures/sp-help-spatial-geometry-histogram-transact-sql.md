---
title: sp_help_spatial_geometry_histogram (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_histogram
- sp_help_spatial_geometry_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_histogram
ms.assetid: 036aaf61-df3e-40f7-aa4e-62983c5a37bd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 640d292dfbef7adae9fc99b53cb3b450f698b651
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085117"
---
# <a name="sphelpspatialgeometryhistogram-transact-sql"></a>sp_help_spatial_geometry_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  協助您輸入空間索引的週框方塊和格線參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geometry_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @xmin = ] 'minx' ]   
     [ , [ @ymin = ] 'miny' ]   
     [ ,.[ @xmax = ] 'maxx' ]  
     [ , [ @ymax = ] 'maxy' ]  
     [ , [ @sample = ] 'sample' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tabname = ] 'tabname'` 是已指定空間索引之資料表的完整或非完整名稱。  
  
 只有在指定限定資料表時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *tabname*已**sysname**，沒有預設值。  
  
`[ @colname = ] 'colname'` 是指定之空間資料行的名稱。 *colname*已**sysname**，沒有預設值。  
  
`[ @resolution = ] 'resolution'` 是週框方塊的解析度。 有效的值是從 10 到 5000。 *解析度*已**tinyint**，沒有預設值。  
  
`[ @xmin = ] 'xmin'` 是 X 最小值週框方塊屬性。 *xmin*已**float**，沒有預設值。  
  
`[ @ymin = ] 'ymin'` 是 Y 最小值週框方塊屬性。 *ymin*已**float**，沒有預設值。  
  
`[ @xmax = ] 'xmax'` 是 X 最大值週框方塊屬性。 *xmax*已**float**，沒有預設值。  
  
`[ @ymax = ] 'ymax'` 是 Y 最大值週框方塊屬性。 *ymax*已**float**，沒有預設值。  
  
`[ @sample = ] 'sample'` 為資料表所使用的百分比。 有效的值是從 0 到 100 之間。 *範例*已**float**。 預設值為 100。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 會傳回資料表值。 下列方格描述資料表的資料行內容。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|代表每一個資料格的唯一識別碼，從 1 開始計算。|  
|**cell**|**幾何**|這是表示每個資料格的矩形多邊形。 資料格形狀與空間索引所使用的資料格形狀相同。|  
|**row_count**|**bigint**|指出觸及或包含資料格之空間物件的數目。|  
  
## <a name="permissions"></a>Permissions  
 使用者必須隸屬**公開**角色。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 SSMS 空間索引標籤會顯示結果的圖形化表示。 您可以對空間視窗查詢結果，以取得結果項目的近似數目。 資料表中的物件可能涵蓋一個以上的資料格，所以資料格的加總可能大於實際的物件數目。  
  
 結果集內可能會加入額外的資料列，以保留週框方塊之外或觸及週框方塊框線的物件數目。 **Cellid**此資料列的是 0，**資料格**這個資料列包含**LineString**表示週框方塊。 這個資料列代表週框方塊外的整個空間。  
  
## <a name="examples"></a>範例  
 下列範例會建立範例資料表，然後呼叫**sp_help_spatial_geometry_histogram**資料表上。  
  
 `USE AdventureWorksDW2012`  
  
 `GO`  
  
 `-- Set database compatibility for circular arc segments`  
  
 `ALTER DATABASE AdventureWorksDW2012`  
  
 `SET COMPATIBILITY_LEVEL = 110;`  
  
 `GO`  
  
 `-- Create table to execute sp_help_spatial_geometry_histogram on`  
  
 `CREATE TABLE TownSites`  
  
 `(`  
  
 `Location geometry NULL,`  
  
 `SiteName nvarchar(50) NULL`  
  
 `)`  
  
 `GO`  
  
 `-- Insert site data into table`  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('POINT(0 0)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Booth Map';`  
  
 `SET @g = geometry::Parse('POLYGON((1 1, 1 2, 2 2, 2 1, 1 1))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Town Hall';`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-1 0, 0 -1, 1 0),(1 0, 1 2, -1 0)))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Park';`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(1 5, 2 2, 5 1)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Road';`  
  
 `-- Call proc to see data within bounding box`  
  
 `EXEC sp_help_spatial_geometry_histogram @tabname = TownSites, @colname = Location, @resolution = 64, @xmin = -2, @ymin = -2, @xmax = 3, @ymax = 3, @sample = 100;`  
  
 `GO`  
  
 `DROP TABLE TownSites;`  
  
 `GO`  
  
## <a name="see-also"></a>另請參閱  
 [空間索引預存程序&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
