---
title: bcp_init |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_init
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d482ac020aaaf5ac8f029306441c3e9979f4379
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131168"
---
# <a name="bcpinit"></a>bcp_init
  初始化大量複製作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_init (  
HDBC   
hdbc  
,  
LPCTSTR   
szTable  
,  
LPCTSTR   
szDataFile  
,  
LPCTSTR   
szErrorFile  
,  
INT   
eDirection  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *szTable*  
 這是要來回複製之資料庫資料表的名稱。 此名稱也可以包含資料庫名稱或擁有者名稱。 例如， **pubs.gracie.titles**， **pubs...標題**， **gracie.titles**，以及**標題**都是合法的資料表名稱。  
  
 如果*eDirection*為 DB_OUT， *szTable*也可以為資料庫檢視的名稱。  
  
 如果*eDirection*為 DB_OUT，而且使用指定的 SELECT 陳述式[bcp_control](bcp-control.md)之前[bcp_exec](bcp-exec.md)呼叫時， **bcp_init** _szTable_必須設為 NULL。  
  
 *szDataFile*  
 這是要來回複製之使用者檔案的名稱。 如果在複製資料時直接從變數使用[bcp_sendrow](bcp-sendrow.md)，將*szDataFile*為 NULL。  
  
 *szErrorFile*  
 這是錯誤檔案的名稱，該檔案會以進度訊息、錯誤訊息，以及因為任何原因而無法從使用者檔案複製到資料表之任何資料列的複本。 若 NULL 作為傳遞*szErrorFile*，會使用任何錯誤檔案。  
  
 *eDirection*  
 這是複製的方向，DB_IN 或 DB_OUT。 DB_IN 表示從程式變數或使用者檔案複製到資料表。 DB_OUT 表示從資料庫資料表複製到使用者檔案。 您必須利用 DB_OUT 指定使用者檔案名稱。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 呼叫**bcp_init**再呼叫其他任何大量複製函數。 **bcp_init**大量複製到工作站之間的資料執行必要的初始化和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **Bcp_init**函式必須提供具有啟用大量複製函數搭配 ODBC 連接控制代碼。 若要啟用控制代碼，請使用[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) sql_copt_ss_bcp 設定為 sql_bcp_on 設定上的已配置但未連接的連接控制代碼。 嘗試在已連接的控制代碼上指派屬性會導致錯誤。  
  
 指定資料檔案時， **bcp_init**會檢查資料庫來源或目標資料表，不是資料檔案的結構。 **bcp_init**指定基礎資料庫資料表、 檢視或 SELECT 結果集中每個資料行的資料檔案的資料格式值。 這個指定包括每個資料行的資料類型、資料中是否有長度或 null 指標和結束字元位元組字串，以及固定長度資料類型的寬度。 **bcp_init**設定這些值，如下所示：  
  
-   指定的資料類型為資料行在資料庫資料表、檢視或 SELECT 結果集中的資料類型。 資料類型會由 sqlncli.h 中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型列舉。 資料本身會以其電腦格式表示。 也就是從資料行的資料**整數**大四位元組順序表示的資料型別-或由小到大陊咈鼣砫建立資料檔案。  
  
-   如果資料庫資料類型的長度是固定的，資料檔案資料的長度也是固定的。 處理資料的大量複製函數 (例如[bcp_exec](bcp-exec.md)) 剖析中的資料庫資料表、 檢視或 SELECT 資料行清單中指定的資料長度相同的資料檔案中的資料長度的資料列。 例如，定義為資料庫資料行的資料**char(13**必須針對每個檔案中的資料列的 13 個字元表示。 如果資料庫資料行允許使用 Null 值，固定長度的資料前置詞可以是 Null 指標。  
  
-   定義結束字元位元組順序時，結束字元位元組順序的長度會設定為 0。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料檔案對於資料庫資料表中的每個資料行都必須有資料。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複製時，來自資料庫資料表、檢視或 SELECT 結果集中所有資料行的資料都會複製到資料檔案中。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料行在資料檔案中的序數位置必須與資料行在資料庫資料表中的序數位置相同。 從複製時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **bcp_exec**會根據資料庫資料表中的資料行的序數位置的資料。  
  
-   如果資料庫資料類型的長度是變數 (例如**varbinary(22)**) 或者如果資料庫資料行可以包含 null 值，資料檔案中的資料的前置詞為長度 /null 指標。 指標的寬度會根據資料類型和大量複製的版本而改變。  
  
 若要變更針對資料檔指定的資料格式值，請呼叫[bcp_columns](bcp-columns.md)並[bcp_colfmt](bcp-colfmt.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的大量複製可以針對不包含索引的資料表進行最佳化，方法是，將資料庫復原模式設定為 SIMPLE 或 BULK_LOGGED。 如需詳細資訊，請參閱 <<c0> [ 大量匯入採用最低限度記錄的必要條件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)並[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql)。  
  
 如果使用的資料檔案時，您必須呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)若要指定的格式和位置在記憶體中的資料為每個資料行，然後將複製的資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="example"></a>範例  
 此範例顯示如何利用格式檔案使用 ODBC bcp_init 函數。  
  
 編譯與執行 C++ 程式碼之前，您需要執行下列動作：  
  
-   建立成為 Test 的 ODBC 資料來源。 您可以讓此資料來源與任何資料庫產生關聯。  
  
-   在資料庫上執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]：  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   在您執行應用程式的目錄中，加入稱為 Bcpfmt.fmt 的檔案，並將其加入至檔案中：  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   在您執行應用程式的目錄中，加入稱為 Bcpodbc.bcp 的檔案，並將其加入至檔案中：  
  
    ```  
    1  
    2  
    ```  
  
 現在，您可以編譯及執行 C++ 程式碼。  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
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
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
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
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
