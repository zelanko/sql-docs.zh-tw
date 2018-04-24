---
title: 使用巢狀 FOR XML 查詢 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], nested FOR XML
- nested FOR XML queries
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 59c5409b29be9b536042ded821c771ef14c7f868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="use-nested-for-xml-queries"></a>使用巢狀 FOR XML 查詢
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **xml** 資料類型和 [FOR XML 查詢中的 TYPE 指示詞](../../relational-databases/xml/type-directive-in-for-xml-queries.md) 可讓 FOR XML 查詢傳回的 XML 在伺服器以及用戶端上進行處理。  
  
## <a name="processing-with-xml-type-variables"></a>處理 xml 類型變數  
 您可以將 FOR XML 查詢結果指派給 **xml** 類型變數，或是使用 XQuery 以查詢結果，然後將那個結果指派給 **xml** 類型變數以進行其他處理。  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 使用其中一種 `@x`xml **資料類型方法，您就可以額外處理以變數** 傳回的 XML。 例如，您可以使用 `ProductModelID` value() 方法 [來擷取](../../t-sql/xml/value-method-xml-data-type.md)屬性值。  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 在下列範例中，因為已在 `FOR XML` 子句中指定 **指示詞，所以傳回的** 查詢結果為 `TYPE` xml `FOR XML` 類型。  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 以下是結果：  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 因為結果為 **xml** 類型，所以您可以直接對此 XML 指定其中一個 **xml** 資料類型方法，如以下查詢所示。 在查詢中，會使用 [query() 方法 (xml 資料類型)](../../t-sql/xml/query-method-xml-data-type.md) 來擷取 <`myRoot`> 元素的第一個 <`row`> 元素子項。  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 以下是結果：  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## <a name="returning-inner-for-xml-query-results-to-outer-queries-as-xml-type-instances"></a>將內部 FOR XML 查詢結果當做 xml 類型執行個體傳回給外部查詢  
 您可以撰寫巢狀 `FOR XML` 查詢，其中的內部查詢結果會以 **xml** 類型傳回給外部查詢。 例如：  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   以內部 `FOR XML` 查詢產生的 XML 會加入至外部 `FOR XML`產生的 XML 中。  
  
-   內部查詢指定了 `TYPE` 指示詞。 因此，內部查詢所傳回的 XML 資料為 **xml** 類型。 如果未指定 TYPE 指示詞，則會以 `FOR XML` nvarchar(max) **傳回內部** 查詢的結果，並實體化 XML 資料。  
  
## <a name="controlling-the-shape-of-resulting-xml-data"></a>控制產生之 XML 資料的外觀  
 巢狀 FOR XML 查詢可讓您有更多的控制權，以定義所產生之 XML 資料的外觀。 您可以使用 FOR XML 查詢來建構部分為屬性中心、部分為元素中心的 XML。  
  
 如需使用巢狀 FOR XML 查詢指定屬性中心及元素中心之 XML 的詳細資訊，請參閱 [與巢狀 FOR XML 查詢比較的 FOR XML 查詢](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md) 和 [使用巢狀 FOR XML 查詢組成 XML](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)。  
  
 您可以指定巢狀 AUTO 模式 FOR XML 查詢來產生含有同層級的 XML 階層。 如需詳細資訊，請參閱 [使用巢狀 AUTO 模式查詢產生同層級](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)。  
  
 不論您使用的模式為何，巢狀 FOR XML 查詢都能提供更多的控制權以描述所產生 XML 的形狀。 它們可用來取代 EXPLICIT 模式查詢。  
  
## <a name="examples"></a>範例  
 下列主題將提供巢狀 FOR XML 查詢的範例。  
  
 [與巢狀 FOR XML 查詢比較的 FOR XML 查詢](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 將單一層 FOR XML 查詢與巢狀 FOR XML 查詢做比較。 此範例包含一個示範，說明如何同時將屬性中心和元素中心 XML 指定為查詢的結果。  
  
 [使用巢狀 AUTO 模式查詢產生同層級](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 示範如何使用巢狀 AUTO 模式查詢產生同層級  
  
 [在 ASP.NET 中使用巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries-in-asp-net.md)  
 示範 ASPX 應用程式如何使用 FOR XML，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中傳回 XML。  
  
 [使用巢狀 FOR XML 查詢組成 XML](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)  
 示範如何使用巢狀 FOR XML 查詢，以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立之 XML 文件的結構。  
  
  
