---
title: 可滾動的資料指標 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304209"
---
# <a name="scrollable-cursors"></a>可捲動的資料指標
在新式螢幕應用程式中，使用者會向前和向後流覽資料。 對於這類應用程式，返回先前提取的資料列會是個問題。 其中一個可能的原因是關閉並重新開啟資料指標，然後提取資料列，直到資料指標到達所需的資料列為止。 另一個可能的原因是讀取結果集、在本機快取，然後在應用程式中執行滾動。 這兩種可能性只適用于小型的結果集，而後者可能很難以實現。 較佳的解決方法是使用可滾動的資料*指標，* 這可以在結果集中向前和向後移動。  
  
 可*滾動*的資料指標通常用於新式螢幕式應用程式中，使用者會在其中來回流覽資料。 不過，只有在順向資料指標不會執行作業時，應用程式才應使用可滾動的資料指標，因為可滾動的資料指標通常會比順向資料指標更昂貴。  
  
 向後移動的功能引發了不適用於順向資料指標的問題：是否應該讓可滾動的資料指標偵測到先前提取的資料列變更？ 也就是，它會偵測更新、刪除和新插入的資料列嗎？  
  
 這個問題是因為結果集的定義（符合特定準則的資料列集）在檢查資料列以查看其是否符合準則時不會處於狀態，也不會指出每次提取資料列時是否必須包含相同的資料。 先前的省略可讓可滾動資料指標偵測是否已插入或刪除資料列，而後者則可以偵測到更新的資料。  
  
 偵測變更的功能有時很有用，有時也不會用到。 例如，會計應用程式需要忽略所有變更的資料指標;如果游標顯示最新的變更，就無法平衡書籍。 相反地，航空公司保留系統需要一個資料指標，以顯示資料的最新變更;如果沒有這種資料指標，它必須持續重新查詢資料庫，以顯示最新的航班可用性。  
  
 為了涵蓋不同應用程式的需求，ODBC 定義了四種不同類型的可滾動資料指標。 這些資料指標的支出和偵測結果集變更的能力各有不同。 請注意，如果可滾動的資料指標可以偵測到資料列的變更，它只會在嘗試重新擷取這些資料列時偵測到它們;資料來源沒有任何方法可以通知游標目前已提取資料列的變更。 請注意，變更的可見度也會受到交易隔離等級的控制;如需詳細資訊，請參閱[交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 此章節包含下列主題。  
  
-   [可捲動的資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可捲動的資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相對與絕對的捲動](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)
