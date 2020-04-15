---
title: 連線到資料來源 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ae59e0bdb005d296341970f4582100b15a0dfdf7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307709"
---
# <a name="connecting-to-a-data-source-odbc"></a>連接至資料來源 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  配置環境與連接控制代碼，並設定任何連接屬性之後，應用程式會連接到資料來源或驅動程式。 您可以用來連接的函數有三種：  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 有關與資料來源建立連線的詳細資訊,包括可用的各種連線字串選項,請參閱[使用 SQL Server 本機客戶端的連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect**是最簡單的連接功能。 它接受三種參數：資料來源名稱、使用者識別碼與密碼。 當這三個參數包含連接到資料庫所需的所有資訊時,請使用**SQLConnect。** 為此,請使用**SQLDataSources**生成數據源清單。提示使用者輸入數據源、使用者 ID 和密碼;然後呼叫**SQLConnect**。  
  
 **SQLConnect**假定資料來源名稱、使用者 ID 和密碼足以連接到資料源,並且 ODBC 資料來源包含 ODBC 驅動程式進行連接所需的所有其他資訊。 與[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)和[SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)不同 **,SQLConnect**不使用連接字串。  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 當需要比數據源名稱、使用者 ID 和密碼更多的資訊時,將使用**SQLDriverConnect。** **SQLDriverConnect**的參數之一是包含特定於驅動程序的資訊的連接字串。 出於以下原因,您可以使用**SQLDriverConnect**而不是**SQLConnect:**  
  
-   在連接階段指定驅動程式專屬的資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   不使用 ODBC 資料來源連接。  
  
 **SQLDriverConnect**連接字串包含一系列關鍵字值對,用於指定ODBC驅動程式支援的所有連接資訊。 除了供驅動程式支援之所有連接資訊使用的驅動程式專屬關鍵字之外，每個驅動程式還支援標準 ODBC 關鍵字 (DSN、FILEDSN、DRIVER、UID、PWD 和 SAVEFILE)。 **SQLDriverConnect**可用於在沒有資料源的情況下進行連接。 例如,設計用於與實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立"DSN-less"連接的應用程式可以使用連接字串調用**SQLDriverConnect,** 該連接字串定義登入 ID、密碼、網路庫、要連接到的伺服器名稱以及要使用的預設資料庫。  
  
 使用**SQLDriverConnect**時,有兩個選項用於提示使用者輸入任何所需的連線資訊:  
  
-   應用程式對話方塊  
  
     您可以建立一個應用程式對話框,提示連接資訊,然後將**SQLDriverConnect**與 NULL 視窗句柄和*驅動程式完成*設定為SQL_DRIVER_NOPROMPT。 這些參數設定可防止 ODBC 驅動程式開啟自己的對話方塊。 當控制應用程式的使用者介面相當重要時，使用此方法。  
  
-   驅動程式對話方塊  
  
     您可以編寫應用程式代碼,將有效的視窗句柄傳遞給**SQLDriverConnect,** 並將*Driver 完成*參數設定為SQL_DRIVER_COMPLETE、SQL_DRIVER_PROMPT或SQL_DRIVER_COMPLETE_REQUIRED。 接著，驅動程式會產生一個對話方塊來提示使用者輸入連接資訊。 這個方法會簡化應用程式的程式碼。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**,就像**SQLDriverConnect**一樣,使用連接字串。 但是,通過使用**SQLBrowseConnect**,應用程式可以在運行時與數據源反覆運算構造完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建立自己的對話方塊來提示輸入此資訊，藉此保持對其使用者介面的控制。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。  
  
     例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 當**SQLBrowseConnect**完成成功的連接時,它將返回一個連接字串,該字串可用於對**SQLDriverConnect**的後續調用。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式始終在成功的**SQLConnect、SQLDriverConnect**或**SQLBrowseConnect**上返回SQL_SUCCESS_WITH_INFO。 **SQLDriverConnect** 當 ODBC 應用程式在取得SQL_SUCCESS_WITH_INFO後呼叫**SQLGetDiagRec**時,它可以收到以下訊息:  
  
 5701  
 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將使用者的內容放入資料來源中定義的預設資料庫，或在資料來源沒有預設資料庫時，放入針對連接中所使用之登入識別碼所定義的預設資料庫中。  
  
 5703  
 表示在伺服器上所使用的語言。  
  
 下列範例會顯示針對系統管理員之成功連接所傳回的訊息：  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 您可以忽略訊息 5701 和 5703；這些訊息僅供參考。 不過，您不得忽略 SQL_SUCCESS_WITH_INFO 傳回碼，因為可能會傳回 5701 或 5703 之外的訊息。 例如,如果驅動程式連接到運行 具有過期目錄儲存過程的實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]例 的伺服器,則透過**SQLGetDiagRec**在SQL_SUCCESS_WITH_INFO後傳回的錯誤是:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接應用程式的錯誤處理功能應呼叫**SQLGetDiagRec,** 直到它傳回SQL_NO_DATA。 然後,它應對除了*pfNative*代碼為 5701 或 5703 的郵件以外的任何消息執行操作。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL 伺服器通訊 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
