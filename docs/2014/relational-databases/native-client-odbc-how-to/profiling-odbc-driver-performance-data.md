---
title: 分析驅動程式效能資料（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7de38f3c91814dbd364caee84b34dacdfbdf475
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63200309"
---
# <a name="profile-driver-performance-data-odbc"></a>分析驅動程式效能資料 (ODBC)
  此範例顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式專用選項，以記錄效能統計資料。 此範例會建立一個檔案：odbcperf.log。此範例會示範如何建立效能資料記錄檔，以及直接從 SQLPERF 資料結構顯示效能資料 (SQLPERF 結構定義於 Odbcss.h 中)。 此範例是針對 ODBC 3.0 版或更新版本所開發。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，您應該使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)將它們加密。  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>使用 ODBC 管理員記錄驅動程式效能資料  
  
1.  在 [**控制台**] 中，按兩下 [系統**管理工具**]，然後按兩下 **[資料來源（ODBC）**]。 或者，您可以叫用 odbcad32.exe。  
  
2.  按一下 [**使用者 DSN**]、[**系統 DSN**] 或 [檔案**DSN** ] 索引標籤。  
  
3.  按一下記錄效能的資料來源。  
  
4.  按一下 [設定]****。  
  
5.  在 Microsoft SQL Server 設定 DSN Wizard] 中，流覽至包含**記錄檔 ODBC 驅動程式統計資料的頁面至記錄**檔。  
  
6.  選取 **[記錄 ODBC 驅動程式統計資料至記錄檔]**。 在方塊中，放置應該記錄其統計資料之檔案的名稱。 或者，按一下 **[流覽**] 來流覽檔案系統中的統計資料記錄檔。  
  
### <a name="to-log-driver-performance-data-programmatically"></a>以程式設計方式記錄驅動程式效能資料  
  
1.  使用 SQL_COPT_SS_PERF_DATA_LOG 和效能資料記錄檔的完整路徑和檔案名來呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 。 例如：  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  使用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_START 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，以開始記錄效能資料。  
  
3.  （選擇性）使用 SQL_COPT_SS_LOG_NOW 和 Null 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，將效能資料的 tab 鍵分隔記錄寫入效能資料記錄檔。 這可以在應用程式執行時完成多次。  
  
4.  使用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_STOP 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，以停止記錄效能資料。  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>將驅動程式效能資料提取到應用程式中  
  
1.  使用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_START 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，以開始分析效能資料。  
  
2.  使用 SQL_COPT_SS_PERF_DATA 和 SQLPERF 結構之指標的位址來呼叫[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) 。 第一個這類呼叫會將指標設定為有效 SQLPERF 結構的位址，其中包含目前的效能資料。 驅動程式不會在效能結構中持續重新整理資料。 應用程式必須在需要使用更多目前的效能資料重新整理結構時，重複呼叫[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) 。  
  
3.  使用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_STOP 呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，以停止記錄效能資料。  
  
## <a name="example"></a>範例  
 您需要名為 AdventureWorks 的 ODBC 資料來源，其預設資料庫為 AdventureWorks 範例資料庫  （您可以從[Microsoft SQL Server 範例和 [社區專案](https://go.microsoft.com/fwlink/?LinkID=85384)] 首頁下載 AdventureWorks 範例資料庫）。此資料來源必須以作業系統所提供的 ODBC 驅動程式為基礎（驅動程式名稱為 "SQL Server"）。 如果您要建立並執行此範例，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。  
  
 這個範例會連接到電腦的預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 若要連接到具名執行個體，請變更 ODBC 資料來源的定義，以便使用下列格式指定執行個體：server\namedinstance。 根據預設，[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 會安裝至具名執行個體。  
  
 使用 odbc32.lib 編譯。  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [分析 ODBC 驅動程式效能的使用說明主題 &#40;ODBC&#41;](profiling-odbc-driver-performance-odbc.md)   
 [分析 ODBC 驅動程式效能](../native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
