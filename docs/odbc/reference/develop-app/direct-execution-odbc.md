---
title: 直接執行 ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305159"
---
# <a name="direct-execution-odbc"></a>直接執行 ODBC
直接執行是執行語句的最簡單方法。 提交語句執行時,數據源將其編譯為訪問計劃,然後執行該訪問計劃。  
  
 直接執行通常用於在運行時生成和執行語句的通用應用程式。 例如,以下代碼產生 SQL 語句並執行一次:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接執行最適合將執行一次的語句。 它的主要缺點是每次執行 SQL 語句時都會對其進行分析。 此外,在執行語句之前,應用程式無法檢索有關語句創建的結果集(如果有)的資訊;如果語句以兩個單獨的步驟準備和執行,則這是可能的。  
  
 要直接執行敘述,應用程式將執行以下操作:  
  
1.  設置任何參數的值。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  呼叫**SQLExecDirect**並傳遞包含 SQL 語句的字串。  
  
3.  呼叫**SQLExecDirect**時,驅動程式:  
  
    -   修改 SQL 語句以使用數據源的 SQL 語法,而不分析 語句;這包括替換[ODBC 中的轉義序列中](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)討論的轉義序列。 應用程式可以通過調用**SQLNativeSql**來檢索 SQL 語句的修改形式。 如果設置了SQL_ATTR_NOSCAN語句屬性,則不會替換轉義序列。  
  
    -   檢索當前參數值並根據需要轉換它們。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   將語句和轉換後的參數值發送到數據源以執行。  
  
    -   返回任何錯誤。 這些包括排序或狀態診斷,如 SQLSTATE 24000(無效游標狀態)、語法錯誤(如 SQLSTATE 42000(語法錯誤或存取衝突)以及語義錯誤,如 SQLSTATE 42S02(找不到基表或視圖)。
