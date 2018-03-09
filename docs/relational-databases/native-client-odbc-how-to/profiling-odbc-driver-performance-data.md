---
title: "分析驅動程式效能資料 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c4f977e3e70579d0555715bc174a5600e42a9a9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="profiling-odbc-driver-performance-data"></a>分析 ODBC 驅動程式效能資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  此範例顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式專用選項，以記錄效能統計資料。 此範例會建立一個檔案： Odbcperf.log 範例會示範如何建立效能資料記錄檔及直接從 SQLPERF 資料結構 （SQLPERF 結構定義於 Odbcss.h） 顯示效能資料。 此範例是針對 ODBC 3.0 版或更新版本所開發。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，則應該用 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532) 加密這些認證。  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>使用 ODBC 管理員記錄驅動程式效能資料  
  
1.  在**控制台**，連按兩下**系統管理工具**，然後按兩下 **資料來源 (ODBC)**。 或者，您可以叫用 odbcad32.exe。  
  
2.  按一下**使用者 DSN**，**系統 DSN**，或**檔案 DSN**  索引標籤。  
  
3.  按一下記錄效能的資料來源。  
  
4.  按一下  **設定**。  
  
5.  在 Microsoft SQL Server 設定 DSN 精靈，瀏覽至包含頁面**記錄 ODBC 驅動程式統計資料記錄檔**。  
  
6.  選取**記錄 ODBC 驅動程式統計資料記錄檔**。 在方塊中，放置應該記錄其統計資料之檔案的名稱。 （選擇性） 按一下**瀏覽**瀏覽檔案系統的統計資料記錄。  
  
### <a name="to-log-driver-performance-data-programmatically"></a>以程式設計方式記錄驅動程式效能資料  
  
1.  呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA_LOG 以及效能資料記錄檔的完整路徑和檔案名稱。 例如：  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_START 開始記錄效能資料。  
  
3.  （選擇性） 呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_LOG_NOW 和 NULL 效能資料的 tab 鍵分隔記錄寫入效能資料記錄檔。 這可以在應用程式執行時完成多次。  
  
4.  呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_STOP 停止記錄效能資料。  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>將驅動程式效能資料提取到應用程式中  
  
1.  呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_START 開始分析效能資料。  
  
2.  呼叫[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA 和 SQLPERF 結構的指標的位址。 第一個這類呼叫會將指標設定為有效 SQLPERF 結構的位址，其中包含目前的效能資料。 驅動程式不會在效能結構中持續重新整理資料。 應用程式必須重複呼叫[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)隨時需要重新整理與較新的效能資料結構。  
  
3.  呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)利用 SQL_COPT_SS_PERF_DATA 和 SQL_PERF_STOP 停止記錄效能資料。  
  
## <a name="example"></a>範例  
 您需要名為 AdventureWorks 的 ODBC 資料來源，其預設資料庫為 AdventureWorks 範例資料庫  (您可以從 [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) (Microsoft SQL Server 範例和社群專案) 首頁下載 AdventureWorks 範例資料庫)。此資料來源必須以作業系統提供的 ODBC 驅動程式為基礎 (驅動程式名稱為 "SQL Server")。 如果您要建立並執行此範例，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。  
  
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
 [分析 ODBC 驅動程式效能的如何主題 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)   
 [分析 ODBC 驅動程式效能](../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
