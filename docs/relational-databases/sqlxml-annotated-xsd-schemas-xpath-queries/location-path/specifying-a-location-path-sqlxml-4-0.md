---
title: 指定位置路徑 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8033000aab35da02b5d06a57462730cc74263322
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082150"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>指定位置路徑 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XPath 查詢會以運算式的形式指定。 運算式有各種不同的類型。 位置路徑是一個運算式，可用來選取相對於內容節點的一組節點。 評估位置路徑的結果為節點集。  
  
## <a name="types-of-location-paths"></a>位置路徑的類型  
 位置路徑可以是下列其中一個形式：  
  
-   **絕對位置路徑**  
  
     絕對位置路徑會從文件的根節點開始。 其中包含一條斜線 (/)，後面選擇性地加上一個相對位置路徑。 斜線 (/) 會選取文件的根節點。  
  
-   **相對位置路徑**  
  
     相對位置路徑會從文件中的內容節點開始。 位置路徑包含一或多個位置步驟的序列，而且每個位置步驟都以斜線 (/) 分隔。 每個步驟都會選取相對於內容節點的一組節點。 步驟的初始序列會選取一組相對於內容節點的節點。 該集合中的每個節點都會當做下列步驟的內容節點使用。 系統會加入由該步驟識別的節點集合。 例如， **child:: order/child:: orderdetail**選取 **\<OrderDetail >** 的元素子系**\<順序 >** 項目內容節點的子系。  
  
    > [!NOTE]  
    >  在 XPath 的 SQLXML 4.0 實作中，即使 XPath 明顯地不是絕對的，每個 XPath 查詢都會從根內容開始。 例如，系統會將 "Customer" 開頭的 XPath 查詢視為 "/Customer"。 在 XPath 查詢**Customer [Order]**，客戶根內容開始，但順序開始在客戶內容。 如需詳細資訊，請參閱 <<c0> [ 簡介使用 XPath 查詢&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)。</c0>  
  
## <a name="location-steps"></a>位置步驟  
 位置路徑 (絕對或相對) 是由包含三個部分的位置步驟所組成：  
  
-   **Axis**  
  
     軸會指定位置步驟與內容節點所選取之節點間的樹狀結構關聯性。 **父代**，**子**，**屬性**，以及**自我**軸所支援。 如果**子系**軸中指定位置路徑中，查詢所選取的所有節點都都在內容節點的子系。 如果**父**座標軸指定為選取的節點內容節點的父節點。 如果**屬性**指定軸、 選取的節點是內容節點的屬性。  
  
-   **節點測試**  
  
     節點測試會指定位置步驟所選取的節點類型。 每個軸 (**子**，**父**，**屬性**，以及**自我**) 有一個主要節點類型。 針對**屬性**軸的主要節點類型是**\<屬性 >**。 針對**父**，**子**，並**自我**軸的主要節點類型是**\<項目 >**。  
  
     例如，如果指定的位置路徑**child:: customer**，則**\<客戶 >** 會選取內容節點的項目子系。 因為**子系**軸具有**\<項目 >** 作為其主要節點類型中，節點測試 Customer 為 TRUE 如果 Customer 是**\<項目 >** 節點。  
  
-   **選取述詞 （零或多個）**  
  
     述詞會針對軸篩選節點集。 在 XPath 運算式中指定選取述詞類似於在 SELECT 陳述式中指定 WHERE 子句。 並指定在方括號之間。 套用在選取述詞中指定的測試會篩選由節點測試傳回的節點。 對於節點集內要篩選的每一個節點，該節點會當做內容節點，而且節點集內的節點數目會當做內容大小，然後評估述詞運算式。 如果述詞運算式評估該節點為 TRUE，則產生的節點集會包含該節點。  
  
     位置步驟的語法是軸名稱之後加上雙冒號 (::)、接著是節點測試，最後是零或其他述詞，每個述詞都會以方括弧括起來。 例如，XPath 運算式 （位置路徑） **child:: customer [@CustomerID= 'ALFKI']** 選取所有**\<客戶 >** 內容節點的項目子系。 然後述詞中的測試會套用至節點集，它只會傳回**\<客戶 >** 項目節點屬性值 'ALFKI' 其**CustomerID**屬性。  
  
## <a name="in-this-section"></a>本節內容  
 [指定軸&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 提供指定軸的範例。  
  
 [指定節點測試中的位置路徑&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 提供指定節點測試的範例。  
  
 [指定選取述詞中的位置路徑&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 提供指定選取述詞的範例。  
  
  
