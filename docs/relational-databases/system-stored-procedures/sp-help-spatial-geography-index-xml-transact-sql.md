---
title: "sp_help_spatial_geography_index_xml (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffc4f49e8087189e9fd7d364d4d9ee3cc668573a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpspatialgeographyindexxml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  名稱和指定的屬性集的值會傳回有關**geography**空間索引。 您可以選擇傳回核心屬性集或索引的所有屬性。  
  
 結果會以 XML 片段傳回，該片段會顯示所選取屬性的名稱和值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>引數  
 請參閱[引數和屬性的空間索引預存程序](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="properties"></a>屬性  
 請參閱[引數和屬性的空間索引預存程序](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)。  
  
## <a name="permissions"></a>Permissions  
 必須為使用者指派 PUBLIC 角色才能存取此程序。 需要在伺服器和物件上具有 READ ACCESS 權限。  
  
## <a name="remarks"></a>備註  
 包含 NULL 值的屬性不會包含在傳回集合中。  
  
## <a name="example"></a>範例  
 下列範例會使用`sp_help_spatial_geography_index_xml`來調查空間索引**SIndx_SpatialTable_geography_col2**資料表上定義**該索引是針對**的給定的查詢範例**@qs**. 此範例以 XML 片段傳回指定索引的核心屬性，該片段會顯示所選取屬性的名稱和值。  
  
 [XQuery](../../xquery/xquery-basics.md)接著會在結果集，傳回特定的屬性上執行。  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 類似於[sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)，此預存程序提供簡單的屬性以程式設計方式存取**geography**空間索引，並報告中 XML 的結果集。  
  
 週框方塊的**geography**是整個地球。  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>請參閱  
 [空間索引預存程序](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間資料 &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery 基本概念](../../xquery/xquery-basics.md)   
 [XQuery 語言參考](../../xquery/xquery-language-reference-sql-server.md)  
  
  
