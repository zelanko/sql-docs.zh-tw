---
title: 以 data() 指定路徑的資料行名稱 | Microsoft 文件
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc2d5d801eb99f2097655c94c15cef16038b3ca4
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664709"
---
# <a name="column-names-with-the-path-specified-as-data"></a>以 data() 指定路徑的資料行名稱

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

如果以資料行名稱指定的路徑是 "data()"，則在產生的 XML 中會將其值視為不可部分完成值。 如果序列化的下一個項目也是不可部分完成值，就會在 XML 中加入空白字元。 當您建立清單類型的元素與屬性值時，這會非常有用。 下列查詢會擷取產品型號識別碼、名稱以及該產品型號中的產品清單。  
  
```sql
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
  
 巢狀 SELECT 會擷取產品識別碼的清單。 它會將 "data()" 指定為產品識別碼的資料行名稱。 因為 PATH 模式會為資料列元素名稱指定空白字串，所以不會產生任何資料列元素。 而是會以指派給父項 SELECT 中 `<ProductModelData>` 資料列項目的 ProductID 屬性來傳回值。 以下是結果：  

```sql
<ProductModelData
  ProductModelID="7"
  ProductModelName="HL Touring Frame"
  ProductIDs="885 887 888 889 890 891 892 893"
/>
```

## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
