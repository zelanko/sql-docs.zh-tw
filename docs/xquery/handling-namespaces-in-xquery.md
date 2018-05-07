---
title: 處理 XQuery 中的命名空間 |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
caps.latest.revision: 24
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4602c1234c00b15191ca616ed56352f0eb784d9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handling-namespaces-in-xquery"></a>處理 XQuery 中的命名空間
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  這個主題所提供的範例將說明如何處理查詢中的命名空間。  
  
## <a name="examples"></a>範例  
  
### <a name="a-declaring-a-namespace"></a>A. 宣告命名空間  
 下列查詢會擷取特定產品型號的製造步驟。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 以下是部份結果：  
  
```  
<AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
…  
```  
  
 請注意，**命名空間**關鍵字用來定義新的命名空間前置詞"AWMI:"。 接著，必須針對所有落在該命名空間範圍中的元素，在查詢中使用此前置詞。  
  
### <a name="b-declaring-a-default-namespace"></a>B. 宣告預設命名空間  
 在上一個查詢中，已經定義了新的命名空間前置詞。 接著，必須在查詢中使用該前置詞，以選取所要的 XML 結構。 此外，您也可以將命名空間宣告為預設命名空間，如下列修改過的查詢中所示：  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是結果：  
  
```  
<step xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
…  
```  
  
 請注意，在此範例中，所定義的命名空間 (`"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`) 會覆寫預設或空的命名空間。 因此，用來進行查詢的路徑運算式中已沒有命名空間前置詞。 結果中出現的元素名稱也不再有命名空間前置詞。 此外，預設命名空間會套用到所有的元素，但不會套用到元素的屬性。  
  
### <a name="c-using-namespaces-in-xml-construction"></a>C. 在 XML 建構中使用命名空間  
 當您定義新的命名空間時，它們不僅會納入查詢的範圍，也會納入建構的範圍中。 例如，在建構 XML 時，您可以使用 "`declare namespace ...`" 宣告來定義新的命名空間，然後將該命名空間用於您所建構的任何元素與屬性，以便顯示於查詢結果中。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 以下是結果：  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 此外，您也可以在每個將命名空間做為部份 XML 建構來使用的位置，明確地定義命名空間，如下列查詢所示：  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>D. 使用預設命名空間的建構  
 您也可以定義要用於所建構之 XML 的預設命名空間。 例如，下列查詢會示範如何指定預設命名空間"uri: somenamespace"\\，若要使用預設值做為建構，例如本機具名元素`<Result>`項目。  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 以下是結果：  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 請注意，若覆寫預設元素命名空間或空的命名空間，所建構的 XML 中所有的本機具名元素之後都會繫結到執行覆寫的預設命名空間。 因此，若您想在建構 XML 時保有運用空命名空間的彈性，請不要覆寫預設元素命名空間。  
  
## <a name="see-also"></a>另請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
