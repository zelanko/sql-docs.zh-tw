---
description: SQL 陳述式處理
title: 處理 SQL 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4ce614f6dcf4c1fe0ab1e1c806b966b4267e7fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476215"
---
# <a name="processing-a-sql-statement"></a>SQL 陳述式處理
在討論以程式設計方式使用 SQL 的技巧之前，必須先討論如何處理 SQL 語句。 所有三種技術都有共通的相關步驟，雖然每種技巧都在不同的時間執行。 下圖顯示處理 SQL 語句所需的步驟，這些步驟將在本節的其餘部分討論。  
  
 ![處理 SQL 陳述式的步驟](../../odbc/reference/media/pr01.gif "pr01")  
  
 為了處理 SQL 語句，DBMS 會執行下列五個步驟：  
  
1.  DBMS 會先剖析 SQL 語句。 它會將語句分成個別的單字（稱為 token），確定語句具有有效的動詞和有效的子句等等。 您可以在此步驟中偵測到語法錯誤和拼寫錯誤。  
  
2.  DBMS 會驗證語句。 它會檢查系統目錄的語句。 語句中的所有資料表都存在於資料庫中嗎？ 所有資料行都存在，而且資料行名稱是否明確？ 使用者是否具有執行語句的必要許可權？ 此步驟可以偵測到某些語意錯誤。  
  
3.  DBMS 會產生語句的存取計畫。 存取計畫是執行語句所需之步驟的二進位標記法;它是相當於可執行程式碼的 DBMS。  
  
4.  DBMS 會優化存取計畫。 它會探索執行存取計畫的各種方式。 是否可以使用索引來加速搜尋？ 如果 DBMS 先將搜尋條件套用至資料表 A，然後將它加入至資料表 B，或應該從聯結開始，然後再使用搜尋條件？ 是否可以將資料表的連續搜尋避免或縮減為數據表的子集？ 探索替代方案之後，DBMS 會選擇其中一種。  
  
5.  DBMS 會執行存取計畫來執行語句。  
  
 用來處理 SQL 語句的步驟，會隨著所需的資料庫存取量以及它們所需的時間量而有所不同。 剖析 SQL 語句不需要存取資料庫，而且可以很快速地完成。 另一方面，優化是需要大量 CPU 的進程，而且需要存取系統目錄。 針對複雜的 multitable 查詢，優化工具可能會探索數千種不同的方式來執行相同的查詢。 不過，執行查詢效率不高的成本通常很高，因為優化所花費的時間，會比在查詢執行速度增加時重新產生更高。 如果可以多次使用相同的優化存取計畫來執行重複的查詢，這會更有意義。
