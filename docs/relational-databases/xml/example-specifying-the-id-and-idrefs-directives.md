---
title: 範例：指定 ID 和 IDREFS 指示詞 | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29468af968f8e4ffd92e52258b12eb4aece3793b
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80662979"
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>範例：指定 ID 和 IDREFS 指示詞

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

元素屬性可以指定為 **ID** 類型屬性，然後可以使用 **IDREFS** 屬性來參考它。 這會啟用內部文件連結，而且與關聯式資料庫中的主索引鍵及外部索引鍵關聯性類似。  
  
 此範例說明如何使用 **ID** 及 **IDREFS** 指示詞，建立 **ID** 及 **IDREFS** 類型的屬性。 因為 ID 不能是整數值，所以此範例中的 ID 值會經過轉換。 換句話說，會經過類型轉換。 ID 值會使用前置詞。  
  
 假設您想要建構如下所示的 XML：  
  
```xml
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
`SalesOrderIDList` 項目的 `<Customer>` 屬性是一項多重值屬性，參考 `SalesOrderID` 項目的 `<SalesOrder>` 屬性。 若要建立此連結，`SalesOrderID` 屬性必須宣告為 `ID` 類型，且 `SalesOrderIDList` 項目的 `<Customer>` 屬性必須宣告為 `IDREFS` 類型。 因為一位客戶可以下多份訂單，所以要使用 `IDREFS` 類型。
  
 **IDREFS** 類型的元素也會有一個以上的值。 因此，您必須使用個別的 select 子句，以重複使用相同的標記、父系及索引鍵資料行資訊。 然後 `ORDER BY` 必須確定構成 **IDREFS** 值的資料列順序，在它們的父元素下會分在同一組。  
  
 以下查詢會產生您想要的 XML。 此查詢會使用 `ID` 和 `IDREFS` 指示詞來複寫資料行名稱 (`SalesOrder!2!SalesOrderID!ID`、 `Customer!1!SalesOrderIDList!IDREFS`) 中的類型。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID   [Customer!1!CustomerID],  
        NULL           [Customer!1!SalesOrderIDList!IDREFS],
        NULL           [SalesOrder!2!SalesOrderID!ID],  
        NULL           [SalesOrder!2!OrderDate]  
FROM   Sales.Customer C   

UNION ALL   
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID,  
        'O-'+CAST(SalesOrderID as varchar(10)),   
        NULL,  
        NULL  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  

UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
        C.CustomerID,  
        NULL,  
        'O-'+CAST(SalesOrderID as varchar(10)),  
        OrderDate  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID
ORDER BY [Customer!1!CustomerID] ,
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 EXPLICIT 模式](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
