---
title: 類型系統（XQuery） |Microsoft Docs
description: 瞭解 XQuery 類型系統，其中包含內建類型的 XML 架構和 xpath 資料類型命名空間中定義的類型。
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
author: rothja
ms.author: jroth
ms.openlocfilehash: cb0b853b83fc65d8faddc341f9f0249debc2d2c1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915264"
---
# <a name="type-system-xquery"></a>類型系統 (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  XQuery 對結構描述類型而言是一個強式類型語言，對於不具類型的資料而言是一個弱式類型語言。 XQuery 的預先定義類型包括下列各項：  
  
-   命名空間中的內建 XML 架構類型 **http://www.w3.org/2001/XMLSchema** 。  
  
-   命名空間中定義的類型 **http://www.w3.org/2004/07/xpath-datatypes** 。  
  
 此主題也描述下列項目：  
  
-   具類型的值與節點的字串值。  
  
-   [Data 函數 &#40;xquery&#41;](../xquery/data-accessor-functions-data-xquery.md) ，而[String 函數 &#40;xquery&#41;](../xquery/data-accessor-functions-string-xquery.md)。  
  
-   比對運算式傳回的序列類型。  
  
## <a name="built-in-types-of-xml-schema"></a>XML 結構描述的內建類型  
 XML 結構描述的內建類型具有預先定義的命名空間前置詞 xs。 其中一些類型包含**xs： integer**和**xs： string**。 這些內建類型都受到支援。 當您建立 XML 結構描述集合時，可以使用這些類型。  
  
 查詢具類型的 XML 時，節點的靜態和動態類型是由被查詢的資料行或變數相關聯之 XML 結構描述集合所決定。 如需靜態和動態類型的詳細資訊，請參閱[運算式內容和查詢評估 &#40;XQuery&#41;](../xquery/expression-context-and-query-evaluation-xquery.md)。 例如，下列查詢是針對具類型的**xml**資料行（）所指定 `Instructions` 。 運算式使用 `instance of` 來確認所傳回之 `LotSize` 屬性的具類型值屬於 `xs:decimal` 類型。  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 此類型資訊是由資料行相關聯的 XML 結構描述集合所提供。  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>XPath 資料類型命名空間中定義的類型  
 命名空間中定義的類型 **http://www.w3.org/2004/07/xpath-datatypes** 具有預先定義的前置詞**xdt**。 下列適用於這些類型：  
  
-   當您建立 XML 結構描述集合時，不能使用這些類型。 這些類型會用於 XQuery 類型系統中，並用於[xquery 和靜態輸入](../xquery/xquery-and-static-typing.md)。 您可以在**xdt**命名空間中轉換成不可部分完成的類型，例如**xdt： untypedAtomic**。  
  
-   查詢不具類型的 XML 時，元素節點的靜態和動態類型是**xdt：** 不具類型，而屬性值的類型為**xdt： untypedAtomic**。 **Query （）** 方法的結果會產生不具類型的 XML。 這表示 XML 節點會分別傳回為**xdt：** 不具類型和**xdt： untypedAtomic**。  
  
-   不支援**xdt： dayTimeDuration**和**xdt： yearMonthDuration**類型。  
  
 在下列範例中，查詢是針對不具類型的 XML 變數所指定。 運算式 `data(/a[1]`) 會傳回含有一個不可部份完成值的序列。 `data()` 函數會傳回 `<a>` 元素的具類型值。 因為要查詢的 XML 不具類型，所以傳回的值類型是 `xdt:untypedAtomic`。 因此，`instance of` 傳回 true。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 下列範例中的運算式 (`/a[1]`) 不會擷取具類型值，而會傳回一個元素 (`<a>` 元素) 的序列。 `instance of` 運算式會使用元素測試來確認運算式傳回的值為 `xdt:untyped type` 的元素節點。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  若您是查詢具類型的 XML 執行個體且查詢運算式包含父軸，則結果節點的靜態類型資訊就無法再使用。 不過，動態類型仍與節點相關聯。  
  
## <a name="typed-value-vs-string-value"></a>具類型值與字串值  
 每一個節點都有一個具類型值和一個字串值。 若為具類型的 XML 資料，具類型值的類型是由被查詢的資料行或變數相關聯之 XML 結構描述集合來提供。 針對不具類型的 XML 資料，具類型值的類型是**xdt： untypedAtomic**。  
  
 您可以使用**data （）** 或**string （）** 函數來取出節點的值：  
  
-   [資料函數 &#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)會傳回節點的具類型值。  
  
-   [String 函數 &#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)會傳回節點的字串值。  
  
 在下列 XML 架構集合中， `root` 會定義整數類型的 <> 元素：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 在下列範例中，運算式會先擷取 `/root[1]` 的具類型值，然後再加 `3`。  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 在下一個範例中，運算式會失敗，因為運算式中的 `string(/root[1])` 會傳回字串類型值。 該值接著會傳遞給算術運算子，而此運算子只接受數值類型值做為其運算元。  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 下列範例計算 `LaborHours` 屬性的總計。 函 `data()` 式會 `LaborHours` 從產品型號的所有 <> 元素中，抓取屬性的具類型值 `Location` 。 根據與資料行相關聯的 XML 架構 `Instruction` ， `LaborHours` 是**xs： decimal**類型。  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 此查詢傳回的結果為 12.75。  
  
> [!NOTE]  
>  此範例中的**資料（）** 函數明確使用僅供說明之用。 如果未指定， **sum （）** 會隱含地套用**data （）** 函數，以解壓縮節點的具類型值。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery 基本概念](../xquery/xquery-basics.md)  
  
  
