---
title: 使用 WITH XMLNAMESPACES 將命名空間新增至查詢 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 67ca4f1a0663b83eb4fe9cb1abfa2a1b609e2c56
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889564"
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>使用 WITH XMLNAMESPACES 將命名空間加入至查詢
  [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](/sql/t-sql/xml/with-xmlnamespaces) 會以下列方式支援命名空間 URI：  
  
-   它可以在 [使用 FOR XML 查詢建構 XML](for-xml-sql-server.md) 時，讓命名空間前置詞到 URI 的對應可供使用。  
  
-   它讓 [xml 資料類型方法](/sql/t-sql/xml/xml-data-type-methods)的靜態命名空間內容，有 URI 對應的命名空間可用。  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>在 FOR XML 查詢中使用 WITH XMLNAMESPACES  
 WITH XMLNAMESPACES 讓您可以在 FOR XML 查詢中包括 XML 命名空間。 例如，請看下列的 FOR XML 查詢：  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 以下是結果：  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 若要將命名空間加入到 FOR XML 查詢所建構的 XML 中，請先使用 WITH NAMESPACES 子句，指定命名空間前置詞到 URI 的對應。 接著，使用命名空間前置詞，在查詢中指定名稱，如下列修改過的查詢所示。 請注意，WITH XMLNAMESPACES 子句會指定命名空間前置詞 (`ns1`) 到 URI (`uri`) 的對應。 然後 `ns1` 前置詞會用來指定 FOR XML 查詢要建構的元素及屬性名稱。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 XML 結果會包括命名空間前置詞：  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 下列適用於 WITH XMLNAMESPACES 子句：  
  
-   只有 FOR XML 查詢的 RAW、AUTO 及 PATH 模式才支援。 不支援 EXPLICIT 模式。  
  
-   它只會影響 FOR XML 查詢的命名空間前置詞及 **xml** 資料類型方法，但不會影響 XML 剖析器。 例如，下列查詢會傳回錯誤，因為 XML 文件沒有 myNS 前置詞的命名空間宣告。  
  
-   如果正在使用 WITH XMLNAMESPACES 子句，就不能使用 FOR XML 指示詞、XMLSCHEMA 及 XMLDATA。  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>使用 XSINIL 指示詞  
 若您正在使用 ELEMENTS XSINIL 指示詞，就無法在 WITH XMLNAMESPACES 子句中定義 xsi 前置詞。 不過，它會在您使用 ELEMENTS XSINIL 時自動加入。 下列查詢會使用 ELEMENTS XSINIL，以產生元素中心的 XML，其中 Null 值會對應到 **xsi:nil** 屬性設為 True 的元素。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 以下是結果：  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>指定預設命名空間  
 您可以使用 DEFAULT 關鍵字來宣告預設的命名空間，而不需要宣告命名空間前置詞。 在 FOR XML 查詢中，它會將預設的命名空間繫結到產生之 XML 中的 XML 節點。 在下面的範例中，WITH XMLNAMESPACES 定義兩個連同預設命名空間一起定義的命名空間前置詞。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 此 FOR XML 查詢會產生元素中心的 XML。 請注意，此查詢在命名節點時兩個命名空間前置詞都會使用。 在 SELECT 子句中，ProductID、Name 及 Color 並未指定具有任何前置詞的名稱。 因此，產生之 XML 中的對應元素會隸屬於預設的命名空間。  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 下列查詢和前一個查詢很類似，差別只在下列查詢指定了 FOR XML AUTO 模式。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>使用預先定義的命名空間  
 使用預先定義的命名空間時，除了使用 ELEMENTS XSINIL 時的 xml 命名空間及 xsi 命名空間之外，您必須使用 WITH XMLNAMESPACES 明確地指定命名空間繫結。 下列查詢針對預先定義的命名空間 (`urn:schemas-microsoft-com:xml-sql`) 明確地定義了命名空間前置詞到 URI 的繫結。  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 以下是結果。 SQLXML 的使用者對這個 XML 範本很熟悉。 如需詳細資訊，請參閱 [SQLXML 4.0 程式設計概念](../sqlxml/sqlxml-4-0-programming-concepts.md)。  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 只有 xml 命名空間前置詞，不用在 WITH XMLNAMESPACES 中明確定義就可以使用，如以下 PATH 模式查詢中所示。 同時，若前置詞已經宣告了，就必須將它繫結到命名空間 http://www.w3.org/XML/1998/namespace。 SELECT 子句中指定的名稱會參考不是使用 WITH XMLNAMESPACES 明確定義的 xml 命名空間前置詞。  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 @xml:lang 屬性會使用預先定義的 XML 命名空間。 因為 XML 1.0 版不需要明確宣告 xml 命名空間繫結，所以結果不會包括命名空間繫結的明確宣告。  
  
 以下是結果：  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>將 WITH XMLNAMESPACES 搭配 xml 資料類型方法使用  
 在 SELECT 查詢中指定 [xml 資料類型方法](/sql/t-sql/xml/xml-data-type-methods) (或 UPDATE 中指定 **modify()** 方法) 時，全部都必須在其初構中重複命名空間宣告。 這可能會很費時。 例如，下列查詢會擷取其目錄描述確實包括規格的產品型號識別碼。 也就是說，有 <`Specifications`> 元素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 在上一個查詢中，**query()** 及 **exist()** 方法都在其初構中宣告了相同的命名空間。 例如：  
  
```  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 另外，您也可以先宣告 WITH XMLNAMESPACES，然後在查詢中使用命名空間前置詞。 在此情況中， **query()** 及 **exist()** 方法就不需要在初構中包含命名空間宣告。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 請注意，XQuery 初構中的明確宣告會覆寫命名空間前置詞，以及 WITH 子句中定義的預設元素命名空間。  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](/sql/t-sql/xml/xml-data-type-methods)   
 [XQuery 語言參考 &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server)   
 [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](/sql/t-sql/xml/with-xmlnamespaces)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
