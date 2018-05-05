---
title: 指定節點測試中的位置路徑 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2c25b27a36a8505f0608ad8690ea13d6c60c197
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路徑中指定節點測試 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  節點測試會指定位置步驟所選取的節點類型。 每個軸 (**子**，**父**，**屬性**，或**自我**) 有一個主體節點類型。 如**屬性**軸，主要節點類型是**\<屬性 >**。 如**父**，**子**，和**自我**軸，主要節點類型是**\<項目 >**。  
  
> [!NOTE]  
>  不支援萬用字元節點測試 * (例如 `child::*`)。  
  
## <a name="node-test-example-1"></a>節點測試： 範例 1  
 位置路徑`child::Customer`選取**\<客戶 >** 內容節點的項目子系。  
  
 在此範例中，`child` 為軸，而 `Customer` 為節點測試。 主要節點類型**子**軸是**\<項目 >**。 因此，會在節點測試為 TRUE，如果**\<客戶 >** 節點是**\<項目 >** 節點。 如果內容節點沒有**\<客戶 >** 子系，會傳回空的節點集。  
  
## <a name="node-test-example-2"></a>節點測試：範例 2  
 位置路徑`attribute::CustomerID`選取**CustomerID**內容節點的屬性。  
  
 在此範例中，`attribute` 為軸，而 `CustomerID` 為節點測試。 主要節點類型**屬性**軸是**\<屬性 >**。 因此，會在節點測試為 TRUE，如果**CustomerID**是**\<屬性 >** 節點。 如果內容節點沒有**CustomerID**，會傳回空的節點集。  
  
> [!NOTE]  
>  在此實作中的 XPath，如果位置步驟參考**\<項目 >** 或**\<屬性 >** 中未宣告之結構描述，則會產生錯誤的類型。 這與 MSXML 中的 XPath 實作不同，該實作會傳回空的節點集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸的縮寫語法  
 位置路徑的以下縮寫語法有受到支援：  
  
-   `attribute::` 可縮寫成 `@`。  
  
     位置路徑 `Customer[@CustomerID="ALFKI"]` 與 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   位置步驟中可省略 `child::`。  
  
     因此，**子**是預設軸。 位置路徑 `Customer/Order` 與 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可以縮寫成一個句號 (.)，而 `parent::node()` 可縮寫成兩個句號 (..)。  
  
  
