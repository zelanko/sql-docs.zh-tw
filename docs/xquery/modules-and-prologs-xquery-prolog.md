---
title: "XQuery 初構 |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, prolog
- prolog
- namespaces [XQuery]
- default namespace declarations
ms.assetid: 03924684-c5fd-44dc-8d73-c6ab90f5e069
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d46786394ce7eb8d6331de98a98ede8999451607
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="modules-and-prologs---xquery-prolog"></a>模組和初構-XQuery 初構
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery 查詢是由初構及主體所組成。 XQuery 初構是一系列的宣告和定義，由這二者共同建立查詢處理所需的環境。 在 SQL Server 中，XQuery 初構可以包含命名空間宣告。 XQuery 主體則由一系列的運算式所組成，可指定所想要得到的查詢結果。  
  
 例如，以下 XQuery 針對 Instructions 資料行所指定**xml**將製造指示儲存為 XML 的型別。 該查詢會擷取工作中心位置 `10` 的製造指示。 `query()`方法**xml**資料類型用來指定 XQuery。  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') AS Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   XQuery 初構包含命名空間前置詞 (AWMI) 宣告， `(namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";`。  
  
-   `declare namespace` 關鍵字定義稍後要用在查詢主體中的命名空間前置詞。  
  
-   `/AWMI:root/AWMI:Location[@LocationID="10"]` 則是查詢主體。  
  
## <a name="namespace-declarations"></a>命名空間宣告  
 命名空間宣告會定義前置詞，並將其與命名空間 URI 產生關聯，如下列查詢所示。 在查詢中，`CatalogDescription`是**xml**類型資料行。  
  
 針對此資料行指定 XQuery 時，查詢初構指定了 `declare namespace` 宣告，使前置詞 `PD` (產品描述) 與命名空間 URI 產生關聯。 接著，在查詢主體中使用這個前置詞來代替命名空間 URI。 所產生 XML 中的節點，就會位在與該命名空間 URI 相關聯的命名空間中。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 若要增進查詢的可讀性，您可以使用 WITH XMLNAMESPACES 來宣告命名空間，而不要在查詢初構中使用 `declare namespace` 來宣告前置詞和命名空間的繫結。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
  
SELECT CatalogDescription.query('  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 如需詳細資訊，請參閱，[查詢使用 WITH XMLNAMESPACES 新增命名空間](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)。  
  
### <a name="default-namespace-declaration"></a>預設命名空間宣告  
 除了使用 `declare namespace` 宣告來宣告命名空間前置詞，您還可以改用 `declare default element namespace` 宣告，以繫結元素名稱的預設命名空間。 在此情況下，您不用指定任何前置詞。  
  
 在以下範例中，查詢主體中的路徑運算式並沒有指定命名空間前置詞。 依預設，所有元素名稱皆屬於初構中所指定的預設命名空間。  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace  "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
 您也可以使用 WITH XMLNAMESPACES 來宣告預設命名空間：  
  
```  
WITH XMLNAMESPACES (DEFAULT 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription')  
SELECT CatalogDescription.query('  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
## <a name="see-also"></a>請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
