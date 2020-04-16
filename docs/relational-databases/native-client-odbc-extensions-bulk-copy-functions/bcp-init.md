---
title: bcp_init |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_init
- bcp_initW
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b8e40091f88c4e9fc739f125a2e44715e62c9ee
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "73782684"
---
# <a name="bcp_init"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

初始化大量複製作業。  

## <a name="syntax"></a>語法  
  
```  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  

Unicode 與 ANSI 名稱:
- bcp_initA(安西)
- bcp_initW(Unicode)

## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *szTable*  
 這是要來回複製之資料庫資料表的名稱。 此名稱也可以包含資料庫名稱或擁有者名稱。 例如,**酒吧.gracie.titles,****酒吧。標題****、gracie.標題**和**標題**都是合法的表名。  
  
 如果*eDirection*是DB_OUT,*則 szTable*也可以是資料庫檢視的名稱。  
  
 如果*eDirection* DB_OUT,並且在呼叫[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)之前使用[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)指定 SELECT 語句,則必須**將 szTable bcp_init***szTable*設置為 NULL。  
  
 *szDataFile*  
 這是要來回複製之使用者檔案的名稱。 如果使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)直接從變數複製資料,則將*szDataFile*設定為 NULL。  
  
 *szErrorFile*  
 這是錯誤檔案的名稱，該檔案會以進度訊息、錯誤訊息，以及因為任何原因而無法從使用者檔案複製到資料表之任何資料列的複本。 如果 NULL 作為*szErrorFile*傳遞,則不使用錯誤檔。  
  
 *eDirection*  
 這是複製的方向，DB_IN 或 DB_OUT。 DB_IN 表示從程式變數或使用者檔案複製到資料表。 DB_OUT 表示從資料庫資料表複製到使用者檔案。 您必須利用 DB_OUT 指定使用者檔案名稱。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 在調用任何其他批量複製功能之前調用**bcp_init。** **bcp_init**為工作站[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和之間的數據批量複製執行必要的初始化。  
  
 **bcp_init**功能必須提供啟用的 ODBC 連接句柄,以便與批量複製功能一起使用。 要啟用該句柄,請使用[SQLSetConnectAttr,](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)將SQL_COPT_SS_BCP設置為在已分配但未連接的連接句柄上SQL_BCP_ON。 嘗試在已連接的控制代碼上指派屬性會導致錯誤。  
  
 指定資料檔時 **,bcp_init**檢查資料庫來源或目標表的結構,而不是資料檔。 **bcp_init**基於資料庫表、檢視或 SELECT 結果集中的每一列指定數據檔的資料格式值。 這個指定包括每個資料行的資料類型、資料中是否有長度或 null 指標和結束字元位元組字串，以及固定長度資料類型的寬度。 **bcp_init**設置這些值,如下所示:  
  
-   指定的資料類型為資料行在資料庫資料表、檢視或 SELECT 結果集中的資料類型。 資料類型會由 sqlncli.h 中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型列舉。 資料本身會以其電腦格式表示。 也就是說,來自**整數**數據類型列的數據由基於創建數據檔的計算機的大位元組或小位元組序列表示。  
  
-   如果資料庫資料類型的長度是固定的，資料檔案資料的長度也是固定的。 處理資料(例如[,bcp_exec)](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)的批量複製函數解析數據行,這些行期望數據檔中的數據長度與資料庫表、視圖或 SELECT 列清單中指定的數據的長度相同。 例如,定義為**char (13)** 的資料庫列的數據必須由檔中每行數據 13 個字元表示。 如果資料庫資料行允許使用 Null 值，固定長度的資料前置詞可以是 Null 指標。  
  
-   定義結束字元位元組順序時，結束字元位元組順序的長度會設定為 0。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料檔案對於資料庫資料表中的每個資料行都必須有資料。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複製時，來自資料庫資料表、檢視或 SELECT 結果集中所有資料行的資料都會複製到資料檔案中。  
  
-   複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，資料行在資料檔案中的序數位置必須與資料行在資料庫資料表中的序數位置相同。 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複製時**bcp_exec**根據列在資料庫表中的表的位距位置放置數據。  
  
-   如果資料庫資料類型的長度是可變的(例如 **,varbinary(22),** 或者如果資料庫列可以包含空值,則數據檔中的數據由長度/空指示器預固定。 指標的寬度會根據資料類型和大量複製的版本而改變。  
  
 要變更資料檔案指定的資料格式值,請呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)並[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的大量複製可以針對不包含索引的資料表進行最佳化，方法是，將資料庫復原模式設定為 SIMPLE 或 BULK_LOGGED。 有關詳細資訊,請參閱批量匯入和[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)[中最小紀錄紀錄的先決條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
 如果未使用資料檔案,則必須呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)以指定每欄資料記憶體的格式和位置,然後將資料列複製[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。  
  
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
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
