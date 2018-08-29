---
title: sp_help_spatial_geometry_index_xml (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1a166589b4544cf38709736ef45d30e383531d8e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036099"
---
# <a name="sphelpspatialgeometryindexxml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回有關的名稱和值的一組指定的屬性**幾何**空間索引。 您可以選擇傳回核心屬性集或索引的所有屬性。  
  
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
 請參閱[引數和屬性的空間索引預存程序](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="properties"></a>屬性  
 請參閱[引數和屬性的空間索引預存程序](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="permissions"></a>Permissions  
 使用者必須隸屬**公開**角色。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在 XML 傳回集合中。  
  
## <a name="example"></a>範例  
 下列範例會使用`sp_help_spatial_geometry_index_xml`來調查空間索引**SIndx_SpatialTable_geometry_col2**資料表上定義**geometry_col&lt**給定的查詢範例 **@qs**. 此範例以 XML 片段傳回指定索引的核心屬性，該片段會顯示所選取屬性的名稱和值。  
  
 [XQuery](../../xquery/xquery-basics.md)接著會在結果集，傳回特定的屬性上執行。  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 類似於[sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)，此預存程序提供較簡單的程式設計存取，空間索引的屬性，並報告中 XML 的結果集。  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [引數和屬性的空間索引預存程序](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [空間索引預存程序](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery 基本概念](../../xquery/xquery-basics.md)   
 [XQuery 語言參考](../../xquery/xquery-language-reference-sql-server.md)  
  
  
