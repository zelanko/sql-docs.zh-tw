---
title: 資料指標 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305289"
---
# <a name="cursors"></a>資料指標
應用程式用*游標*獲取數據。 游標與結果集不同:結果集是匹配特定搜索條件的行集,而游標是將這些行返回到應用程式的軟體。 名稱*游標*(如適用於資料庫)可能源自電腦終端上的閃爍游標。 正如該游標指示螢幕上的當前位置以及鍵入的單詞接下來將出現的位置一樣,結果集中的游標指示結果集中的當前位置以及接下來將返回的行。  
  
 ODBC 中的游標模型基於嵌入式 SQL 中的游標模型。 這些模型之間的一個顯著區別是打開游標的方式。 在嵌入式 SQL 中,必須顯式聲明和打開游標,然後才能使用它。 在 ODBC 中,在執行創建結果集的語句時隱式打開遊標。 打開游標時,游標位於結果集的第一行之前。 在嵌入式 SQL 和 ODBC 中,必須在應用程式完成使用後關閉游標。  
  
 不同的游標具有不同的特徵。 最常見的游標類型稱為*僅前進游標,* 只能通過結果集向前移動。 要返回到上一行,應用程式必須關閉並重新打開遊標,然後從結果集的開頭讀取行,直到到達所需的行。 僅前游標提供了一種快速機制,用於通過結果集進行單個傳遞。  
  
 僅前游標對於基於螢幕的應用程式使用較少,使用者在其中通過數據向後和向前滾動。 此類應用程式可以通過讀取結果集一次、在本地緩存數據以及自行執行滾動來使用僅轉發游標。 但是,這僅適用於少量數據。 更好的解決方案是使用*可滾動的遊標,* 它提供對結果集的隨機訪問。 此類應用程式還可以通過使用所謂的*塊游標*一次獲取多行數據來提高性能。 有關區塊游標的詳細資訊,請參閱[使用區塊游標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 僅前游標是 ODBC 中的預設游標類型,在以下各節中討論。 有關區塊游標和可捲軸的詳細資訊,請參閱[區塊游標](../../../odbc/reference/develop-app/block-cursors.md),[並選擇滑動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  通過顯式調用**SQLEndTran**或以自動提交模式操作來提交或回滾事務,會導致某些數據源關閉連接上所有語句上的所有游標。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明中SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR屬性。
