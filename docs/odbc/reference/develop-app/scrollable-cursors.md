---
title: 可滾動游標 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304209"
---
# <a name="scrollable-cursors"></a>可捲動的資料指標
在現代基於螢幕的應用程式中,用戶通過數據向前滾動。 對於此類應用程式,返回到以前提取的行是一個問題。 一種可能性是關閉並重新打開遊標,然後提取行,直到游標到達所需的行。 另一種可能性是讀取結果集,將其本地緩存,並在應用程式中實現滾動。 這兩種可能性只有在結果集時才很良好,而後一種可能性很難實現。 更好的解決方案是使用*可滾動的遊標,* 它可以在結果集中向後和向前移動。  
  
 *可滾動游標*通常用於基於螢幕的現代應用程式,使用者在其中通過數據來回滾動。 但是,應用程式應僅在僅轉發游標無法執行作業時才使用可滾動遊標,因為可滾動遊標通常比僅轉發游標更昂貴。  
  
 向後移動的能力引發了一個不適用於僅向前游標的問題:可滾動遊標是否應檢測以前獲取的行所做的更改? 也就是說,它應該檢測更新、刪除和新插入的行嗎?  
  
 出現此問題的原因是,結果集的定義(與特定條件匹配的行集)不說明何時檢查行以查看它們是否與該條件匹配,也不說明每次提取行時是否必須包含相同的數據。 前一個遺漏使可滾動的遊標能夠檢測行是否已插入或刪除,而後者則使它們能夠檢測更新的數據。  
  
 檢測更改的能力有時很有用,有時不是。 例如,會計應用程式需要忽略所有更改的游標;如果游標顯示最新的更改,則無法平衡書籍。 另一方面,航空公司預訂系統需要一個游標,用於顯示數據的最新更改;如果沒有這樣的游標,它必須不斷重新查詢資料庫以顯示最新的飛行可用性。  
  
 為了滿足不同應用的需求,ODBC 定義了四種不同類型的可滾動遊標。 這些游標在費用和檢測結果集更改的能力上都有所不同。 請注意,如果可滾動的遊標可以檢測行的更改,則它只能在嘗試重新提取這些行時檢測它們;數據源無法通知游標當前提取的行的更改。 另請注意,更改的可見性也受事務隔離級別控制;有關詳細資訊,請參閱[事務隔離](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 此章節包含下列主題。  
  
-   [可捲動的資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可捲動的資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相對與絕對的捲動](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)
