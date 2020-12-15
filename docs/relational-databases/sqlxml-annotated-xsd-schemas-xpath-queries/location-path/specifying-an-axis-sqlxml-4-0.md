---
title: 指定 (SQLXML) 的軸
description: 瞭解如何在 SQLXML 4.0 XPath 查詢中指定軸，以指定位置步驟所選取的節點與內容節點之間的樹狀結構關聯性。
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03c0fff271ef3774116eb9c97025b1f602f7852c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431156"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定軸 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
    
-   軸會指定位置步驟與內容節點所選取之節點間的樹狀結構關聯性。 支援下列座標軸：**子** 系  
  
     包含內容節點的子系。  
  
     下列 XPath 運算式 (位置路徑) 從目前內容節點選取所有 **\<Customer>** 子系：  
  
    ```  
    child::Customer  
    ```  
  
     在下列 XPath 查詢中，`child` 為軸。 `Customer` 為節點測試。  
  
-   **parent**  
  
     包含內容節點的父系。  
  
     下列 XPath 運算式會選取子系的所有父系 **\<Customer>** **\<Order>** ：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     這與指定 `child::Customer` 相同。 在此 XPath 查詢中，`child` 和 `parent` 為軸。 `Customer` 和 `Order` 為節點測試。  
  
-   **屬性**  
  
     包含內容節點的屬性。  
  
     下列 XPath 運算式會選取內容節點的 **CustomerID** 屬性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **自我**  
  
     包含內容節點本身。  
  
     下列 XPath 運算式會選取目前的節點（如果它是 **\<Order>** 節點的話）：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查詢中，`self` 為軸，而 `Order` 為節點測試。  
  
  
