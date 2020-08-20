---
description: 動態 SQL
title: 動態 SQL |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de711543748a91015a9aa0d4cb8aadb011744306
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494579"
---
# <a name="dynamic-sql"></a>動態 SQL
雖然靜態 SQL 在許多情況下都能順利運作，但還是有一個應用程式類別無法事先判斷資料存取。 例如，假設試算表允許使用者輸入查詢，試算表接著會將該查詢傳送至 DBMS 以取得資料。 撰寫試算表程式時，程式設計人員顯然無法得知這項查詢的內容。  
  
 若要解決這個問題，試算表會使用一種稱為動態 SQL 的內嵌 SQL 形式。 不同于在程式中硬式編碼的靜態 SQL 語句，可以在執行時間建立動態 SQL 語句，並放入字串主機變數中。 然後將它們傳送至 DBMS 進行處理。 因為 DBMS 必須在執行時間為動態 SQL 語句產生存取計畫，所以動態 SQL 的速度通常會比靜態 SQL 慢。 當編譯包含動態 SQL 語句的程式時，不會從程式中移除動態 SQL 語句，如同在靜態 SQL 中一樣。 相反地，它們會由將語句傳遞至 DBMS 的函式呼叫取代;相同程式中的靜態 SQL 語句會正常處理。  
  
 執行動態 SQL 語句最簡單的方式是使用 EXECUTE IMMEDIATE 語句。 這個語句會將 SQL 語句傳遞至 DBMS 以進行編譯和執行。  
  
 EXECUTE IMMEDIATE 語句的其中一個缺點是，DBMS 必須在每次執行語句時，逐一處理 SQL 語句的五個步驟。 如果有許多語句是以動態方式執行，則此程式所牽涉到的負擔可能會很大，而且如果這些語句很類似，則會很浪費。 為了解決這種情況，動態 SQL 提供了一種優化形式的執行，稱為「準備執行」，其會使用下列步驟：  
  
1.  程式會在緩衝區中建立 SQL 語句，就如同在 EXECUTE IMMEDIATE 語句中一樣。 問號 (？ ) 可以取代為語句文字中任何位置的常數，以指出稍後將會提供常數的值，而不是主變數。 問號稱為「參數標記」（parameter 標記）。  
  
2.  此程式會使用 PREPARE 語句將 SQL 語句傳遞給 DBMS，這會要求 DBMS 剖析、驗證及優化語句，並為其產生執行計畫。 然後，程式會使用 EXECUTE 語句 (不是 EXECUTE IMMEDIATE 語句) 稍後再執行 PREPARE 語句。 它會透過稱為 SQL 資料區域或 SQLDA 的特殊資料結構，傳遞語句的參數值。  
  
3.  此程式可以重複使用 EXECUTE 語句，每次執行動態語句時都提供不同的參數值。  
  
 備妥的執行仍與靜態 SQL 不同。 在靜態 SQL 中，處理 SQL 語句的前四個步驟會在編譯時期進行。 在備妥的執行中，這些步驟仍會在執行時間執行，但只會執行一次：只有在呼叫 EXECUTE 時，才會執行方案。 這有助於消除動態 SQL 架構中固有的一些效能缺點。
