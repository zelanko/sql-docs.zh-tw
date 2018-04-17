---
title: 內嵌 SQL 範例 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5f6aca6e448a7707394b563f02fe3ca5a31a5424
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="embedded-sql-example"></a>內嵌的 SQL 範例
下列程式碼是簡單內嵌的 SQL 撰寫的程式，在 c 中。程式會說明許多，但不是所有的內嵌 SQL 技術。 程式會提示使用者輸入訂單號碼、 擷取客戶編號、 銷售人員，以及狀態的順序，以及在螢幕上顯示所擷取的資訊。  
  
```  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 請注意下列有關此計劃：  
  
-   **主機變數**加上一節中宣告的主機變數**開始宣告一節**和**結束宣告區段**關鍵字。 每個主機的變數名稱前面加上冒號 （:） 出現在內嵌的 SQL 陳述式時。 冒號允許先行編譯器區別主機變數和資料庫物件，例如資料表和資料行具有相同的名稱。  
  
-   **資料型別**DBMS 和主機語言支援的資料類型可以是相當不同。 這會影響主機變數，因為它們播放雙重角色。 在某一方面，主機變數會是程式變數，宣告，而且操作主機語言陳述式。 相反地，它們用於內嵌的 SQL 陳述式來擷取資料庫資料。 如果沒有對應至 DBMS 資料型別沒有主機語言類型，DBMS 就會自動轉換資料。 不過，因為每個 DBMS 有它自己的規則和轉換程序相關聯的特性，主機變數型別必須仔細選擇。  
  
-   **錯誤處理**DBMS 報告應用程式，透過 SQL 通訊區域中或 SQLCA 的執行階段錯誤。 在上述程式碼範例中，第一個內嵌的 SQL 陳述式會是包含 SQLCA。 這會告訴程式中包含 SQLCA 結構先行編譯器。 這是必要的每當程式會處理由 DBMS 傳回的錯誤。 WHENEVER...GOTO 陳述式會告知先行編譯器產生分支到特定的標記錯誤時，就會發生的錯誤處理程式碼。  
  
-   **單一選取**用來傳回資料的陳述式是單一 SELECT 陳述式; 也就是說，它會傳回單一資料列的資料。 因此，程式碼範例不宣告或使用資料指標。
