---
title: 搭配 FOR XML 使用 AUTO 模式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e6464fee5779e35559b6eca23981aa09312aeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63193270"
---
# <a name="use-auto-mode-with-for-xml"></a>搭配 FOR XML 使用 AUTO 模式
  如同 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)中所述，AUTO 模式會將查詢結果當作巢狀 XML 元素傳回。 這對於從查詢結果產生出來的 XML 外觀，並未提供很大的控制權。 如果您想要產生簡單的階層，AUTO 模式查詢會很有用。 不過， [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md) 和 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md) 提供更多控制權和彈性來從查詢結果決定 XML 的形狀。  
  
 FROM 子句中的每個資料表都至少有一資料行是列在 SELECT 子句中，這些資料表是以 XML 元素表示。 若在 FOR XML 子句中指定選用性的 ELEMENTS 選項，SELECT 子句中所列的資料行就會對應至屬性或子元素。  
  
 所產生之 XML 中的 XML 階層 (巢狀元素)，是依據 SELECT 子句中指定資料行所識別的資料表順序。 因此，在 SELECT 子句中指定的資料行名稱順序是很重要的。 所識別的左邊第一個資料表，會形成所產生之 XML 文件的最上層元素。 由 SELECT 陳述式之資料行所識別的左邊第二個資料表，則形成最上層元素中的子元素，以此類推。  
  
 如果 SELECT 子句中列出的資料行名稱是來自 SELECT 子句先前指定之資料行所識別的資料表，這時會加入該資料行，做為已建立之元素的屬性，而不是開啟新的階層架構層級。 而如果指定了 ELEMENTS 選項，便會加入資料行做為屬性。  
  
 例如，執行以下的查詢：  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 以下是部份結果：  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 請注意 SELECT 子句中的下列各項：  
  
-   CustomerID 會參考 Cust 資料表。 因此，會建立 <`Cust`> 元素，並加入 CustomerID 做為其屬性。  
  
-   接著，OrderHeader.CustomerID、OrderHeader.SaleOrderID 及 OrderHeader.Status 這三個資料行會參考 OrderHeader 資料表。 因此，會加入 <`OrderHeader`> 元素做為 <`Cust`> 元素的子元素，並加入這三個資料行，做為 <`OrderHeader`> 的屬性。  
  
-   接下來，Cust.CustomerType 資料行又會參考已由 Cust.CustomerID 資料行所識別的 Cust 資料表。 因此並未建立任何新元素。 反之，會將 CustomerType 屬性加入先前所建立的 <`Cust`> 元素。  
  
-   查詢會為資料表名稱指定別名。 這些別名會以對應的元素名稱來顯示。  
  
-   若要將所有子系集合在一個父系之下，則需要 ORDER BY。  
  
 此查詢和上一個查詢類似，不同的是 SELECT 子句會將 OrderHeader 資料表中的資料行，指定在 Cust 資料表中的資料行之前。 因此，會先建立 <`OrderHeader`> 元素，然後再加入 <`Cust`> 子元素。  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 以下是部份結果：  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 若將 ELEMENTS 選項加入 FOR XML 子句，則會傳回元素中心的 XML。  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 以下是部份結果：  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 在此查詢中，建立 \<Cust> 項目時，會一一比較資料列中的 CustomerID 值，因為 CustomerID 是資料表的主索引鍵。 若未將 CustomerID 識別成資料表的主索引鍵，則會一一比較資料列中的所有資料行值 (在此查詢中是 CustomerID、CustomerType)。 若值有所差異，就會加入新的 \<Cust> 項目至 XML。  
  
 在比較這些資料行的值時，如果所要比較的任何資料行中具有 **text**、 **ntext**、 **image**或 **xml**類型，FOR XML 就會認定該值是不同的 (即使該值可能是相同的)，而不加以比較。 這是因為不支援比較大型物件。 針對所選取的每個資料列，都會將元素加入結果中。 請注意， **(n)varchar(max)** 及 **varbinary(max)** 的資料行會進行比較。  
  
 當 SELECT 子句中的資料行無法與 FROM 子句中所識別的任何資料表建立關聯 (例如：彙總資料行或計算資料行)，在清單中發現該資料行時，就會將其加入至最深之巢狀層級中的 XML 文件。 若該資料行是出現在 SELECT 子句中的第一個資料行，則會將該資料行新增至最上層元素。  
  
 若在 SELECT 子句中指定星號 (*) 萬用字元，就會根據查詢引擎所傳回的資料列順序，以上述同樣的方式來決定巢狀作業。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關 AUTO 模式的詳細資訊：  
  
-   [使用 BINARY BASE64 選項](use-the-binary-base64-option.md)  
  
-   [用來形成傳回之 XML 的 AUTO 模式啟發式方法](auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [範例：使用 AUTO 模式](examples-using-auto-mode.md)  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
