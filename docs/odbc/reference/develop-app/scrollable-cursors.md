---
description: 可捲動的資料指標
title: 可滾動資料指標 |Microsoft Docs
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
ms.openlocfilehash: 9c347dcb130a2f1f899f2e1b83ae28289ff0a923
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476480"
---
# <a name="scrollable-cursors"></a>可捲動的資料指標
在新式螢幕應用程式中，使用者會在資料中向前和向後滾動。 針對這類應用程式，返回先前提取的資料列是個問題。 其中一個可能的原因是關閉並重新開啟資料指標，然後提取資料列，直到資料指標到達所需的資料列為止。 另一個可能的原因是讀取結果集、在本機快取，然後在應用程式中執行滾動。 這兩種可能性只適用于小型的結果集，而後者的可能性很難實行。 更好的解決方法是使用可滾動的資料 *指標，* 它可以在結果集中向前和向下移動。  
  
 可 *滾動* 的資料指標通常用於新式螢幕應用程式中，使用者會在這些應用程式中來回移動資料。 不過，只有順向資料指標不會執行工作時，應用程式才應該使用可滾動的資料指標，因為可滾動的資料指標通常比順向資料指標更昂貴。  
  
 向前復原的能力會引發不適用順向資料指標的問題：可滾動的資料指標是否會偵測到先前提取的資料列發生了變更？ 也就是說，它應該偵測更新、刪除和新插入的資料列嗎？  
  
 發生這個問題的原因是結果集的定義-符合特定準則的資料列集，在檢查資料列以查看它們是否符合該準則時，並不會指出資料列是否必須在每次提取時都包含相同的資料。 先前的省略可讓可滾動的資料指標偵測是否已插入或刪除資料列，而後者讓它們可以偵測更新的資料。  
  
 偵測變更的功能有時很有用，有時也是很有用。 例如，會計應用程式需要會忽略所有變更的資料指標;如果資料指標顯示最新的變更，就無法平衡書籍。 另一方面，航空公司預訂系統需要資料指標，以顯示資料的最新變更;如果沒有這類資料指標，它就必須持續重新查詢資料庫，以顯示最新的航班可用性。  
  
 為了涵蓋不同應用程式的需求，ODBC 定義了四種不同類型的可滾動資料指標。 這些資料指標的費用和偵測結果集變更的能力各有不同。 請注意，如果可滾動的資料指標可以偵測到資料列的變更，只有在嘗試重新擷取這些資料列時，才可以偵測到它們;沒有任何方法可讓資料來源通知資料指標目前所提取的資料列變更。 也請注意，變更的可見度也會由交易隔離等級控制;如需詳細資訊，請參閱 [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 此章節包含下列主題。  
  
-   [可捲動的資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可捲動的資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相對與絕對的捲動](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)
