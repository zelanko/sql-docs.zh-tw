---
title: 在位置路徑中指定節點測試（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e4ff55980c7ca4cae45d568f03fef32ba1ea5155
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703104"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路徑中指定節點測試 (SQLXML 4.0)
  節點測試會指定位置步驟所選取的節點類型。 每個軸 (`child`、`parent`、`attribute` 或 `self`) 都有一個主要節點類型。 若為 `attribute` 軸，主要節點類型為** \< 屬性>**。 針對 `parent` 、 `child` 和 `self` 座標軸，主要節點類型為** \< element>**。  
  
> [!NOTE]  
>  不支援萬用字元節點測試 * (例如 `child::*`)。  
  
## <a name="node-test-example-1"></a>節點測試：範例1  
 位置路徑會 `child::Customer` 選取內容節點的** \< 客戶>** 元素子系。  
  
 在此範例中，`child` 為軸，而 `Customer` 為節點測試。 軸的主要節點類型 `child` 是** \< 元素>**。 因此，如果** \< 客戶>** 節點是>節點的** \< 元素**，節點測試就會是 TRUE。 如果內容節點沒有** \< 客戶>** 子系，則會傳回空的節點集。  
  
## <a name="node-test-example-2"></a>節點測試：範例 2  
 位置路徑會 `attribute::CustomerID` 選取內容節點的**CustomerID**屬性。  
  
 在此範例中，`attribute` 為軸，而 `CustomerID` 為節點測試。 軸的主要節點類型 `attribute` 是>的** \< 屬性**。 因此，如果**CustomerID**是>節點的** \< 屬性**，節點測試就會是 TRUE。 如果內容節點沒有**CustomerID**，則會傳回空的節點集。  
  
> [!NOTE]  
>  在此 XPath 的執行中，如果位置步驟參考>的** \< 元素**，或未在架構中宣告的** \< 屬性>** 類型，則會產生錯誤。 這與 MSXML 中的 XPath 實作不同，該實作會傳回空的節點集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸的縮寫語法  
 位置路徑的以下縮寫語法有受到支援：  
  
-   `attribute::` 可縮寫成 `@`。  
  
     位置路徑 `Customer[@CustomerID="ALFKI"]` 與 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   位置步驟中可省略 `child::`。  
  
     因此，`child` 是預設軸。 位置路徑 `Customer/Order` 與 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可以縮寫成一個句號 (.)，而 `parent::node()` 可縮寫成兩個句號 (..)。  
  
  
