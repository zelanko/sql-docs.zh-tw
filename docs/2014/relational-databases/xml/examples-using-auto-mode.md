---
title: 範例:使用 AUTO 模式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93a26764a7111a01b07d23c61bfbfb5c4a728e72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287813"
---
# <a name="examples-using-auto-mode"></a>範例:使用 AUTO 模式
  下列範例說明 AUTO 模式的用法。 這些查詢中有許多是針對自行車製造說明的 XML 文件來指定的，而這些文件儲存在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中 ProductModel 資料表的 Instructions 資料行中。  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>範例擷取客戶、 訂單及訂單詳細資訊  
 此查詢會擷取特定客戶的客戶、訂單及訂單詳細資訊。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 因為此查詢會識別 `Cust`、 `OrderHeader`、 `Detail`及 `Product` 資料表別名，所以 `AUTO` 模式會產生對應的元素。 而 `SELECT` 子句中指定之資料行所識別的資料表順序，會決定這些元素的階層。  
  
 以下是部份結果。  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>範例指定 GROUP BY 及彙總函式  
 下列查詢會傳回個別的客戶識別碼，以及客戶所要求的訂單數量。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>範例在 AUTO 模式中指定計算資料行  
 此查詢會傳回串連的個別客戶名稱及訂單資訊。 因為計算資料行指派給此時所發現的最內層 (在此範例中為 <`SOH`> 元素)， 因此在結果中，串連的客戶名稱會被當成 <`SOH`> 元素的屬性來加入。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 以下是部份結果：  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 若要擷取 <`IndividualCustomer`> 元素 (而其 `Name` 屬性中，包含每個銷售訂單的標頭資訊做為子元素)，使用子 Select 來重寫查詢。 內部的 Select 會建立暫存的 `IndividualCustomer` 資料表，且其中的計算資料行含有個別客戶的名稱。 接著此資料表會與 `SalesOrderHeader` 資料表聯結，以取得結果。  
  
 請注意， `Sales.Customer` 資料表會儲存個別客戶的資訊，包括該客戶的 `PersonID` 值。 然後再使用此 `PersonID` ，在 `Person.Person` 資料表中尋找連絡人名稱。  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 以下是部份結果：  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>範例傳回二進位資料  
 此查詢會從 `ProductPhoto` 資料表傳回產品相片。 `ThumbNailPhoto` 是 `ProductPhoto` 資料表中的 `varbinary(max)` 資料行。 依預設， `AUTO` 模式會傳回二進位資料的參考，此為執行查詢所在之資料庫虛擬根目錄的相對 URL。 您必須指定 `ProductPhotoID` 索引鍵屬性來識別影像。 如同此範例所說明，在擷取影像參考時，也必須在 `SELECT` 子句中指定資料表的主索引鍵，以識別具唯一性的資料列。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 以下是結果：  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 同樣的查詢，可以使用 `BINARY BASE64` 選項執行。 該查詢會以 Base64 編碼格式傳回二進位資料。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 以下是結果：  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 依預設，當您使用 AUTO 模式來擷取二進位資料時，將會傳回一個參考 (此為執行查詢所在之資料庫虛擬根目錄的相對 URL)，而不會傳回二進位資料。 若沒有指定 BINARY BASE64 選項，就會發生這種情形。  
  
 當 AUTO 模式針對不區分大小寫之資料庫中的二進位資料，傳回其 URL 參考，而查詢中所指定的資料表或資料行名稱並不符合資料庫中的資料表或資料行名稱時，查詢仍可執行。 不過，參考中所傳回的大小寫會不一致。 例如：  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 以下是結果：  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 這可能會是一個問題，尤其是在針對區分大小寫的資料庫執行 dbobject 查詢時。 為了避免發生這個問題，查詢中指定之資料表或資料行名稱的大小寫，應該要與資料庫中資料表或資料行名稱的大小寫相符。  
  
## <a name="example-understanding-the-encoding"></a>範例了解的編碼方式  
 此範例顯示結果中所出現的各種編碼方式。  
  
 建立下述資料表：  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 將下列資料加入資料表：  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 此查詢傳回來自於該資料表的資料。 並已指定 FOR XML AUTO 模式。 二進位資料是以參考來傳回。  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 以下是結果：  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 下述處理序是用來對結果中的特殊字元進行編碼：  
  
-   在查詢結果中，所傳回之元素及屬性名稱中的 XML 與 URL 特殊字元，是使用對應之 Unicode 字元的十六進位值來進行編碼。 在上述結果中，元素名稱 <`Special Chars`> 在傳回時會變成 <`Special_x0020_Chars`>。 屬性名稱 <`Col#&2`> 會以 <`Col_x0023__x0026_2`> 形式傳回。 XML 和 URL 特殊字元都會加以編碼。  
  
-   如果項目或屬性的值包含五種標準 XML 字元實體 ('、""、\<、> 及 &) 的其中任何一種，則一律都會使用 XML 字元編碼方式來將這些 XML 特殊字元編碼。 在上述結果中，<`Col1`> 屬性值中的 `&` 值會編碼成 `&`。 不過，# 字元仍保留為 #，因為它是有效的 XML 字元，並非特殊 XML 字元。  
  
-   如果元素或屬性的值包含任何於 URL 中是具有特殊意義的 URL 特殊字元，則只有位於 DBOBJECT URL 值內且當特殊字元為資料表或資料行名稱的一部分時，才會對這些字元進行編碼。 在結果中，屬於資料表名稱 `#` 一部分的 `Col#&2` 字元會被編碼成 `_x0023_ in the DBOJBECT URL`。  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 AUTO 模式](use-auto-mode-with-for-xml.md)  
  
  
