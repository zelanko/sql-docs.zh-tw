---
title: 動態 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbecd1d6db1d5ed77082253f6a6a57a96ceec4d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748399"
---
# <a name="dynamic-sql"></a>動態 SQL
雖然靜態 SQL 也適用於多種情況，還有無法事先判斷資料存取的應用程式類別。 例如，假設試算表，讓使用者能夠輸入的查詢，試算表然後傳送到 DBMS 以擷取資料。 此查詢的內容很明顯地無法得知程式設計人員寫入試算表程式時。  
  
 若要解決此問題，試算表會使用一種稱為動態 SQL 的內嵌 SQL。 不同靜態 SQL 陳述式，也就是硬式編碼在程式中，於動態 SQL 陳述式可以在執行階段建置並放在字串的主應用程式變數。 他們再傳送到 DBMS 進行處理。 DBMS 必須產生動態 SQL 陳述式的執行階段存取計劃，因為動態 SQL 低於一般靜態 SQL。 包含動態 SQL 陳述式的程式編譯時，動態 SQL 陳述式不會從程式，如同靜態 SQL 中移除。 相反地，它們會取代函式呼叫的陳述式給 DBMS;在同一個程式中的靜態 SQL 陳述式的正常處理。  
  
 執行動態 SQL 陳述式的最簡單方式是使用 立即執行的陳述式。 此陳述式會將 SQL 陳述式傳遞至進行編譯和執行 DBMS。  
  
 立即執行的陳述式的缺點是 DBMS 必須通過每個處理 SQL 陳述式每次執行陳述式時的五個步驟。 如果許多陳述式，以動態方式執行，而且如果這些陳述式與底下類似，它是一種浪費，此程序所涉及的額外負荷很可觀。 若要解決這種情況下，動態 SQL 會提供稱為備妥的執行，使用下列步驟執行的最佳化的形式：  
  
1.  程式會建構 SQL 陳述式在緩衝區中，就如同直接執行陳述式。 而不是主機變數來表示常數的值將會稍後提供的陳述式文字中的任何位置的常數的問號 （？） 都可以取代。 問號是作為參數標記呼叫。  
  
2.  程式會將 SQL 陳述式傳遞至 DBMS，使用哪些要求 DBMS，剖析、 驗證及最佳化陳述式及產生執行規劃的準備陳述式。 接著，程式會執行準備陳述式，以在稍後使用 EXECUTE 陳述式 （不立即執行陳述式）。 它會傳遞透過稱為 SQL 資料區域或 sqlda 裡的特殊資料結構的陳述式的參數值。  
  
3.  程式可以在 EXECUTE 陳述式重複使用，每次執行時動態的陳述式提供不同的參數值。  
  
 備妥的執行仍不是靜態 SQL 相同。 在靜態 SQL 中，處理 SQL 陳述式的前四個步驟進行編譯時期。 在已備妥的執行中，這些步驟仍在執行階段，會發生，但它們都只執行一次;執行計畫時，才會呼叫 EXECUTE。 這有助於避免的一些架構中的動態 SQL 的固有效能缺點。 下圖顯示靜態 SQL、 立即執行，使用動態 SQL 和動態 SQL 搭配備妥的執行之間的差異。
