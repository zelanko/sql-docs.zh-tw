---
title: 配置方向並連線到 SQL 伺服器 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d26af711c07c4ea296d5351d0fcb0d1f9710706
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294459"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>配置控制代碼並連接到 SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>配置控制代碼並連接到 SQL Server  
  
1.  加入 ODBC 標頭檔 Sql.h、Sqlext.h、Sqltypes.h。  
  
2.  加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驅動程式專屬的標頭檔 Odbcss.h。  
  
3.  使用**處理類型**呼叫[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) SQL_HANDLE_ENV 以初始化 ODBC 並分配環境句柄。  
  
4.  將[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)設置為SQL_ATTR_ODBC_VERSION,ValuePtr 設置為SQL_OV_ODBC3,以指示應用程式將使用 ODBC 3.x**Attribute****ValuePtr**格式函數調用。  
  
5.  或者,調用[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)來設置其他環境選項,或者調用[SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403)獲取環境選項。  
  
6.  使用**句柄類型**SQL_HANDLE_DBC調用[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396)以分配連接句柄。  
  
7.  或者,調用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)來設置連接選項,或者調用[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)獲取連接選項。  
  
8.  呼叫 SQLConnect 使用現有資料來源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線到 。  
  
     Or  
  
     呼叫[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)使用連接字串連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 。  
  
     完整的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接字串至少擁有下列其中一種形式：  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     如果連接字串不完整 **,SQLDriverConnect**可以提示輸入所需的資訊。 這由為*驅動程式完成*參數指定的值控制。  
  
     \- 或 -  
  
     以反覆運算方式多次呼叫[SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)以產生連接字串並連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 。  
  
9. 或者,調用[SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)獲取數據[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]源的驅動程式屬性和行為。  
  
10. 配置與使用陳述式。  
  
11. 呼叫 SQL 斷線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接以斷線連接,並使連接句柄可用於新連接。  
  
12. 使用**SQL_HANDLE_DBC的句柄類型**調用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)以釋放連接句柄。  
  
13. 使用**SQL_HANDLE_ENV的句柄類型**調用**SQLFreeHandle**以釋放環境句柄。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果必須保留認證,則應使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)對其進行加密。  
  
## <a name="example"></a>範例  
 此示例顯示對**SQLDriverConnect**的調用,以連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例 ,而無需現有的 ODBC 數據來源。 通過將不完整的連接字串傳遞到**SQLDriverConnect,** 它會導致 ODBC 驅動程式提示使用者輸入缺少的資訊。  
  
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
  
  
