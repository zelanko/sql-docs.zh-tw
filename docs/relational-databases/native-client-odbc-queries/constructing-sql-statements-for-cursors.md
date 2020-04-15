---
title: 為游標構造 SQL 語句 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0e422be747c2b47dacb1feb97ba6c00fa1131fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291398"
---
# <a name="constructing-sql-statements-for-cursors"></a>建構資料指標的 SQL 陳述式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式使用伺服器游標來實現 ODBC 規範中定義的游標功能。 ODBC 應用程式使用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來控制游標行為,從而設置不同的語句屬性。 下面是這些屬性及其預設值。  
  
|屬性|預設|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 當在執行 SQL 語句時將這些選項設定為其預設值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時, 本機用戶端 ODBC 驅動程式不使用伺服器游標來實現結果集;因此,本機用戶端 ODBC 驅動程式不會使用伺服器游標來實現結果集。相反,它使用默認結果集。 如果在執行 SQL 語句時,這些選項中的任何一個都與其預設值發生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]更改, 本機用戶端 ODBC 驅動程式將嘗試使用伺服器游標來實現結果集。  
  
 預設結果集支援所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 使用預設結果集時，可執行的 SQL 陳述式類型沒有任何限制。  
  
 伺服器資料指標不支援所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 伺服器資料指標不支援任何產生多個結果集的 SQL 陳述式。  
  
 伺服器資料指標不支援下列陳述式類型：  
  
-   批次  
  
     根據兩個或多個個別 SQL SELECT 陳述式所建立的 SQL 陳述式，例如：  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   具有多個 SELECT 陳述式的預存程序  
  
     執行包含多個 SELECT 陳述式之預存程序的 SQL 陳述式。 這包括填入參數或變數的 SELECT 陳述式。  
  
-   關鍵字  
  
     包含 FOR BROWSE 或 INTO 關鍵字的 SQL 陳述式。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果與其中任何條件相符的 SQL 陳述式是使用伺服器資料指標執行，此伺服器資料指標就會隱含轉換成預設結果集。 **SQLExecDirect**或**SQLExecute**返回SQL_SUCCESS_WITH_INFO後,遊標屬性將設置回其默認設置。  
  
 不符合上述類別目錄的 SQL 陳述式可以使用任何陳述式屬性設定執行。它們的運作方式就如同預設結果集或伺服器資料指標。  
  
## <a name="errors"></a>Errors  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和更新版本中，如果嘗試執行產生多個結果集的陳述式，就會產生 SQL_SUCCESS_WITH INFO 和下列訊息：  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 接收此消息的 ODBC 應用程式可以調用[SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)以確定當前的游標設置。  
  
 如果使用伺服器資料指標時嘗試執行具有多個 SELECT 陳述式的程序，就會產生下列錯誤：  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 如果使用伺服器資料指標時嘗試執行具有多個 SELECT 陳述式的批次，就會產生下列錯誤：  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 收到這些錯誤的 ODBC 應用程式必須將所有資料指標陳述式屬性重設為其預設值，然後再嘗試執行此陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
