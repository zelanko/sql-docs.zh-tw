---
title: "xml (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs: TSQL
helpviewer_keywords: xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b738180bbf6b2f3f18bbd38ebfe7139736f33cee
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這是儲存 XML 資料的資料類型。 您可以儲存**xml**中資料行或變數的執行個體**xml**型別。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>引數  
 CONTENT  
 限制**xml**是語式正確的 XML 片段的執行個體。 XML 資料可以在最上層包含多個零或更多元素。 最上層也可以有文字節點。  
  
 這是預設行為。  
  
 DOCUMENT  
 限制**xml**是語式正確的 XML 文件的執行個體。 XML 資料必須也只能有一個根元素。 最上層不能有文字節點。  
  
 *xml_schema_collection*  
 這是 XML 結構描述集合的名稱。 若要建立具類型**xml**資料行或變數，您可以選擇性地指定 XML 結構描述集合名稱。 詳細資訊關於輸入與不具類型的 XML，請參閱[比較具類型的 XML 與不具類型 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="remarks"></a>備註  
 預存的表示法**xml**資料類型執行個體不能超過 2 gb 的大小。  
  
 CONTENT 和 DOCUMENT Facet 只適用於具類型的 XML。 如需詳細資訊，請參閱[比較具類型的 XML 與不具類型 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="examples"></a>範例  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @y xml (Sales.IndividualSurveySchemaCollection);  
SET @y =  (SELECT TOP 1 Demographics FROM Sales.Individual);  
SELECT @y;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型轉換 &#40; Database Engine &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
