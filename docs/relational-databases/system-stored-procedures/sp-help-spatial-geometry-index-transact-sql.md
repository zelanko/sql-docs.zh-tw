---
description: sp_help_spatial_geometry_index (Transact-SQL)
title: sp_help_spatial_geometry_index (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e59df620f51de5a3e99ab759460c73eb517bd7cf
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810896"
---
# <a name="sp_help_spatial_geometry_index-transact-sql"></a>sp_help_spatial_geometry_index (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回關於 **幾何** 空間索引的指定屬性集的名稱和值。 結果會以資料表格式傳回。 您可以選擇傳回核心屬性集或索引的所有屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>引數  
 請參閱 [空間索引預存程式的引數和屬性](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 請參閱 [空間索引預存程式的引數和屬性](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="permissions"></a>權限  
 必須為使用者指派 PUBLIC 角色才能存取此程序。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在傳回集合中。  
  
## <a name="example"></a>範例  
 下列範例會使用 `sp_help_spatial_geometry_index` 來調查** \@ qs**中指定查詢範例在資料表**geometry_col**上定義的空間索引**SIndx_SpatialTable_geometry_col2** 。 這個範例只會傳回指定索引的核心屬性。  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>另請參閱  
 [空間索引預存程式](./spatial-index-stored-procedures-arguments-and-properties.md)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
