---
title: 已準備好的執行 ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282308"
---
# <a name="prepared-execution-odbc"></a>備妥的執行 ODBC
準備執行是多次執行語句的有效方法。 該語句首先編譯或*準備*到訪問計劃中。 然後,稍後將執行一次或多次訪問計劃。 有關存取計畫的詳細資訊,請參閱處理[SQL 語句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 垂直和自訂應用程式通常使用準備執行來重複執行相同的參數化 SQL 語句。 例如,以下代碼準備一個語句來更新不同部件的價格。 然後,它每次使用不同的參數值多次執行語句。  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 準備執行比多次執行語句的直接執行快,這主要是因為語句只編譯一次;每次執行語句時,都會編譯直接執行的語句。 準備好的執行還可以減少網路流量,因為如果數據源支援訪問計劃標識符,則驅動程式可以在每次執行語句時向數據源發送訪問計劃標識符,而不是整個 SQL 語句。  
  
 應用程式可以在準備語句后和執行語句之前檢索結果集的元數據。 但是,返回已準備好的未執行語句的元數據對於某些驅動程序來說非常昂貴,如果可能,應避免互操作應用程式。 有關詳細資訊,請參閱[結果集中資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 備妥的執行不應該用於單次執行的陳述式。 對於此類語句,它比直接執行稍慢,因為它需要額外的ODBC函數調用。  
  
> [!IMPORTANT]  
>  通過顯式調用**SQLEndTran**或以自動提交模式工作來提交或回滾事務,會導致某些數據源刪除連接上所有語句的訪問計畫。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明中SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR選項。  
  
 要準備和執行語句,應用程式:  
  
1.  呼叫**SQLPrepare**並傳遞包含 SQL 語句的字串。  
  
2.  設置任何參數的值。 參數實際上可以在準備語句之前或之後設置。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
3.  呼叫**SQLExecute**並執行任何必要的其他處理,例如提取資料。  
  
4.  根據需要重複步驟 2 和 3。  
  
5.  呼叫**SQLPrepare**時,驅動程式:  
  
    -   修改 SQL 語句以使用數據來源的 SQL 語法,而無需分析該語句。 這包括替換[ODBC 中的轉義序列中](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)討論的轉義序列。 應用程式可以通過調用**SQLNativeSql**來檢索 SQL 語句的修改形式。 如果設置了SQL_ATTR_NOSCAN語句屬性,則不會替換轉義序列。  
  
    -   將語句發送到數據源進行準備。  
  
    -   存儲返回的訪問計劃標識符以備以後執行(如果準備成功)或返回任何錯誤(如果準備失敗)。 錯誤包括語法錯誤,如 SQLSTATE 42000(語法錯誤或訪問衝突)和語義錯誤,如 SQLSTATE 42S02(找不到基本表或檢視)。  
  
        > [!NOTE]  
        >  某些驅動程式此時不返回錯誤,而是在執行語句或調用目錄函數時返回錯誤。 因此 **,SQLPrepare**在實際上出現故障時可能似乎已經成功。  
  
6.  呼叫**SQLExecute**時,驅動程式:  
  
    -   檢索當前參數值並根據需要轉換它們。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   將訪問計畫識別碼和轉換的參數值發送到資料來源。  
  
    -   返回任何錯誤。 這些通常是運行時錯誤,如 SQLSTATE 24000(無效游標狀態)。 但是,此時某些驅動程式返回語法和語義錯誤。  
  
 如果數據源不支援語句準備,驅動程式必須盡可能類比它。 例如,在調用**SQLPrepare**時,驅動程式可能不執行任何操作,然後在調用**SQLExecute**時直接執行語句。  
  
 如果數據源支援不執行的語法檢查,驅動程式可能會提交語句以在調用**SQLPrepare**時進行檢查,並在調用**SQLExecute**時提交語句以執行。  
  
 如果驅動程式無法類比語句準備,它將在調用**SQLPrepare**時儲存語句,並在調用**SQLExecute**時提交該語句以執行。  
  
 由於類比語句準備不完美 **,SQLExecute**可以返回**SQLPrepare**通常返回的任何錯誤。
