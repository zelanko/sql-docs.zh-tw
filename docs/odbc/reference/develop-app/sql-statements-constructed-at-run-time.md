---
description: 在執行階段建構 SQL 陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff9f7a4e579ce4e1d1177b8f5fa67f7d13a4fdc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424550"
---
# <a name="sql-statements-constructed-at-run-time"></a>在執行階段建構 SQL 陳述式
執行特定分析的應用程式通常會在執行時間建立 SQL 語句。 例如，試算表可能可讓使用者選取要從中取得資料的資料行：  
  
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
  
 在執行時間通常會建立 SQL 語句的另一種應用程式類別是應用程式開發環境。 不過，它們所建立的語句會在其所建立的應用程式中硬式編碼，通常可以進行優化和測試。  
  
 在執行時間建立 SQL 語句的應用程式，可為使用者提供極大的彈性。 如同上述範例所示，它甚至不支援像 **WHERE** 子句、 **ORDER BY** 子句或聯結這樣的一般作業，在執行時間建立 SQL 語句會比硬式編碼的語句更為複雜。 此外，測試這類應用程式有問題，因為它們可以建立任意數目的 SQL 語句。  
  
 在執行時間建立 SQL 語句的潛在缺點是，要比使用硬式編碼的語句更多時間來建立語句。 幸運的是，這不是很重要的問題。 這類應用程式通常會耗用大量使用者介面，相較于使用者花在輸入準則的時間，應用程式花在建立 SQL 語句的時間通常很小。
