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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306686"
---
# <a name="dynamic-sql"></a>動態 SQL
雖然靜態 SQL 在許多情況下都能順利運作，但還是有一個應用程式類別無法事先判斷資料存取。 例如，假設有一個試算表允許使用者輸入查詢，然後試算表就會將它傳送至 DBMS 來抓取資料。 撰寫試算表程式時，程式設計人員顯然無法得知此查詢的內容。  
  
 為了解決這個問題，試算表使用一種內嵌 SQL 的形式，稱為動態 SQL。 不同于程式中硬式編碼的靜態 SQL 語句，可以在執行時間建立動態 SQL 語句，並將其放在字串主機變數中。 然後將它們傳送至 DBMS 進行處理。 因為 DBMS 必須在執行時間針對動態 SQL 語句產生存取計畫，所以動態 SQL 的速度通常會比靜態 SQL 慢。 當編譯包含動態 SQL 語句的程式時，不會從程式中移除動態 SQL 語句，如同在靜態 SQL 中。 相反地，它們會由將語句傳遞至 DBMS 的函式呼叫所取代。相同程式中的靜態 SQL 語句會正常處理。  
  
 執行動態 SQL 語句最簡單的方式是使用 EXECUTE IMMEDIATE 語句。 此語句會將 SQL 語句傳遞至 DBMS，以進行編譯和執行。  
  
 EXECUTE IMMEDIATE 語句的一個缺點是，DBMS 必須在每次執行語句時，逐一處理 SQL 語句的每個步驟。 如果您以動態方式執行許多語句，此程式所牽涉到的負擔可能會很大，而且如果這些語句很類似，就會浪費成本。 為了解決這種情況，動態 SQL 提供了一種稱為「備妥執行」的優化形式執行，其使用下列步驟：  
  
1.  程式會在緩衝區中建立 SQL 語句，就如同對 EXECUTE IMMEDIATE 語句所做的一樣。 問號（？）可以取代語句文字中的常數，以指出稍後將會提供常數的值，而不是主機變數。 問號會當做參數標記來呼叫。  
  
2.  程式會使用 PREPARE 語句將 SQL 語句傳遞至 DBMS，要求 DBMS 剖析、驗證和優化語句，並為其產生執行計畫。 然後，程式會使用 EXECUTE 語句（而不是 EXECUTE IMMEDIATE 語句），稍後再執行 PREPARE 語句。 它會透過稱為 SQL 資料區域或 SQLDA 的特殊資料結構，傳遞語句的參數值。  
  
3.  程式可以重複使用 EXECUTE 語句，並在每次執行動態語句時提供不同的參數值。  
  
 備妥的執行仍然與靜態 SQL 不相同。 在靜態 SQL 中，處理 SQL 語句的前四個步驟會在編譯時期進行。 在備妥的執行中，這些步驟仍會在執行時間進行，但是只會執行一次。只有在呼叫 EXECUTE 時，才會執行計畫。 這有助於消除動態 SQL 架構中固有的部分效能缺點。 下圖顯示靜態 SQL、具有立即執行的動態 SQL，以及具有備妥執行的動態 SQL 之間的差異。
