---
description: 連接至資料來源 (ODBC)
title: 連接到 (ODBC) 的資料來源 |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dabf2e0c4fe2f23ad5dee576c73a2bafdb67a8be
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464949"
---
# <a name="connecting-to-a-data-source-odbc"></a>連接至資料來源 (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  配置環境與連接控制代碼，並設定任何連接屬性之後，應用程式會連接到資料來源或驅動程式。 您可以用來連接的函數有三種：  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 如需有關建立資料來源連接的詳細資訊，包括可用的各種連接字串選項，請參閱 [使用連接字串關鍵字搭配 SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** 是最簡單的連接函數。 它接受三種參數：資料來源名稱、使用者識別碼與密碼。 當這三個參數包含連接到資料庫所需的所有資訊時，請使用 **SQLConnect** 。 若要這樣做，請使用 **SQLDataSources** 建立資料來源的清單。提示使用者提供資料來源、使用者識別碼和密碼;然後呼叫 **SQLConnect**。  
  
 **SQLConnect** 會假設資料來源名稱、使用者識別碼和密碼都足以連接到資料來源，而且 odbc 資料來源包含 odbc 驅動程式建立連接所需的所有其他資訊。 不同于 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 和 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)， **SQLConnect** 不會使用連接字串。  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 當需要超過資料來源名稱、使用者識別碼和密碼的資訊時，就會使用 **SQLDriverConnect** 。 其中一個要 **SQLDriverConnect** 的參數是包含驅動程式特定資訊的連接字串。 您可以使用 **SQLDriverConnect** 而非 **SQLConnect** ，原因如下：  
  
-   在連接階段指定驅動程式專屬的資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   不使用 ODBC 資料來源連接。  
  
 **SQLDriverConnect** 連接字串包含一系列的關鍵字-值配對，可指定 ODBC 驅動程式支援的所有連接資訊。 除了供驅動程式支援之所有連接資訊使用的驅動程式專屬關鍵字之外，每個驅動程式還支援標準 ODBC 關鍵字 (DSN、FILEDSN、DRIVER、UID、PWD 和 SAVEFILE)。 **SQLDriverConnect** 可以用來連接，而不需要資料來源。 例如，設計用來對實例進行「無 DSN」連接的應用程式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用定義登入識別碼、密碼、網路程式庫、要連接的伺服器名稱，以及要使用之預設資料庫的連接字串來呼叫 **SQLDriverConnect** 。  
  
 使用 **SQLDriverConnect** 時，有兩個選項可提示使用者輸入任何所需的連接資訊：  
  
-   應用程式對話方塊  
  
     您可以建立應用程式對話方塊，以提示輸入連接資訊，然後呼叫 **SQLDriverConnect** 並將 Null 視窗控制碼和 *DriverCompletion* 設定為 SQL_DRIVER_NOPROMPT。 這些參數設定可防止 ODBC 驅動程式開啟自己的對話方塊。 當控制應用程式的使用者介面相當重要時，使用此方法。  
  
-   驅動程式對話方塊  
  
     您可以撰寫應用程式的程式碼，以將有效的視窗控制碼傳遞至 **SQLDriverConnect** ，並將 *DriverCompletion* 參數設定為 SQL_DRIVER_COMPLETE、SQL_DRIVER_PROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED。 接著，驅動程式會產生一個對話方塊來提示使用者輸入連接資訊。 這個方法會簡化應用程式的程式碼。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**（例如 **SQLDriverConnect**）會使用連接字串。 不過，藉由使用 **SQLBrowseConnect**，應用程式可以在執行時間與資料來源反復建立完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建立自己的對話方塊來提示輸入此資訊，藉此保持對其使用者介面的控制。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。  
  
     例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 當 **SQLBrowseConnect** 完成連接成功時，它會傳回一個連接字串，可用於後續的 **SQLDriverConnect** 呼叫。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式永遠會在成功 **SQLConnect**、 **SQLDriverConnect** 或 **SQLBrowseConnect** 上傳回 SQL_SUCCESS_WITH_INFO。 當 ODBC 應用程式在取得 SQL_SUCCESS_WITH_INFO 之後呼叫 **SQLGetDiagRec** 時，可能會收到下列訊息：  
  
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
  
 您可以忽略訊息 5701 和 5703；這些訊息僅供參考。 不過，您不得忽略 SQL_SUCCESS_WITH_INFO 傳回碼，因為可能會傳回 5701 或 5703 之外的訊息。 例如，如果驅動程式連接到執行實例的伺服器 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而該伺服器具有過期的目錄預存程式，則 SQL_SUCCESS_WITH_INFO 之後透過 **SQLGetDiagRec** 傳回的其中一個錯誤就是：  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 連接應用程式的錯誤處理函式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應該呼叫 **SQLGetDiagRec** ，直到它傳回 SQL_NO_DATA 為止。 然後，它應該會處理 *pfNative* 代碼為5701或5703的任何訊息。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server &#40;ODBC&#41;通訊 ](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
