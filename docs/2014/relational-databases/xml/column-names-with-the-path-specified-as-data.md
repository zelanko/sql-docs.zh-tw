---
title: 以 data() 指定路徑的資料行名稱 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe23dba019511137c9ad817ecdf87fae1938bbd6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63288794"
---
# <a name="column-names-with-the-path-specified-as-data"></a>以 data() 指定路徑的資料行名稱
  如果以資料行名稱指定的路徑是 "data()"，則在產生的 XML 中會將其值視為不可部分完成值。 如果序列化的下一個項目也是不可部分完成值，就會在 XML 中加入空白字元。 當您建立清單類型的元素與屬性值時，這會非常有用。 下列查詢會擷取產品型號識別碼、名稱以及該產品型號中的產品清單。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 巢狀 SELECT 會擷取產品識別碼的清單。 它會將 "data()" 指定為產品識別碼的資料行名稱。 因為 PATH 模式會為資料列元素名稱指定空白字串，所以不會產生任何資料列元素。 而是會以指派給父項 SELECT 中 <`ProductModelData`> 資料列元素的 ProductID 屬性來傳回值。 以下是結果：  
  
 `<ProductModelData ProductModelID="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 888 889 890 891 892 893" />`  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)  
  
  
