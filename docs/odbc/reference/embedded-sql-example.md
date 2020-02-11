---
title: 內嵌 SQL 範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 966962bdda79a57e83a0bce06b9254267efb474c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068664"
---
# <a name="embedded-sql-example"></a>內嵌 SQL 範例
下列程式碼是簡單的內嵌 SQL 程式，以 C 撰寫。此程式說明許多（但非全部）的內嵌 SQL 技術。 此程式會提示使用者輸入訂單號碼、抓取客戶編碼、銷售人員和訂單狀態，並在螢幕上顯示已抓取的資訊。  
  
```cpp  
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
  
 請注意下列關於此計畫的事項：  
  
-   **主機變數**主機變數會在以**BEGIN DECLARE 區段**和**END declare 區段**關鍵字括住的區段中宣告。 每個主機變數名稱的前面會加上冒號（:)當它出現在內嵌 SQL 語句中時。 冒號可讓先行編譯器區別具有相同名稱的主機變數與資料庫物件（例如資料表和資料行）。  
  
-   **資料類型**DBMS 和主機語言所支援的資料類型可能會有相當大的不同。 這會影響主機變數，因為它們扮演雙重角色。 一方面，主機變數是程式變數，由主語言語句宣告和操作。 另一方面，它們會用於內嵌 SQL 語句來抓取資料庫資料。 如果沒有對應至 DBMS 資料類型的主控制項語言類型，DBMS 會自動轉換資料。 不過，因為每個 DBMS 都有自己的規則和特性與轉換程式相關聯，所以必須謹慎選擇主機變數類型。  
  
-   **錯誤處理**DBMS 會透過 SQL 通訊區域或 SQLCA，向應用程式的運行時錯誤報表。 在上述程式碼範例中，第一個內嵌 SQL 語句包括 [SQLCA]。 這會告訴先行編譯器在程式中包含 SQLCA 結構。 每當程式將處理 DBMS 傳回的錯誤時，就必須這麼做。 當 .。。GOTO 語句會指示先行編譯器在發生錯誤時，產生分支至特定標籤的錯誤處理常式代碼。  
  
-   **單一選取**用來傳回資料的語句是單一 SELECT 語句;也就是說，它只會傳回單一資料列。 因此，此程式碼範例不會宣告或使用資料指標。
