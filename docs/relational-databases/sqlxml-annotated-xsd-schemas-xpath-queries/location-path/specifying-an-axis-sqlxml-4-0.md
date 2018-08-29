---
title: 指定軸 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b3a822bf7c6814fb9e9e7b671beddb19d976bd5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079616"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定軸 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   軸會指定位置步驟與內容節點所選取之節點間的樹狀結構關聯性。 支援下列軸：**子系**  
  
     包含內容節點的子系。  
  
     下列 XPath 運算式 （位置路徑） 從目前所有的內容節點中選取**\<客戶 >** 子系：  
  
    ```  
    child::Customer  
    ```  
  
     在下列 XPath 查詢中，`child` 為軸。 `Customer` 為節點測試。  
  
-   **parent**  
  
     包含內容節點的父系。  
  
     下列 XPath 運算式會選取所有**\<客戶 >** 父系**\<順序 >** 子系：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     這與指定 `child::Customer` 相同。 在此 XPath 查詢中，`child` 和 `parent` 為軸。 `Customer` 和 `Order` 為節點測試。  
  
-   **屬性**  
  
     包含內容節點的屬性。  
  
     下列 XPath 運算式選取**CustomerID**內容節點的屬性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **self**  
  
     包含內容節點本身。  
  
     下列 XPath 運算式會選取目前的節點才**\<順序 >** 節點：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查詢中，`self` 為軸，而 `Order` 為節點測試。  
  
  
