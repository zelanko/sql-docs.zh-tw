---
title: 範例：指定 HIDE 指示詞 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
author: rothja
ms.author: jroth
ms.openlocfilehash: 423ee36f679467c07a604b9754172f6e261971b1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067770"
---
# <a name="example-specifying-the-hide-directive"></a>範例：指定 HIDE 指示詞
  此範例說明 **HIDE** 指示詞的用法。 當您希望查詢可以傳回由查詢傳回的通用資料表中，用以排序資料列的屬性，但又不希望在最後的結果 XML 文件中看見該屬性時，此指示詞就相當有用。  
  
 此查詢會建構以下 XML：  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 此查詢會產生您想要的 XML。 查詢可識別出資料行名稱中標記值各為 1 及 2 的兩個資料行群組。  
  
 此查詢使用 [xml](/sql/t-sql/xml/query-method-xml-data-type) 資料類型的 **query() 方法 (xml 資料類型)** ，以查詢 **xml** 類型的 CatalogDescription 資料行來擷取摘要描述。 此查詢也可以使用 [xml](/sql/t-sql/xml/value-method-xml-data-type) 資料類型的 **value() 方法 (xml 資料類型)** ，以擷取 CatalogDescription 資料行的 ProductModelID 值。 結果 XML 中不需要有此值，但必須要有此值才能將產生的資料列集排序。 因此，資料行名稱 `[Summary!2!ProductModelID!HIDE]`會包含 **HIDE** 指示詞。 如果 SELECT 陳述式中不包括此資料行，您將必須依照 `[ProductModel!1!ProdModelID]` 和 `[Summary!2!SummaryDescription]` (此為 **xml** 類型) 排序資料列集，而且無法以 ORDER BY 使用 **xml** 類型資料行。 因此，會增加額外的 `[Summary!2!ProductModelID!HIDE]` 資料行，然後以 ORDER BY 子句指定。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 以下是結果：  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md)  
  
  
