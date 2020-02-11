---
title: 配置控制碼並連接到 SQL Server （ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 322120624c612371b56029c2cf29c9ab457c81b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63225497"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>配置控制代碼並連接到 SQL Server (ODBC)
    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>配置控制代碼並連接到 SQL Server  
  
1.  加入 ODBC 標頭檔 Sql.h、Sqlext.h、Sqltypes.h。  
  
2.  加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驅動程式專屬的標頭檔 Odbcss.h。  
  
3.  使用[](https://go.microsoft.com/fwlink/?LinkId=58396) SQL_HANDLE_ENV `HandleType`的呼叫 SQLALLOCHANDLE，以初始化 ODBC 並配置環境控制碼。  
  
4.  呼叫[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)並`Attribute`將設定為 SQL_ATTR_ODBC_VERSION `ValuePtr` ，並將設定為 SQL_OV_ODBC3，以指示應用程式將使用 ODBC 3.x 格式函式呼叫。  
  
5.  （選擇性）呼叫[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)以設定其他環境選項，或呼叫[SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403)來取得環境選項。  
  
6.  使用[](https://go.microsoft.com/fwlink/?LinkId=58396) SQL_HANDLE_DBC `HandleType`的呼叫 SQLAllocHandle，以配置連接控制碼。  
  
7.  （選擇性）呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)來設定連接選項，或呼叫[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md)來取得連接選項。  
  
8.  呼叫 SQLConnect，以使用現有的資料來源連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     Or  
  
     呼叫[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) ，以使用連接字串連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     完整的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接字串至少擁有下列其中一種形式：  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     如果連接字串不完整，`SQLDriverConnect` 可以提示所需的資訊。 這是由指定給*DriverCompletion*參數的值所控制。  
  
     \- 或 -  
  
     以反復方式多次呼叫[SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md) ，以建立連接字串並連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
9. （選擇性）呼叫[SQLGetInfo](../native-client-odbc-api/sqlgetinfo.md)以取得資料來源的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驅動程式屬性和行為。  
  
10. 配置與使用陳述式。  
  
11. 呼叫 SQLDisconnect 以中斷與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連線，並讓連接控制碼可用於新的連接。  
  
12. 使用[](../native-client-odbc-api/sqlfreehandle.md) SQL_HANDLE_DBC `HandleType`的呼叫 SQLFreeHandle 來釋放連接控制碼。  
  
13. 利用 SQL_HANDLE_ENV 的 `SQLFreeHandle` 呼叫 `HandleType` 來釋放環境控制代碼。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，您應該使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)將它們加密。  
  
## <a name="example"></a>範例  
 此範例顯示呼叫 `SQLDriverConnect` 來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，而不需要現有的 ODBC 資料來源。 將不完整的連接字串傳遞到 `SQLDriverConnect` 時，會使 ODBC 驅動程式提示使用者輸入遺漏的資訊。  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
