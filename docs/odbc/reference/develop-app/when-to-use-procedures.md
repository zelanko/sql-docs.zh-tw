---
title: "當使用程序 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7bae5e984d66d8b71a9e4b84708f3ea126c1e0b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="when-to-use-procedures"></a>當使用程序
有使用程序的優點，所有基礎的使用程序的 SQL 陳述式從移到資料來源的應用程式。 應用程式中不會變是互通的程序呼叫。 這些優點包括：  
  
-   **效能**程序通常是最快速的方式來執行 SQL 陳述式。 像備妥的執行，此陳述式是編譯和執行以兩個不同的步驟。 不同於備妥的執行程序只能在執行階段執行。 而是在不同的時間進行編譯。  
  
-   **商務規則**A*商務規則*是關於相同所在公司商務規則。 例如，具有一個銷售人員的標題可能允許加入新的銷售訂單。 在程序中放置這些規則可讓個別公司自訂垂直應用程式的重寫應用程式而不需要修改應用程式程式碼呼叫的程序。 例如，訂單輸入應用程式可能會呼叫程序**InsertOrder**具有固定數目的參數; 方式**InsertOrder**實作可能會不同公司的公司。  
  
-   **可取代性**密切相關放置程序中的商務規則是程序，可以取代不需要重新編譯應用程式的事實。 如果商務規則變更公司已購買並安裝應用程式之後，公司可以變更含有該規則的程序。 從應用程式的觀點來看，沒有任何變更。它仍會呼叫特定程序來完成特定工作。  
  
-   **DBMS 專屬 SQL**程序提供應用程式利用 DBMS 專屬 SQL，並仍然可互通的方式。 例如，DBMS 在 SQL 中支援的流程控制陳述式上的程序可能截獲並復原錯誤，而上不支援的流程控制陳述式 DBMS 的程序可能只會傳回錯誤。  
  
-   **程序未被交易**某些資料來源，在認可或回復交易時，會刪除所有完成準備的陳述式的存取計畫的連接上。 將 SQL 陳述式放在永久儲存在資料來源，程序的陳述式繼續執行的交易。 是否程序會存留在備妥，部分備妥，或已取消準備的狀態是 DBMS 專屬。  
  
-   **區隔開發**可以個別開發程序，從應用程式的其餘部分。 在大型企業，這可能會提供方法，以進一步利用非常特殊的程式設計人員的技能。 換句話說，應用程式設計人員可以撰寫使用者介面程式碼，以及資料庫程式設計人員可以撰寫程序。  
  
 垂直和自訂應用程式通常會使用程序。 這些應用程式通常執行固定的工作，而且可在其中的硬式編碼程序呼叫。 例如，訂單輸入應用程式可能會呼叫程序**InsertOrder**， **DeleteOrder**， **UpdateOrder**，和**GetOrders**.  
  
 沒有什麼道理，從一般應用程式呼叫程序。 程序通常撰寫特定的應用程式的內容中執行的工作，因此有任何使用泛型應用程式。 例如，試算表有理由来呼叫**InsertOrder**剛才所提到的程序。 此外，泛型應用程式不應該建構程序在執行階段，想要提供更快的陳述式執行。不只是要低於備妥或直接執行，這可能也需要 DBMS 特定 SQL 陳述式。  
  
 這個例外狀況是應用程式開發環境，其通常會提供方法來建立 SQL 陳述式來執行程序，可能會提供方法，讓測試程序的程式設計人員的程式設計人員。 這類環境呼叫**SQLProcedures**清單可用的程序和**SQLProcedureColumns**列出輸入、 輸入/輸出和輸出參數，程序會傳回值和資料行程序所建立的任何結果集。 不過，這類程序必須開發事先上每個資料來源;這樣做需要 DBMS 特定 SQL 陳述式。  
  
 有三個主要缺點使用程序。 第一個是程序必須撰寫和編譯的應用程式是執行每個 DBMS。 雖然這不是自訂應用程式的問題，它可以大幅提高開發和維護時間垂直設計以數字的 Dbms 執行的應用程式。  
  
 第二個缺點是，有許多 Dbms 不支援程序。 同樣地，這是最可能是設計成以數字的 Dbms 執行垂直應用程式的問題。 若要判斷是否支援程序，應用程式呼叫**SQLGetInfo** SQL_PROCEDURES 選項。  
  
 第三個缺點則是特別適用於應用程式開發環境，是 ODBC 不會定義標準文法建立程序。 也就是說，雖然應用程式可以 interoperably 呼叫程序，他們無法建立它們 interoperably。
