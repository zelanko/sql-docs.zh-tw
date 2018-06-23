---
title: 連接到資料來源 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1b4972792bf40c5569a3529c583209bfd4f53407
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031231"
---
# <a name="connecting-to-a-data-source-odbc"></a>連接至資料來源 (ODBC)
  配置環境與連接控制代碼，並設定任何連接屬性之後，應用程式會連接到資料來源或驅動程式。 您可以用來連接的函數有三種：  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 如需有關連接到資料來源，包括各種連接字串可用的選項，請參閱[Using Connection String Keywords with SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect**是最簡單的連線函式。 它接受三種參數：資料來源名稱、使用者識別碼與密碼。 使用**SQLConnect**當這三個參數會包含所有連接到資料庫所需的資訊。 若要這樣做，請建立使用資料來源的清單**SQLDataSources**; 提示使用者輸入資料來源、 使用者識別碼和密碼，然後再呼叫**SQLConnect**。  
  
 **SQLConnect**假設資料來源名稱、 使用者識別碼和密碼就足以連接至資料來源和 ODBC 資料來源包含 ODBC 驅動程式必須進行連接的其他資訊。 不同於[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md)和[SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md)， **SQLConnect**不會使用連接字串。  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect**需要比資料來源名稱、 使用者識別碼和密碼的詳細資訊時使用。 其中一個參數來**SQLDriverConnect**是包含驅動程式特定資訊的連接字串。 您可能會使用**SQLDriverConnect**而不是**SQLConnect** ，原因如下：  
  
-   在連接階段指定驅動程式專屬的資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   不使用 ODBC 資料來源連接。  
  
 **SQLDriverConnect**連接字串包含一連串的關鍵字-值配對所指定的 ODBC 驅動程式支援的所有連接資訊。 除了供驅動程式支援之所有連接資訊使用的驅動程式專屬關鍵字之外，每個驅動程式還支援標準 ODBC 關鍵字 (DSN、FILEDSN、DRIVER、UID、PWD 和 SAVEFILE)。 **SQLDriverConnect**可以用於不使用資料來源連接。 例如，應用程式是設計用來建立的執行個體的 「 無 dsn 」 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以呼叫**SQLDriverConnect**定義登入識別碼、 密碼、 網路程式庫、 伺服器名稱以連接字串連接到，並預設使用的資料庫。  
  
 當使用**SQLDriverConnect**，有兩個選項，提示使用者輸入任何需要的連接資訊：  
  
-   應用程式對話方塊  
  
     您可以建立一個應用程式的對話方塊，提示輸入連接資訊，然後再撥打**SQLDriverConnect**與 NULL 視窗控制代碼和*DriverCompletion*設定為 SQL_DRIVER_NOPROMPT。 這些參數設定可防止 ODBC 驅動程式開啟自己的對話方塊。 當控制應用程式的使用者介面相當重要時，使用此方法。  
  
-   驅動程式對話方塊  
  
     您可以撰寫程式碼應用程式傳遞有效的視窗控制代碼**SQLDriverConnect**並設定*DriverCompletion* SQL_DRIVER_COMPLETE、 SQL_DRIVER_PROMPT 或 SQL_DRIVER_COMPLETE_ 參數必要項。 接著，驅動程式會產生一個對話方塊來提示使用者輸入連接資訊。 這個方法會簡化應用程式的程式碼。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**、 like **SQLDriverConnect**，會使用連接字串。 不過，透過使用**SQLBrowseConnect**，應用程式可以在執行階段建構資料來源反覆完成連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建立自己的對話方塊來提示輸入此資訊，藉此保持對其使用者介面的控制。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。  
  
     例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 當**SQLBrowseConnect**完成成功連接之後，它會傳回連接字串可以用在後續呼叫**SQLDriverConnect**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式一律會傳回 SQL_SUCCESS_WITH_INFO 上成功**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**。 當 ODBC 應用程式呼叫**SQLGetDiagRec**取得 SQL_SUCCESS_WITH_INFO 之後, 可接收下列訊息：  
  
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
  
 您可以忽略訊息 5701 和 5703；這些訊息僅供參考。 不過，您不得忽略 SQL_SUCCESS_WITH_INFO 傳回碼，因為可能會傳回 5701 或 5703 之外的訊息。 例如，如果驅動程式會連接到執行的執行個體的伺服器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]過期的目錄預存程序傳回的其中一個錯誤透過**SQLGetDiagRec** SQL_SUCCESS_WITH_INFO 之後：  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 錯誤處理應用程式的函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接應該呼叫**SQLGetDiagRec**直到傳回 sql_no_data 為止。 它應該接著處理任何訊息之外*pfNative* 5701 或 5703 的程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server 通訊&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  