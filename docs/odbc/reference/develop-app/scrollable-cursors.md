---
title: 可捲動資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38eb4c8e5cc859297a36115ba5cc6dd2c0529304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061607"
---
# <a name="scrollable-cursors"></a>可捲動的資料指標
新式具有螢幕為基礎的應用程式，在使用者捲動向前及向後的資料。 對於這類應用程式中，返回先前擷取的資料列是問題。 其中一個可能性是關閉並重新開啟資料指標直到資料指標所需的資料列，然後提取資料列。 另一個可能性是讀取結果集、 快取在本機，和實作應用程式中捲動。 這兩種可能性也僅適用於小型結果集，後者可能的原因是難以實作。 更好的解決方案是使用*捲動資料指標，* 這可以向後移動，並轉送結果集中。  
  
 A*捲動資料指標*常用的新式螢幕為基礎的應用程式所在使用者捲動來回資料。 不過，應用程式時應該使用可捲動資料指標只能順向資料指標會執行作業，因為通常成本高於順向資料指標可捲動資料指標。  
  
 向後移動的能力會引發問題不適用於順向資料指標：可捲動資料指標應該會偵測先前擷取的資料列所做的變更嗎？ 也就是說，它應該偵測更新、 刪除及新插入的資料列？  
  
 因為資料列會檢查以查看是否符合該條件，當無法敘述集的資料列符合特定準則的結果集的定義，就會發生這個問題，也不會狀態資料列是否必須包含相同的資料會擷取每一次。 先前省略能夠偵測資料列是否已插入或刪除，而後者可讓它們偵測更新的資料，可捲動資料指標。  
  
 偵測變更的功能有時很有用，有時不是。 例如，會計應用程式需要的資料指標，會忽略所有的變更;平衡書籍是不可能的資料指標會顯示最新的變更。 相反地，航班訂位系統需要的資料指標，顯示資料的最新變更沒有這類資料指標，它必須持續重新查詢以顯示最新的航班可用性資料庫。  
  
 若要處理不同的應用程式的需求，ODBC 定義可捲動資料指標的四種不同的類型。 這些資料指標會在費用而有所不同，並在能夠偵測結果的變更設定。 請注意，是否可捲動資料指標可以偵測資料列的變更，它可以只偵測到它們時它會嘗試重新提取這些資料列;沒有任何方法可讓資料來源通知資料指標目前提取的資料列的變更。 請注意也可見性的變更也會受到交易隔離層級;如需詳細資訊，請參閱 <<c0> [ 交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 此章節包含下列主題。  
  
-   [可捲動的資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可捲動的資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相對與絕對的捲動](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)
