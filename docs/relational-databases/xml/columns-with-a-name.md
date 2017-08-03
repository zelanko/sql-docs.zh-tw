---
title: "有名稱的資料行 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3cda571a6e30387ccf1764e94fe6e6a3f1625262
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="columns-with-a-name"></a>有名稱的資料行
  以下是具有名稱的資料列集資料行，以區分大小寫的方式對應至產生之 XML 的特定條件：  
  
-   此資料行名稱以 @ 符號開頭。  
  
-   此資料行名稱不是以 @ 符號開頭。  
  
-   此資料行名稱不是以 @ 符號開頭且包含斜線 (/)。  
  
-   數個資料行共用相同的前置詞。  
  
-   一個資料行具有不同的名稱。  
  
## <a name="column-name-starts-with-an-at-sign-"></a>資料行名稱以 @ 符號開頭  
 如果資料行名稱是以 @ 符號開頭且不包含斜線 (/)，就會建立具有對應資料行值的 <`row`> 元素之屬性。 例如，下列查詢會傳回兩個資料行 (@PmId、Name) 的資料列集。 在產生的 XML 中，**PmId** 屬性會加入對應的 <`row`> 元素中，並會將 ProductModelID 值指派給該元素。  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 以下是結果：  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 請注意在相同的層級中，屬性必須在任何其他節點類型的前面，例如元素節點與文字節點。 下列查詢將傳回錯誤：  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>資料行名稱不是以 @ 符號開頭  
 如果資料行名稱不是以 At 符號 (@) 開頭、不是其中一個 XPath 節點測試，而且不包含斜線 (/)，預設會建立資料列元素 <`row`> 的子元素之 XML 元素。  
  
 下列查詢指定資料行名稱，也就是結果。 因此，<`result`> 子元素會加入 <`row`> 元素。  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 以下是結果：  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 下列查詢會針對 **xml** 類型的 Instructions 資料行指定之 XQuery 所傳回的 XML，指定資料行名稱 ManuWorkCenterInformation。 因此，將以 <`row`> 元素的子元素加入 <`ManuWorkCenterInformation`> 元素。  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 以下是結果：  
  
```  
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>資料行名稱不是以 @ 符號開頭且包含斜線 (/)  
 如果資料行名稱不是以 @ 符號開頭，但包含斜線 (/)，則資料行名稱會指出 XML 階層。 例如，如果資料行名稱是 "Name1/Name2/Name3.../Name***n*** "，則每個 Name***i*** 代表一個元素名稱，該元素以巢狀化方式出現在目前資料列元素 (for i=1) 中，或是在具有 Name***i-1***名稱之元素的底下。 如果 Name***n*** 以 '@' 開頭，它會對應至 Name***n-1*** 元素的屬性。  
  
 例如，下列查詢將會傳回員工識別碼與姓名，它們是以複雜的元素 EmpName 所代表，該元素包含姓名的 First、Middle 及 Last。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 該資料行名稱是在 PATH 模式中建構 XML 時當做路徑使用。 包含員工識別碼值的資料行名稱是以 '@' 開頭，因此會將 **EmpID** 屬性加入 <`row`> 元素。 在指出階層的資料行名稱中，所有其他的資料行都包含斜線 ('/')。 產生的 XML 在 <`row`> 元素底下將有 <`EmpName`> 子元素，而且 <`EmpName`> 子元素將有 <`First`>、<`Middle`> 及 <`Last`> 子元素。  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 員工中間名字為 Null，Null 值預設與缺少的元素或屬性相對應。 如果您要為 NULL 值產生元素，您可以指定具有 XSINL 的 ELEMENTS 指示詞，如下列查詢所示。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 以下是結果：  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 根據預設，PATH 模式會產生元素中心的 XML。 因此，在 PATH 模式查詢中指定 ELEMENTS 指示詞將不會有任何作用。 然而，如上述範例所示，ELEMENTS 指示詞加上 XSINIL 就可以為 Null 值產生元素。  
  
 除了識別碼與名稱之外，下列查詢還會擷取員工地址。 根據地址資料行之資料行名稱中的路徑，會將 <`Address`> 子元素加入 <`row`> 元素，而地址詳細資料則會以 <`Address`> 元素的子元素加入。  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 以下是結果：  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>數個資料行共用相同的路徑前置詞  
 如果數個後續的資料行共用相同的路徑前置詞，則會在相同的名稱下將它們群組在一起。 即使不同的命名空間前置詞是與相同的命名空間繫結，但仍使用了它們，就會將路徑視為不同。 在上述查詢中，FirstName、MiddleName 及 LastName 資料行是共用相同的 EmpName 前置詞。因此，會將它們以 <`EmpName`> 子元素加入。 當您在上述範例中建立 <`Address`> 元素時也是如此。  
  
## <a name="one-column-has-a-different-name"></a>一個資料行具有不同的名稱  
 如果具有不同名稱的資料行出現在其間，它將會拆散群組，如下列修改的查詢所示。 查詢會在 FirstName 與 MiddleName 資料行之間加入地址資料行，以拆散上述查詢所指定的 FirstName、MiddleName 及 LastName 的群組。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 因此，此查詢會建立兩個 <`EmpName`> 元素。 第一個 <`EmpName`> 元素具有 <`FirstName`> 子元素，而第二個 <`EmpName`> 元素則具有 <`MiddleName`> 及 <`LastName`> 子元素。  
  
 以下是結果：  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
