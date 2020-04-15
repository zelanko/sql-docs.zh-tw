---
title: 處理 SQL 語句 |微軟文件
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
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280518"
---
# <a name="processing-a-sql-statement"></a>SQL 陳述式處理
在討論以程式設計方式使用 SQL 的技術之前,有必要討論如何處理 SQL 語句。 所涉及的步驟是所有三種技術的共同步驟,儘管每種技術在不同時間執行它們。 下圖顯示了處理 SQL 語句所涉及的步驟,本節的其餘部分將討論這些步驟。  
  
 ![處理 SQL 陳述式的步驟](../../odbc/reference/media/pr01.gif "pr01")  
  
 要處理 SQL 語句,DBMS 執行以下五個步驟:  
  
1.  DBMS 首先分析 SQL 語句。 它將語句分解為單個單詞(稱為令牌),確保語句具有有效的動詞和有效子句,等等。 在此步驟中可以檢測到語法錯誤和拼寫錯誤。  
  
2.  DBMS 驗證該語句。 它根據系統目錄檢查語句。 語句中命名的所有表是否存在在資料庫中? 是否存在所有列,列名稱是明確的? 使用者是否具有執行語句所需的許可權? 在此步驟中可以檢測到某些語義錯誤。  
  
3.  DBMS 為語句生成訪問計劃。 訪問計劃是執行語句所需的步驟的二進位表示形式;它是等效於可執行代碼的 DBMS。  
  
4.  DBMS 優化訪問計劃。 它探討了執行訪問計劃的各種方法。 索引能否用於加快搜索速度? DBMS 應該首先將搜索條件應用於表 A,然後將其聯接到表 B,還是應該從聯接開始,然後使用搜索條件? 是否可以避免通過表進行順序搜索,也可以縮減為表的子集? 在探索備選方案後,DBMS會選擇其中一個。  
  
5.  DBMS 通過運行訪問計劃來執行語句。  
  
 用於處理 SQL 語句的步驟在所需的資料庫訪問量和花費的時間方面有所不同。 分析 SQL 語句不需要訪問資料庫,而且可以非常快速地完成。 另一方面,優化是一個非常耗費 CPU 的過程,需要訪問系統目錄。 對於複雜的多表查詢,優化器可以探索數千種不同的執行相同查詢的方法。 但是,執行查詢的成本通常很高,以至於在優化中花費的時間比在提高查詢執行速度中所花費的時間要高。 如果可以反覆使用相同的優化訪問計劃來執行重複查詢,則這一點更為重要。
