---
title: 內嵌式 SQL 範例 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294169"
---
# <a name="embedded-sql-example"></a>內嵌 SQL 範例
以下代碼是一個簡單的嵌入式 SQL 程式,用 C 編寫。該程式演示了許多(但不是全部)嵌入式 SQL 技術。 程式提示用戶輸入訂單號,檢索客戶編號、銷售人員和訂單狀態,並在螢幕上顯示檢索到的資訊。  
  
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
  
 請注意有關此程式的以下內容:  
  
-   **主機變數**主機變數在由**BEGIN DECLARE C 和****結束聲明節**關鍵字隨附的部分中聲明。 每個主機變數名稱都由冒號(:)當它出現在嵌入的 SQL 語句中時。 冒號允許預編譯器區分具有相同名稱的主機變數和資料庫物件(如表和列)。  
  
-   **資料類型**DBMS 和宿主語言支援的數據類型可能大不相同。 這會影響主機變數,因為它們具有雙重作用。 一方面,主機變數是程式變數,由宿主語言語句聲明和操作。 另一方面,它們用於嵌入式 SQL 語句來檢索資料庫數據。 如果沒有與 DBMS 數據類型對應的主機語言類型,DBMS 將自動轉換數據。 但是,由於每個 DBMS 都有自己的規則和與轉換過程關聯的特性,因此必須仔細選擇主機變數類型。  
  
-   **錯誤處理**DBMS 透過 SQL 通訊區域或 SQLCA 向應用程式報告執行時錯誤。 在前面的代碼示例中,第一個嵌入的 SQL 語句是 INCLUDE SQLCA。 這告訴預編譯器在程式中包括 SQLCA 結構。 每當程式處理 DBMS 傳回的錯誤時,都需要這樣做。 隨時...GOTO 語句告訴預編譯器生成錯誤處理代碼,當發生錯誤時,該代碼分支到特定標籤。  
  
-   **單頓選擇**用於返回數據的語句是單例 SELECT 語句;用於返回數據的語句是單例 SELECT 語句。也就是說,它只返回一行數據。 因此,代碼示例不聲明或使用游標。
