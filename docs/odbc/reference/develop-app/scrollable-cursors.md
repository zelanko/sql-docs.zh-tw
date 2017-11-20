---
title: "可捲動資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e868f5798e759a9b84e9c28d2c1fa82bb34c4f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="scrollable-cursors"></a>可捲動資料指標
在現代螢幕應用程式中，使用者捲動向前和向後的資料。 這類應用程式中，返回先前擷取的資料列是一個問題。 一個可能的原因是關閉並重新開啟游標然後提取資料列，直到游標達到所需的資料列。 另一個可能性是讀取結果集、 快取在本機，並實作應用程式中捲動。 這兩種可能性也僅適用於小型結果集，和第二個可能的原因是難以實作。 更好的解決方案是使用*可捲動資料指標，*其可以向後移動，並在結果集中轉寄。  
  
 A*可捲動資料指標*常用於新式螢幕為基礎的應用程式中使用者捲動來回資料。 不過，應用程式可捲動資料指標時才應該使用順向資料指標將不會執行該作業，因為通常成本高於順向資料指標可捲動資料指標。  
  
 向後移動的能力會引發問題不適用於順向資料指標： 可捲動資料指標應該會偵測先前擷取的資料列所做的變更嗎？ 也就是說，它應該偵測更新、 刪除及新插入的資料列？  
  
 因為結果的定義設定，就會發生這個問題的答案，符合特定準則的資料列集-未指定時檢查資料列，以查看是否符合該條件，也不會其狀態還是資料列必須包含相同的資料每次提取。 在先前省略讓可捲動資料指標來偵測資料列是否已插入或刪除，而後者可讓它們偵測到更新的資料。  
  
 偵測變更的功能有時候是很有用，有時不。 例如，會計應用程式需要的資料指標，會忽略所有變更;平衡書籍時如果資料指標會顯示最新的變更。 相反地，航空保留系統需要的資料指標，會顯示最新變更的資料。沒有這類資料指標，它必須不斷重新查詢以顯示最新的分段可用性資料庫。  
  
 若要處理不同的應用程式的需求，ODBC 定義四種可捲動資料指標類型。 這些資料指標不在費用和能力偵測結果的變更集。 請注意，是否可捲動資料指標可以偵測資料列的變更，它可以只偵測到它們時若嘗試重新提取這些資料列。沒有任何方法可讓資料來源通知資料指標的目前所提取的資料列的變更。 也請注意變更的可見性也由交易隔離等級。如需詳細資訊，請參閱[交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 此章節包含下列主題。  
  
-   [可捲動資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可捲動資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相對與絕對捲動](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)

