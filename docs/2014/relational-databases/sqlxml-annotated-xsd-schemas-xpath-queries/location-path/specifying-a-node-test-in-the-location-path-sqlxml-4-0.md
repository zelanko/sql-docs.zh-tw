---
title: 指定節點測試中的位置路徑 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ca3eff7a8d915588d632dc12ff94e42d946d8aad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022833"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路徑中指定節點測試 (SQLXML 4.0)
  節點測試會指定位置步驟所選取的節點類型。 每個軸 (`child`、`parent`、`attribute` 或 `self`) 都有一個主要節點類型。 如`attribute`軸，主要節點類型是**\<屬性 >**。 如`parent`， `child`，和`self`軸，主要節點類型是**\<項目 >**。  
  
> [!NOTE]  
>  不支援萬用字元節點測試 * (例如 `child::*`)。  
  
## <a name="node-test-example-1"></a>節點測試： 範例 1  
 位置路徑`child::Customer`選取**\<客戶 >** 內容節點的項目子系。  
  
 在此範例中，`child` 為軸，而 `Customer` 為節點測試。 主要節點類型`child`軸是**\<項目 >**。 因此，會在節點測試為 TRUE，如果**\<客戶 >** 節點是**\<項目 >** 節點。 如果內容節點沒有**\<客戶 >** 子系，會傳回空的節點集。  
  
## <a name="node-test-example-2"></a>節點測試：範例 2  
 位置路徑`attribute::CustomerID`選取**CustomerID**內容節點的屬性。  
  
 在此範例中，`attribute` 為軸，而 `CustomerID` 為節點測試。 主要節點類型`attribute`軸是**\<屬性 >**。 因此，會在節點測試為 TRUE，如果**CustomerID**是**\<屬性 >** 節點。 如果內容節點沒有**CustomerID**，會傳回空的節點集。  
  
> [!NOTE]  
>  在此實作中的 XPath，如果位置步驟參考**\<項目 >** 或**\<屬性 >** 中未宣告之結構描述，則會產生錯誤的類型。 這與 MSXML 中的 XPath 實作不同，該實作會傳回空的節點集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸的縮寫語法  
 位置路徑的以下縮寫語法有受到支援：  
  
-   `attribute::` 可縮寫成 `@`。  
  
     位置路徑 `Customer[@CustomerID="ALFKI"]` 與 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   位置步驟中可省略 `child::`。  
  
     因此，`child` 是預設軸。 位置路徑 `Customer/Order` 與 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可以縮寫成一個句號 (.)，而 `parent::node()` 可縮寫成兩個句號 (..)。  
  
  