---
title: xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66e49e14785f3e99bde79c1de987ea5ac38d06d2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754797"
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  這是儲存 XML 資料的資料類型。 您可以將 **xml** 執行個體儲存在資料行或 **xml** 類型的變數中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>引數  
 CONTENT  
 將 **xml** 執行個體限制為格式正確的 XML 片段。 XML 資料可以在最上層包含多個零或更多元素。 最上層也可以有文字節點。  
  
 此為預設行為。  
  
 DOCUMENT  
 將 **xml** 執行個體限制為格式正確的 XML 文件。 XML 資料必須也只能有一個根元素。 最上層不能有文字節點。  
  
 *xml_schema_collection*  
 這是 XML 結構描述集合的名稱。 若要建立具類型的 **xml** 資料行或變數，您可以選擇性指定 XML 結構描述集合名稱。 如需具類型和不具類型之 XML 的詳細資訊，請參閱[比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="remarks"></a>備註  
 **xml** 資料類型執行個體的預存表示法大小不得超過 2 GB。  
  
 CONTENT 和 DOCUMENT Facet 只適用於具類型的 XML。 如需詳細資訊，請參閱[比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="examples"></a>範例  
  
```  
USE AdventureWorks;  
GO  
DECLARE @DemographicData xml (Person.IndividualSurveySchemaCollection);  
SET @DemographicData =  (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
