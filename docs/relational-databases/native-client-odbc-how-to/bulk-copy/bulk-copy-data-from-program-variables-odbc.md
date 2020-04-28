---
title: 從程式變數（ODBC）大量資料複製 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bulk copy [ODBC]
ms.assetid: 0c3f2d7c-4ff2-4887-adfd-1f488a27c21c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ebabedb2c801881a4dc908ead93515dc9119fc3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299603"
---
# <a name="bulk-copy-data-from-program-variables-odbc"></a>從程式變數中大量複製資料 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  這個範例會示範如何使用大量複製函數，從程式變數大量複製資料到使用**bcp_bind**和**bcp_sendrow**的 SQL Server。 (為了簡化這個範例會移除錯誤檢查程式碼)。  
  
 此範例是針對 ODBC 3.0 版或更新版本所開發。  
  
 **安全性注意事項**可能的話，請使用 Windows 驗證。 如果無法使用 Windows 驗證，請提示使用者在執行階段輸入認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，則應該用 [Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504) 加密這些認證。  
  
### <a name="to-use-bulk-copy-functions-directly-on-program-variables"></a>若要直接針對程式變數使用大量複製函數  
  
1.  配置環境控制代碼和連接控制代碼。  
  
2.  將 SQL_COPT_SS_BCP 和 SQL_BCP_ON 設定為啟用大量複製作業。  
  
3.  連接到 SQL Server。  
  
4.  呼叫[bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)以設定下列資訊：  
  
    -   要進行大量複製之來源或目標資料表或檢視表的名稱。  
  
    -   針對資料檔案的名稱指定 NULL。  
  
    -   要接收任何大量複製錯誤訊息的資料檔案名稱 (如果您不需要訊息檔案，請指定 NULL)。  
  
    -   複製的方向：DB_IN (從應用程式到檢視表或資料表) 或 DB_OUT (從資料表或檢視表到應用程式)。  
  
5.  針對大量複製中的每個資料行呼叫[bcp_bind](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) ，以將資料行系結至程式變數。  
  
6.  使用資料填入程式變數，並呼叫[bcp_sendrow](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)來傳送資料列。  
  
7.  傳送數個數據列之後，請呼叫[bcp_batch](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)來檢查已傳送的資料列。 最好至少為每1000個數據列呼叫[bcp_batch](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)一次。  
  
8.  傳送所有資料列之後，請呼叫[bcp_done](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)以完成作業。  

 您可以藉由呼叫[bcp_colptr](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)和[bcp_collen](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)，在大量複製作業期間改變程式變數的位置和長度。 使用[bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)來設定各種大量複製選項。 使用[bcp_moretext](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) ，將區段中的**text**、 **Ntext**和**image**資料傳送至伺服器。  
  
## <a name="example"></a>範例  
 IA64 不支援此範例。  
  
 您需要名為 AdventureWorks 的 ODBC 資料來源，其預設資料庫為 AdventureWorks 範例資料庫  （您可以從[Microsoft SQL Server 範例和 [社區專案](https://go.microsoft.com/fwlink/?LinkID=85384)] 首頁下載 AdventureWorks 範例資料庫）。此資料來源必須以作業系統所提供的 ODBC 驅動程式為基礎（驅動程式名稱為 "SQL Server"）。 如果您要建立並執行此範例，當做 64 位元作業系統上的 32 位元應用程式，您必須利用 %windir%\SysWOW64\odbcad32.exe，以 ODBC 管理員身分建立 ODBC 資料來源。  
  
 這個範例會連接到電腦的預設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。 若要連接到具名執行個體，請變更 ODBC 資料來源的定義，以便使用下列格式指定執行個體：server\namedinstance。 根據預設，[!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] 會安裝至具名執行個體。  
  
 執行第一個（ [!INCLUDE[tsql](../../../includes/tsql-md.md)]）程式代碼清單，以建立範例將使用的資料表。  
  
 使用 odbc32.lib 和 odbcbcp.lib 編譯第二個 (C++) 程式碼清單。 如果您使用 MSBuild.exe 建立，請將 Bcpfmt.fmt 和 Bcpodbc.bcp 從專案目錄複製到具有該 .exe 的目錄，然後叫用該 .exe。  
  
 執行第三個[!INCLUDE[tsql](../../../includes/tsql-md.md)]（）程式代碼清單，以刪除此範例所使用的資料表。  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPSource')  
     DROP TABLE BCPSource  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPTarget')  
     DROP TABLE BCPTarget  
GO  
  
CREATE TABLE BCPSource (cola int PRIMARY KEY, colb CHAR(10) NULL)  
INSERT INTO BCPSource (cola, colb) VALUES (1, 'aaa')  
INSERT INTO BCPSource (cola, colb) VALUES (2, 'bbb')  
CREATE TABLE BCPTarget (cola int PRIMARY KEY, colb CHAR(10) NULL)  
```  
  
```  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC, hdbc2 = SQL_NULL_HDBC;  
SQLHSTMT hstmt2 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt2 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt2);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (hdbc2 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc2);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc2);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // BCP variables.  
   char *terminator = "\0";  
  
   // bcp_done takes a different format return code because it returns number of rows bulk copied  
   // after the last bcp_batch call.  
   DBINT cRowsDone = 0;  
  
   // Set up separate return code for bcp_sendrow so it is not using the same retcode as SQLFetch.  
   RETCODE SendRet;  
  
   // Column variables.  cbCola and cbColb must be defined right before Cola and szColb because   
   // they are used as bulk copy indicator variables.  
   struct ColaData {  
      int cbCola;  
      SQLINTEGER Cola;  
   } ColaInst;  
  
   struct ColbData {  
      int cbColb;  
      SQLCHAR szColb[11];  
   } ColbInst;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set bulk copy mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // sample uses Integrated Security, create the SQL Server DSN using Windows NT authentication  
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "AdventureWorks..BCPTarget", NULL, NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the program variables for the bulk copy.  
   retcode = bcp_bind(hdbc1, (BYTE *)&ColaInst.cbCola, 4, SQL_VARLEN_DATA, NULL, (INT)NULL, SQLINT4, 1);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_bind(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Could normally use strlen to calculate the bcp_bind cbTerm parameter, but this terminator   
   // is a null byte (\0), which gives strlen a value of 0. Explicitly give cbTerm a value of 1.  
   retcode = bcp_bind(hdbc1, (BYTE *)&ColbInst.cbColb, 4, 11, (UCHAR*)terminator, 1, SQLCHARACTER, 2);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_bind(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate second ODBC connection handle so bulk copy and cursor operations do not conflict.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc2);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc2, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate ODBC statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt2);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hstmt2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
SQLLEN lDataLengthA;  
SQLLEN lDataLengthB;  
  
   // Bind the SELECT statement to the same program variables bound to the bulk copy operation.  
   retcode = SQLBindCol(hstmt2, 1, SQL_C_SLONG, &ColaInst.Cola, 0, &lDataLengthA);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLBindCol(hstmt2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLBindCol(hstmt2, 2, SQL_C_CHAR, &ColbInst.szColb, 11, &lDataLengthB);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLBindCol(hstmt2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute SELECT statement to build a cursor containing data to be bulk copied to new table.  
   retcode = SQLExecDirect(hstmt2, (UCHAR*)"SELECT * FROM BCPSource", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
   // Go into a loop fetching rows from the cursor until each row is fetched. Because the   
   // bcp_bind calls and SQLBindCol calls each reference the same variables, each fetch fills   
   // the variables used by bcp_sendrow, so all you have to do to send the data to SQL Server is   
   // to call bcp_sendrow.  
   while ( (retcode = SQLFetch(hstmt2) ) != SQL_NO_DATA) {  
      if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLFetch Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
  
      ColaInst.cbCola = (int)lDataLengthA;  
      ColbInst.cbColb = (int)lDataLengthB;  
  
     if ( (SendRet = bcp_sendrow(hdbc1) ) != SUCCEED ) {  
         printf("bcp_sendrow(hdbc1) Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Signal the end of the bulk copy operation.  
   cRowsDone = bcp_done(hdbc1);  
   if ( (cRowsDone == -1) ) {  
      printf("bcp_done(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied after last bcp_batch call = %d.\n", cRowsDone);  
  
   // Cleanup.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt2);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLDisconnect(hdbc2);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc2);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
```  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPSource')  
     DROP TABLE BCPSource  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPTarget')  
     DROP TABLE BCPTarget  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server ODBC 驅動程式的大量複製如何 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [從程式變數中大量複製](../../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
  
