---
title: 在執行時間所建立的 SQL 語句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8333000c9bb806116244ac6d4f654fa195205868
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107466"
---
# <a name="sql-statements-constructed-at-run-time"></a>在執行階段建構 SQL 陳述式
執行臨機操作分析的應用程式通常會在執行時間建立 SQL 語句。 例如，試算表可能會允許使用者選取要從中取出資料的資料行：  
  
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
  
 在執行時間經常用來建立 SQL 語句的另一種應用程式類別是應用程式開發環境。 不過，它們所建造的語句會在其所建立的應用程式中進行硬式編碼，通常可以進行優化和測試。  
  
 在執行時間建立 SQL 語句的應用程式可以為使用者提供極大的彈性。 如先前的範例所示，它甚至不支援像是**where**子句、 **ORDER BY**子句或聯結之類的一般作業，在執行時間建立 SQL 語句比硬式編碼語句更為複雜。 此外，測試這類應用程式會有問題，因為它們可以建立任意數目的 SQL 語句。  
  
 在執行時間建立 SQL 語句的可能缺點是，比使用硬式編碼語句所花的時間更久。 幸好，這不是很重要的問題。 這類應用程式通常會需要大量使用者介面，而應用程式花在建立 SQL 語句的時間，與使用者花費在輸入準則的時間一般很小。
