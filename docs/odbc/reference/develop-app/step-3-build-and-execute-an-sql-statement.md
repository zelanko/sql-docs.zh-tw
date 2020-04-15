---
title: 第 3 步:生成並執行 SQL 語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8322cf5e7b4a91bfc5f5f0204cfb25fa4bdad92
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306829"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步驟 3：建立和執行 SQL 陳述式
第三步是生成並執行 SQL 語句,如下圖所示。 用於執行此步驟的方法可能會有很大差異。 應用程式可能會提示使用者輸入 SQL 語句、基於使用者輸入生成 SQL 語句或使用硬編碼 SQL 語句。 有關詳細資訊,請參閱建構[SQL 語句](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![顯示 SQL 陳述式的建置和執行](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 語句包含參數,則應用程式通過為每個參數調用**SQLBind 參數**將它們綁定到應用程式變數。 有關詳細資訊,請參閱[敘述參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 生成 SQL 語句並綁定任何參數後,該語句將使用**SQLExecDirect**執行。 如果文句將執行多次,則可以使用**SQLPrepare 準備**,並使用**SQLExecute 執行**。 有關詳細資訊,請參閱[執行語句](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 應用程式還可能完全放棄執行 SQL 語句,而是調用函數來返回包含目錄資訊的結果集,如可用的列或表。 關於詳細資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 應用程式的下一個操作取決於所執行的 SQL 語句的類型。  
  
|SQL 語句的類型|繼續|  
|---------------------------|----------------|  
|**選擇**或目錄功能|[步驟 4a：擷取結果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**、**刪除**或**插入**|[步驟 4b：擷取資料列計數](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 語句|步驟 3:生成和執行 SQL 語句(本主題)或[步驟 5:提交事務](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
