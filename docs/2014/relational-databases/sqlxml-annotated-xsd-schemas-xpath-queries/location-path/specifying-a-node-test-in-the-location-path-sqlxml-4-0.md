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
ms.openlocfilehash: 02f78577eab391f1774251ad2c6ca7b9a4bd2dab
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015223"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路徑中指定節點測試 (SQLXML 4.0)
  節點測試會指定位置步驟所選取的節點類型。 每個軸 (`child`、`parent`、`attribute` 或 `self`) 都有一個主要節點類型。 若為 `attribute` 軸，主要節點類型為 **\<attribute>** 。 針對 `parent` 、 `child` 和 `self` 座標軸，主要節點類型為 **\<element>** 。  
  
> [!NOTE]  
>  不支援萬用字元節點測試 * (例如 `child::*`)。  
  
## <a name="node-test-example-1"></a>節點測試：範例1  
 位置路徑會 `child::Customer` 選取 **\<Customer>** 內容節點的元素子系。  
  
 在此範例中，`child` 為軸，而 `Customer` 為節點測試。 軸的主要節點類型 `child` 是 **\<element>** 。 因此，如果節點是節點，節點測試就是 TRUE **\<Customer>** **\<element>** 。 如果內容節點沒有子系 **\<Customer>** ，則會傳回空的節點集。  
  
## <a name="node-test-example-2"></a>節點測試：範例 2  
 位置路徑會 `attribute::CustomerID` 選取內容節點的**CustomerID**屬性。  
  
 在此範例中，`attribute` 為軸，而 `CustomerID` 為節點測試。 軸的主要節點類型 `attribute` 是 **\<attribute>** 。 因此，如果**CustomerID**為節點，則節點測試為 TRUE **\<attribute>** 。 如果內容節點沒有**CustomerID**，則會傳回空的節點集。  
  
> [!NOTE]  
>  在此 XPath 的執行中，如果位置步驟參考的 **\<element>** **\<attribute>** 是或未在架構中宣告的類型，則會產生錯誤。 這與 MSXML 中的 XPath 實作不同，該實作會傳回空的節點集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸的縮寫語法  
 位置路徑的以下縮寫語法有受到支援：  
  
-   `attribute::` 可縮寫成 `@`。  
  
     位置路徑 `Customer[@CustomerID="ALFKI"]` 與 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   位置步驟中可省略 `child::`。  
  
     因此，`child` 是預設軸。 位置路徑 `Customer/Order` 與 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可以縮寫成一個句號 (.)，而 `parent::node()` 可縮寫成兩個句號 (..)。  
  
  
