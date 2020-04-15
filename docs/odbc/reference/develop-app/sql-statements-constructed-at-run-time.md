---
title: 執行時建構的 SQL 語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301969"
---
# <a name="sql-statements-constructed-at-run-time"></a>在執行階段建構 SQL 陳述式
執行暫時分析的應用程式通常在執行時生成 SQL 語句。 例如,電子表格可能允許使用者選擇要從中檢索資料的列:  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 通常在執行時建構 SQL 語句的另一類應用程式是應用程式開發環境。 但是,它們構造的語句在構建的應用程式中是硬編碼的,通常可以在其中對其進行優化和測試。  
  
 在運行時建構 SQL 語句的應用程式可以為使用者提供極大的靈活性。 從前面的示例中可以看出,它甚至不支援**像 WHERE**子句 **、ORDER BY**子句或聯接這樣的常見操作,在運行時構造 SQL 語句比硬編碼語句複雜得多。 此外,測試此類應用程式存在問題,因為它們可以構造任意數量的 SQL 語句。  
  
 在運行時建構 SQL 語句的潛在缺點是,構建語句所需的時間比使用硬編碼語句的時間要多得多。 幸運的是,這很少是一個問題。 此類應用程式往往佔用使用者介面,與使用者輸入條件的時間相比,應用程式構建 SQL 語句所花費的時間通常很小。
