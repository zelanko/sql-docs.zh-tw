---
title: 指定 (SQLXML) 的位置路徑
description: 瞭解如何在 SQLXML 4.0 XPath 查詢中指定位置路徑，以選取相對於內容節點的一組節點，並產生節點集。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9dedf4df4aa43f79ca4146da6f1183b0ee06286b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431176"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>指定位置路徑 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XPath 查詢會以運算式的形式指定。 運算式有各種不同的類型。 位置路徑是一個運算式，可用來選取相對於內容節點的一組節點。 評估位置路徑的結果為節點集。  
  
## <a name="types-of-location-paths"></a>位置路徑的類型  
 位置路徑可以是下列其中一個形式：  
  
-   **絕對位置路徑**  
  
     絕對位置路徑會從文件的根節點開始。 其中包含一條斜線 (/)，後面選擇性地加上一個相對位置路徑。 斜線 (/) 會選取文件的根節點。  
  
-   **相對位置路徑**  
  
     相對位置路徑會從文件中的內容節點開始。 位置路徑包含一或多個位置步驟的序列，而且每個位置步驟都以斜線 (/) 分隔。 每個步驟都會選取相對於內容節點的一組節點。 步驟的初始序列會選取一組相對於內容節點的節點。 該集合中的每個節點都會當做下列步驟的內容節點使用。 系統會加入由該步驟識別的節點集合。 例如， **child：： Order/child：： OrderDetail** 會選取 **\<OrderDetail>** **\<Order>** 內容節點之元素子系的元素子系。  
  
    > [!NOTE]  
    >  在 XPath 的 SQLXML 4.0 實作中，即使 XPath 明顯地不是絕對的，每個 XPath 查詢都會從根內容開始。 例如，系統會將 "Customer" 開頭的 XPath 查詢視為 "/Customer"。 在 XPath 查詢 **customer [Order]** 中，客戶從根內容開始，但訂單從客戶內容開始。 如需詳細資訊，請參閱 [使用 XPath 查詢的簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)。  
  
## <a name="location-steps"></a>位置步驟  
 位置路徑 (絕對或相對) 是由包含三個部分的位置步驟所組成：  
  
-   **軸**  
  
     軸會指定位置步驟與內容節點所選取之節點間的樹狀結構關聯性。 支援 **parent**、 **child**、 **attribute** 和 **self** 軸。 如果在位置路徑中指定了 **子** 軸，則查詢選取的所有節點都是內容節點的子系。 如果指定了 **父** 軸，則選取的節點會是內容節點的父節點。 如果指定 **屬性** 軸，則選取的節點是內容節點的屬性。  
  
-   **節點測試**  
  
     節點測試會指定位置步驟所選取的節點類型。 每個軸 (**子** 系、 **父系**、 **屬性** 和 **self**) 都有主要節點類型。 如果是 **屬性** 軸，主要節點類型為 **\<attribute>** 。 若為 **父系**、 **子** 系和 **自我** 軸，主要節點類型為 **\<element>** 。  
  
     例如，如果位置路徑指定了 **child：： Customer**，則 **\<Customer>** 會選取內容節點的元素子系。 因為 **子** 軸的 **\<element>** 主要節點類型是，所以如果客戶是節點，節點測試客戶就會是 TRUE **\<element>** 。  
  
-   **選取述詞 (零或其他)**  
  
     述詞會針對軸篩選節點集。 在 XPath 運算式中指定選取述詞類似於在 SELECT 陳述式中指定 WHERE 子句。 並指定在方括號之間。 套用在選取述詞中指定的測試會篩選由節點測試傳回的節點。 對於節點集內要篩選的每一個節點，該節點會當做內容節點，而且節點集內的節點數目會當做內容大小，然後評估述詞運算式。 如果述詞運算式評估該節點為 TRUE，則產生的節點集會包含該節點。  
  
     位置步驟的語法是軸名稱之後加上雙冒號 (::)、接著是節點測試，最後是零或其他述詞，每個述詞都會以方括弧括起來。 例如，XPath 運算式 (位置路徑) **child：： Customer [ @CustomerID = ' ALFKI ']** 會選取 **\<Customer>** 內容節點的所有元素子系。 然後，述詞中的測試會套用到節點集，而節點集只會傳回 **\<Customer>** 其 **CustomerID** 屬性的屬性值為 ' ALFKI ' 的元素節點。  
  
## <a name="in-this-section"></a>本節內容  
 [指定 &#40;SQLXML 4.0&#41;的軸 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 提供指定軸的範例。  
  
 [在位置路徑中指定節點測試 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 提供指定節點測試的範例。  
  
 [在位置路徑中指定選取述詞 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 提供指定選取述詞的範例。  
  
  
