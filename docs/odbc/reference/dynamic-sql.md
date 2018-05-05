---
title: 動態 SQL |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 465f9785436880fce74136dd293abab33d1d2b4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-sql"></a>動態 SQL
靜態 SQL 都適用於許多情況下，雖然還有無法事先判斷資料存取的應用程式類別。 例如，假設試算表可讓使用者輸入的查詢，試算表然後傳送給 DBMS 來擷取資料。 此查詢的內容很明顯地不知道程式設計人員寫入試算表程式時。  
  
 若要解決這個問題，試算表會使用稱為動態 SQL 的內嵌式 SQL 的形式。 與靜態 SQL 陳述式，也就是硬式編碼程式中，不同的是可以在執行階段建立並放在字串的主機變數動態 SQL 陳述式。 他們再傳送至 DBMS 進行處理。 DBMS 必須產生動態 SQL 陳述式的執行階段存取計劃，因為動態 SQL 低於一般靜態 SQL。 編譯程式，包含動態 SQL 陳述式時，動態 SQL 陳述式不會予以程式與靜態 SQL 去除。 相反地，它們會取代函式呼叫會將陳述式傳遞給 DBMS;相同程式中的靜態 SQL 陳述式的正常處理。  
  
 執行動態 SQL 陳述式的最簡單方式是使用 立即執行的陳述式。 這個陳述式會將 SQL 陳述式傳遞至編譯及執行 DBMS。  
  
 立即執行的陳述式的一個缺點是 DBMS 必須通過每個處理 SQL 陳述式每次執行陳述式時的五個步驟。 此程序中的額外負荷可能十分顯著，如果許多陳述式，以動態方式執行，但它是一種浪費，如果這些陳述式相似。 若要解決這種情況下，動態 SQL 會提供稱為備妥的執行，會使用下列步驟執行的最佳化的方式：  
  
1.  程式建構 SQL 陳述式在緩衝區中，也會立即執行的陳述式。 而不是主機變數問號 （？） 可以取代常數來表示稍後提供的值之常數的陳述式文字中的任何位置。 問號是作為參數標記呼叫。  
  
2.  程式會將 SQL 陳述式傳遞至 DBMS 使用準備陳述式，哪些要求 DBMS，剖析、 驗證及最佳化陳述式和產生執行計畫。 接著，程式會執行準備陳述式，以在稍後使用 EXECUTE 陳述式 （不立即執行陳述式）。 它會傳遞稱為 SQL 資料區或 sqlda 裡的特殊資料結構的陳述式的參數值。  
  
3.  程式可以在 EXECUTE 陳述式重複使用，每次執行時動態的陳述式提供不同的參數值。  
  
 備妥的執行仍未與靜態 SQL 相同。 在靜態 SQL 中，處理 SQL 陳述式的前四個步驟發生在編譯時間。 在已備妥的執行中，這些步驟仍然會在執行階段，但一次; 執行執行計畫在呼叫 EXECUTE 時，才會發生。 這有助於減少動態 SQL 的架構中原本的效能缺點。 下圖顯示靜態 SQL、 立即執行，與動態 SQL 和動態 SQL 搭配備妥的執行之間的差異。
