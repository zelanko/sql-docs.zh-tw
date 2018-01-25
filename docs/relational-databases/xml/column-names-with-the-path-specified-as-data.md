---
title: "以 data() 指定路徑的資料行名稱 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e97d1a5fc6a121dab9411deedfb5bea494513abb
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="column-names-with-the-path-specified-as-data"></a>以 data() 指定路徑的資料行名稱
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 如果以資料行名稱指定的路徑是 "data()"，則在產生的 XML 中會將其值視為不可部分完成值。 如果序列化的下一個項目也是不可部分完成值，就會在 XML 中加入空白字元。 當您建立清單類型的元素與屬性值時，這會非常有用。 下列查詢會擷取產品型號識別碼、名稱以及該產品型號中的產品清單。  
  
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
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
