---
title: '在位置路徑中設定選取述詞 (SQLXML) '
description: 瞭解如何在 XPath 的位置路徑運算式中指定選取述詞 (SQLXML 4.0) 查詢篩選要查詢的節點集。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c02a33e76fd478e77e2b5a743b5cc6e1d32f1ff
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414409"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>在位置路徑 (SQLXML 4.0) 中指定選取述詞
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  述詞會篩選與軸有關的節點集 (與 SELECT 陳述式中的 WHERE 子句相似)， 並指定在方括號之間。 對於節點集內要篩選的每一個節點，該節點會當做內容節點，而且節點集內的節點數目會當做內容大小，然後評估述詞運算式。 如果述詞運算式評估該節點為 TRUE，則產生的節點集會包含該節點。  
  
 XPath 也允許以位置為基礎的篩選。 評估為數字的述詞運算式會選取該序數節點。 例如，位置路徑 `Customer[3]` 會傳回第三客戶。 但是不支援這類數值述詞， 只支援傳回布林值的述詞運算式。  
  
> [!NOTE]  
>  如需 XPath 實作為 XPath 的限制以及其與 W3C 規格之間差異的詳細資訊，請參閱 [使用 Xpath 查詢的簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="selection-predicate-example-1"></a>選取專案述詞：範例1  
 下列 XPath 運算式 (位置路徑) 從目前內容節點選取所有 **\<Customer>** 具有 **CustomerID** 屬性且值為 ALFKI 的元素子系：  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 在這個 XPath 查詢中，`child` 和 `attribute` 是軸的名稱。 `Customer` 如果是，則節點測試 (TRUE `Customer` **\<element node>** ，因為 **\<element>** 是軸) 的主要節點類型 `child` 。 `attribute::CustomerID="ALFKI"` 是述詞。 在述詞中， `attribute` 是軸，而且 `CustomerID` 如果 **CustomerID** 是內容節點的屬性，則為節點測試 (TRUE，因為 **\<attribute>** 是 **屬性** 軸的主要節點類型) 。  
  
 使用縮寫語法，XPath 查詢也可以指定為：  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>選取專案述詞：範例2  
 下列 XPath 運算式 (位置路徑) 從目前內容節點選取所有 **\<Order>** 具有值1之 **SalesOrderID** 屬性的孫系：  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 在這個 XPath 運算式中，`child` 和 `attribute` 是軸的名稱。 `Customer`、`Order` 和 `SalesOrderID` 是節點測試。 `attribute::OrderID="1"` 是述詞。  
  
 使用縮寫語法，XPath 查詢也可以指定為：  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>選取專案述詞：範例3  
 下列 XPath 運算式 (位置路徑) 從目前的內容節點選取 **\<Customer>** 具有一個或多個子系的所有子系 **\<ContactName>** ：  
  
```  
child::Customer[child::ContactName]  
```  
  
 這個範例假設在 **\<ContactName>** XML 檔中是元素的子項目 **\<Customer>** ，在批註式 XSD 架構中，這稱為 *元素中心的對應* 。  
  
 在這個 XPath 運算式中，`child` 是軸的名稱。 `Customer` 如果是節點，節點測試 (TRUE `Customer` **\<element>** ，因為 **\<element>** 是軸) 的主要節點類型 `child` 。 `child::ContactName` 是述詞。 在述詞中， `child` 是軸，而且是節點 `ContactName` 測試 (TRUE （如果 `ContactName` 是 **\<element>** 節點) ）。  
  
 此運算式只會傳回 **\<Customer>** 具有專案子系的內容節點之元素子系 **\<ContactName>** 。  
  
 使用縮寫語法，XPath 查詢也可以指定為：  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>選取專案述詞：範例4  
 下列 XPath 運算式會選取沒有 **\<Customer>** 元素子系的內容節點之元素子系 **\<ContactName>** ：  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 這個範例假設 **\<ContactName>** 是 XML 檔中專案的子專案 **\<Customer>** ，而且資料庫中不需要 [連絡人] 欄位。  
  
 在此範例中，`child` 為軸。 `Customer` 如果 `Customer` 是節點) ，節點測試是否 (TRUE \<element> 。 `not(child::ContactName)` 是述詞。 在述詞中， `child` 是軸，而且是節點 `ContactName` 測試 (TRUE （如果 `ContactName` 是 \<element> 節點) ）。  
  
 使用縮寫語法，XPath 查詢也可以指定為：  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>選取專案述詞：範例5  
 下列 XPath 運算式會從目前內容節點選取 **\<Customer>** 具有 **CustomerID** 屬性的所有子系：  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 在此範例中， `child` 是軸而且 `Customer` 是節點測試 (TRUE （如果 `Customer` 是 \<element> 節點) ）。 `attribute::CustomerID` 是述詞。 在述詞中， `attribute` 是軸，而且 `CustomerID` 如果 `CustomerID` 是節點) ，則為述詞 (TRUE **\<attribute>** 。  
  
 使用縮寫語法，XPath 查詢也可以指定為：  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>選取述詞：範例 6  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 支援在述詞中包含交叉乘積的 XPath 查詢，如下列範例所示：  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 這個查詢會選取所有客戶，其方式是使用任何 `Order`，其中 `OrderDate` 要等於任何 `ShipDate` 的 `Order`。  
  
## <a name="see-also"></a>另請參閱  
 [批註式 XSD 架構簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [用戶端 XML 格式 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
