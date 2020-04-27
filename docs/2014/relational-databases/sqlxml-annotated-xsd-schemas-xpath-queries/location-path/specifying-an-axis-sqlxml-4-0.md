---
title: 指定軸（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8da239fd8a6bbf559f89ba5fd1b0fa0ab10ec190
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012653"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定軸 (SQLXML 4.0)
    
-   軸會指定位置步驟與內容節點所選取之節點間的樹狀結構關聯性。 支援下列軸：`child`  
  
     包含內容節點的子系。  
  
     下列 XPath 運算式（位置路徑）會從目前的內容節點中選取所有** \<客戶>** 子系：  
  
    ```  
    child::Customer  
    ```  
  
     在下列 XPath 查詢中，`child` 為軸。 `Customer` 為節點測試。  
  
-   `parent`  
  
     包含內容節點的父系。  
  
     下列 XPath 運算式會選取** \<訂單>** 子系的所有** \<客戶>** 父系：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     這與指定 `child::Customer` 相同。 在此 XPath 查詢中，`child` 和 `parent` 為軸。 `Customer` 和 `Order` 為節點測試。  
  
-   `attribute`  
  
     包含內容節點的屬性。  
  
     下列 XPath 運算式會選取內容節點的**CustomerID**屬性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     包含內容節點本身。  
  
     下列 XPath 運算式會選取目前的節點（如果它是** \<Order>** 節點）：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查詢中，`self` 為軸，而 `Order` 為節點測試。  
  
  
