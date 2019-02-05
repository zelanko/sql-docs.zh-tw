---
title: 處理錯誤 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 535881ed3ece30996390af6c9a22568d49bc6d3e
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736961"
---
# <a name="handling-errors"></a>處理錯誤
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，所有資料庫錯誤狀況都會使用 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 類別，當作例外狀況傳回至 Java 應用程式。 SQLServerException 類別的下列方法是繼承自 java.sql.SQLException 和 java.lang.Throwable；它們可以用來傳回有關所發生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的特定資訊：  
  
-   `getSQLState()` 傳回例外狀況的標準 X/Open 或 SQL99 狀態碼。
  
-   `getErrorCode()` 傳回特定的資料庫錯誤號碼。
  
-   `getMessage()` 傳回例外狀況的全文。 錯誤訊息文字會描述問題，而且通常包括顯示錯誤訊息時會插入其中的資訊之預留位置，例如物件名稱。
  
-   `getNextException()` 傳回下一個 `SQLServerException` 物件，如果沒有其他例外狀況物件要傳回，則傳回 Null。

-   `getSQLServerError()` 傳回`SQLServerError`物件，其中包含有關例外狀況的詳細的資訊，接收從 SQL Server。 這個方法會傳回 null，如果沒有發生任何伺服器錯誤。

下列方法`SQLServerError`類別可用來取得從伺服器產生的錯誤相關的其他詳細資料。

-   `SQLServerError.getErrorMessage()` 傳回從伺服器收到的錯誤訊息。

-   `SQLServerError.getErrorNumber()` 傳回數字，識別錯誤的類型。

-   `SQLServerError.getErrorState()` 從表示錯誤、 警告或 「 找不到資料 」 訊息的 SQL Server 傳回的數值錯誤碼。

-   `SQLServerError.getErrorSeverity()` 傳回所收到的錯誤的嚴重性層級。

-   `SQLServerError.getServerName()` 傳回正在執行的 SQL Server 執行個體之電腦的名稱產生錯誤。

-   `SQLServerError.getProcedureName()` 傳回遠端程序呼叫 (RPC) 產生錯誤之預存程序的名稱。

-   `SQLServerError.getLineNumber()` 傳回內的 TRANSACT-SQL 命令批次或預存程序產生錯誤的行號。
  
 在下列範例中，連至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入函式，並會建構一個格式錯誤的 SQL 陳述式，它不含 FROM 子句。 然後，會執行此陳述式，並處理 SQL 例外狀況。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
