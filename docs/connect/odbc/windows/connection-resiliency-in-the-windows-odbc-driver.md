---
title: Windows ODBC 驅動程式中的連線恢復功能 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 147716f986fb89d756c1800ac6fd71e138fae6a1
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600858"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Windows ODBC 驅動程式中的連接恢復功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  若要確保應用程式仍然連線到 [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)]，Windows 上的 ODBC 驅動程式可以還原閒置的連線。  
  
> [!IMPORTANT]  
>  Microsoft Azure SQL Database 和 SQL Server 2014 (和更新版本) 伺服器版本都支援連接恢復功能。  
  
 如需閒置連線恢復功能的詳細資訊，請參閱[技術文章 – 閒置連線恢復功能](https://go.microsoft.com/fwlink/?LinkId=393996)。  
  
 為了控制重新連接的行為，Windows 上的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 有兩個選項：  
  
-   連接重試計數。  
  
     連接重試計數可控制連接失敗時的重新連接嘗試次數。 有效值的範圍介於 0 到 255 之間。 零 (0) 表示不嘗試重新連接。 預設值是嘗試重新連接一次。  
  
     您可以在執行下列作業時修改連接重試次數：  
  
    -   透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接重試計數 **控制項定義或修改使用 ODBC Driver for** 的資料來源。  
  
    -   使用 **ConnectRetryCount** 連接字串關鍵字。  
  
     若要擷取連線重試的嘗試次數，請使用 **SQL_COPT_SS_CONNECT_RETRY_COUNT** (唯讀) 連線屬性。 如果應用程式連線到不支援連線恢復功能的伺服器，**SQL_COPT_SS_CONNECT_RETRY_COUNT** 會傳回 0。  
  
-   連接重試間隔。  
  
     連接重試間隔會指定每個連接重試嘗試的間隔秒數。 有效值為 1-60。 重新連接的時間總計不可超過連接逾時 (SQLSetStmtAttr 中的 SQL_ATTR_QUERY_TIMEOUT)。 預設值為 10 秒。  
  
     您可以在執行下列作業時修改連接重試間隔：  
  
    -   透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接重試間隔 **控制項定義或修改使用 ODBC Driver for** 的資料來源。  
  
    -   使用 **ConnectRetryInterval** 連接字串關鍵字。  
  
     若要擷取連線重試間隔的長度，請使用 **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (唯讀) 連線屬性。  
  
 如果應用程式透過 SQL_DRIVER_COMPLETE_REQUIRED 建立連接，且後續嘗試透過中斷的連接執行陳述式，ODBC 驅動程式將不會再次顯示對話方塊。 此外，在復原進行期間，  
  
-   在復原期間，任何對 **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** 的呼叫，都必須傳回 **SQL_CD_FALSE**。  
  
-   如果復原失敗，任何對 **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** 的呼叫，都必須傳回 **SQL_CD_TRUE**。  
  
 以下是在伺服器上執行命令的任何函數皆可能傳回的狀態碼：  
  
|State|訊息|  
|-----------|-------------|  
|IMC01|連接中斷，且無法復原。 用戶端驅動程式已嘗試復原連接一或多次，但所有嘗試皆失敗。 請提高 ConnectRetryCount 的值，以增加復原嘗試次數。|  
|IMC02|伺服器未認可復原嘗試，無法進行連接復原。|  
|IMC03|伺服器未保存在復原嘗試期間要求的確切用戶端 TDS 版本，無法進行連接復原。|  
|IMC04|伺服器未保存在復原嘗試期間要求的確切伺服器主要版本，無法進行連接復原。|  
|IMC05|連接中斷，且無法復原。 伺服器將連接標示為無法復原。 未嘗試還原連接。|  
|IMC06|連接中斷，且無法復原。 用戶端驅動程式將連接標示為無法復原。 未嘗試還原連接。|  
  
## <a name="example"></a>範例  
 下列範例包含兩個函數。 **func1** 說明如何連接使用 Windows 版 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的資料來源名稱 (DSN)。 DSN 會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證，而且它會指定使用者識別碼。 **func1**接著會擷取與連接重試次數**SQL_COPT_SS_CONNECT_RETRY_COUNT**。  
  
 **func2** 會使用 **SQLDriverConnect**、 **ConnectRetryCount** 連接字串關鍵字和連接屬性來擷取連接重試與重試間隔的設定。  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
