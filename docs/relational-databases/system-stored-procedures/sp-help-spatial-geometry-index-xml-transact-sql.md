---
description: sp_help_spatial_geometry_index_xml (Transact-SQL)
title: sp_help_spatial_geometry_index_xml (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7bc4e0df3bfcffa7bdfd84b681c33ed179af75b9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546053"
---
# <a name="sp_help_spatial_geometry_index_xml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回關於 **幾何** 空間索引的指定屬性集的名稱和值。 您可以選擇傳回核心屬性集或索引的所有屬性。  
  
 結果會以 XML 片段傳回，該片段會顯示所選取屬性的名稱和值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ]'{ 0 | 1 }]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>引數  
 請參閱 [空間索引預存程式的引數和屬性](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="properties"></a>屬性  
 請參閱 [空間索引預存程式的引數和屬性](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="permissions"></a>權限  
 使用者必須是 **public** 角色的成員。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在 XML 傳回集合中。  
  
## <a name="example"></a>範例  
 下列範例會使用 `sp_help_spatial_geometry_index_xml` 來調查** \@ qs**中指定查詢範例在資料表**geometry_col**上定義的空間索引**SIndx_SpatialTable_geometry_col2** 。 此範例以 XML 片段傳回指定索引的核心屬性，該片段會顯示所選取屬性的名稱和值。  
  
 然後，會在結果集上執行 [XQuery](../../xquery/xquery-basics.md) ，傳回特定屬性。  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 類似于 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)，此預存程式可讓您以程式設計方式存取空間索引的屬性，並以 XML 報告結果集。  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [空間索引預存程式的引數和屬性](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [空間索引預存程式](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery 基本概念](../../xquery/xquery-basics.md)   
 [XQuery 語言參考](../../xquery/xquery-language-reference-sql-server.md)  
  
  
