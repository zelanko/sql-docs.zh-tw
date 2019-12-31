---
title: 在位置路徑中指定節點測試（SQLXML）
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f94f155ee86df6daf0c039a18f27c30e294d57df
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254743"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路徑中指定節點測試 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  節點測試會指定位置步驟所選取的節點類型。 每個軸（**子**系、**父系**、**屬性**或**本身**）都具有主要節點類型。 若為**屬性**軸，主要節點類型為** \<屬性>**。 若為**父代**、**子**系和**獨立**軸，主要節點類型為** \<element>**。  
  
> [!NOTE]  
>  不支援萬用字元節點測試 * (例如 `child::*`)。  
  
## <a name="node-test-example-1"></a>節點測試：範例1  
 位置路徑`child::Customer`會選取** \<** 內容節點的客戶>元素子系。  
  
 在此範例中，`child` 為軸，而 `Customer` 為節點測試。 **子**軸的主要節點類型是** \<元素>**。 因此，如果** \<客戶>** 節點是>節點的** \<元素**，節點測試就會是 TRUE。 如果內容節點沒有** \<客戶>** 子系，則會傳回空的節點集。  
  
## <a name="node-test-example-2"></a>節點測試：範例 2  
 位置路徑`attribute::CustomerID`會選取內容節點的**CustomerID**屬性。  
  
 在此範例中，`attribute` 為軸，而 `CustomerID` 為節點測試。 **屬性**軸的主要節點類型是** \<>的屬性**。 因此，如果**CustomerID**是>節點的** \<屬性**，節點測試就會是 TRUE。 如果內容節點沒有**CustomerID**，則會傳回空的節點集。  
  
> [!NOTE]  
>  在此 XPath 的執行中，如果位置步驟參考>的** \<元素**，或未在架構中宣告的** \<屬性>** 類型，則會產生錯誤。 這與 MSXML 中的 XPath 實作不同，該實作會傳回空的節點集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>軸的縮寫語法  
 位置路徑的以下縮寫語法有受到支援：  
  
-   
  `attribute::` 可縮寫成 `@`。  
  
     位置路徑 `Customer[@CustomerID="ALFKI"]` 與 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   位置步驟中可省略 `child::`。  
  
     因此， **child**是預設軸。 位置路徑 `Customer/Order` 與 `child::Customer/child::Order` 相同。  
  
-   
  `self::node()` 可以縮寫成一個句號 (.)，而 `parent::node()` 可縮寫成兩個句號 (..)。  
  
  
