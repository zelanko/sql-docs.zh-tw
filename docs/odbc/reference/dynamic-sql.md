---
title: 動態 SQL |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306686"
---
# <a name="dynamic-sql"></a>動態 SQL
儘管靜態 SQL 在許多情況下工作良好,但有一類應用程式無法提前確定數據訪問。 例如,假設電子表格允許使用者輸入查詢,然後電子錶格將查詢發送到 DBMS 以檢索數據。 編寫電子表格程式時,程式師顯然無法知道此查詢的內容。  
  
 為了解決此問題,電子表格使用一種稱為動態 SQL 的嵌入式 SQL 形式。 與靜態 SQL 語句(在程式中硬編碼)不同,動態 SQL 語句可以在運行時生成並放置在字串主機變數中。 然後,它們將發送到 DBMS 進行處理。 由於 DBMS 必須在執行時為動態 SQL 語句生成訪問計畫,因此動態 SQL 通常比靜態 SQL 慢。 編譯包含動態 SQL 語句的程式時,動態 SQL 語句不會從程式中剝離,如靜態 SQL 中那樣。 相反,它們被將語句傳遞給 DBMS 的函數調用替換;同一程式中的靜態 SQL 語句得到正常處理。  
  
 執行動態 SQL 語句的最簡單方法是使用 EXECUTE 立即文句。 此語句將 SQL 語句傳遞給 DBMS 進行編譯和執行。  
  
 EXECUTE 立即語句的一個缺點是,每次執行語句時,DBMS 都必須執行處理 SQL 語句的五個步驟中的每個步驟。 如果動態執行許多語句,則此過程所涉及的開銷可能很大,如果這些語句相似,則浪費。 為了解決此問題,動態 SQL 提供了一種優化的執行形式,稱為準備執行,它使用以下步驟:  
  
1.  程式在緩衝區中構造 SQL 語句,就像執行立即語句一樣。 可以代替宿主變數,將問號 (?) 替換為語句文本中任意位置的常量,以指示稍後將提供常量的值。 問號稱為參數標記。  
  
2.  程式使用 PREPARE 語句將 SQL 語句傳遞給 DBMS,該語句請求 DBMS 解析、驗證和優化該語句併為其生成執行計劃。 然後,程式使用 EXECUTE 語句(而不是 EXECUTE 立即文句)在以後執行 PREPARE 語句。 它通過稱為 SQL 資料區域或 SQLDA 的特殊數據結構傳遞語句的參數值。  
  
3.  程式可以重複使用 EXECUTE 語句,每次執行動態語句時提供不同的參數值。  
  
 準備執行仍與靜態 SQL 不同。 在靜態 SQL 中,處理 SQL 語句的前四個步驟發生在編譯時。 在準備執行時,這些步驟仍發生在運行時,但它們只執行一次;計劃執行僅在調用 EXECUTE 時執行。 這有助於消除動態 SQL 體系結構中固有的一些性能劣勢。 下圖顯示了靜態 SQL、具有即時執行的動態 SQL 和具有準備執行的動態 SQL 之間的區別。
