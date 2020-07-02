---
title: bcp_control |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_control
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_control function
ms.assetid: 32187282-1385-4c52-9134-09f061eb44f5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a58b41665d1b10a1e9f9868796b98b80e43e92d6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774303"
---
# <a name="bcp_control"></a>bcp_control
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  針對檔案和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的大量複製，變更各種控制項參數的預設設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_control (  
        HDBC hdbc,  
        INT eOption,  
        void* iValue);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *eOption*  
 為下列其中一項：  
  
 BCPABORT  
 停止已經進行的大量複製作業。 從另一個執行緒呼叫具有 BCPABORT *eOption*的**bcp_control** ，以停止執行大量複製作業。 *IValue*參數會被忽略。  
  
 BCPBATCH  
 這是每一批次中的資料列數目。 預設值為 0，這表示在擷取資料時，會指出資料表中的所有資料列，或在資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，會指出使用者資料檔中的所有資料列。 小於 1 的值會重設 BCPBATCH 為預設值。  
  
 BCPDELAYREADFMT  
 布林值，如果設定為 true，將會導致[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)在執行時讀取。 如果為 false （預設值），bcp_readfmt 會立即讀取格式檔案。 如果 BCPDELAYREADFMT 為 true，而且您呼叫 bcp_columns 或 bcp_setcolfmt，就會發生順序錯誤。  
  
 `bcp_control(hdbc,` `, (void *)FALSE)` 呼叫 `bcp_control(hdbc,` BCPDELAYREADFMT `, (void *)TRUE)` 和 bcp_writefmt 之後，如果您呼叫 BCPDELAYREADFMT，也會發生順序錯誤。  
  
 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 BCPFILECP  
 *iValue*包含資料檔案的字碼頁數目。 您可以指定字碼頁的數目，例如 1252 或 850，或以下任一個值：  
  
 BCPFILE_ACP：檔案中的資料位於用戶端的 Microsoft Windows® 字碼頁。  
  
 BCPFILE_OEMCP：檔案中的資料位於用戶端的 OEM 字碼頁 (預設值)。  
  
 BCPFILE_RAW：檔案中的資料位於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的字碼頁。  
  
 BCPFILEFMT  
 資料檔案格式的版本號碼。 這可以是80（ [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ）、90（ [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ）、100（ [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ）、110（ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ）或120（ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ）。 120 是預設值。 這個值在使用舊版伺服器支援的格式匯出和匯入資料時非常實用。 例如，若要將從伺服器文字資料行取得的資料匯入 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 至或更新版本之伺服器中的**Varchar （max）** 資料行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，您應該指定80。 同樣地，如果您在從**Varchar （max）** 資料行匯出資料時指定80，則它的儲存方式就像是以格式儲存文字資料行， [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 而且可以匯入到伺服器的文字資料行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。  
  
 BCPFIRST  
 這是要複製的檔案或資料表的第一個資料列。 預設值為 1，小於 1 的值會將這個選項重設為預設。  
  
 BCPFIRSTEX  
 如果是 BCP Out 作業，則指定將資料庫資料表第一個資料列複製到資料檔案中。  
  
 如果是 BCP In 作業，則指定將資料檔案的第一個資料列複製到資料庫資料表中。  
  
 *IValue*參數應該是包含值的帶正負號64位整數的位址。 可傳遞至 BCPFIRSTEX 的最大值為 2^63-1。  
  
 BCPFMTXML  
 指定所產生的格式檔案應該是 XML 格式。 預設為關閉。  
  
 XML 格式檔案提供更高的彈性，但是需要加入一些條件約束。 例如，您不可以同時指定欄位的前置詞和結束字元，即使在舊版的格式檔案中可以這麼做。  
  
> [!NOTE]  
>  XML 格式檔案只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 一起安裝時才受到支援。  
  
 BCPHINTS  
 *iValue*包含 SQLTCHAR 字元字串指標。 定址的字串會指定處理提示的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量複製或傳回結果集的 Transact-SQL 陳述式。 如果 Transact-SQL 陳述式指定為傳回一個以上的結果集，則第一個結果集之後的所有結果集都會被忽略。 如需大量複製處理提示的詳細資訊，請參閱[Bcp Utility](../../tools/bcp-utility.md)。  
  
 BCPKEEPIDENTITY  
 當*iValue*為 TRUE 時，指定大量複製函數會插入為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 identity 條件約束所定義之資料行提供的資料值。 輸入檔案必須提供識別資料行的值。 如果沒有設定，就會為插入的資料列產生新的識別值。 檔案中屬於識別欄位的所有資料都會被忽略。  
  
 BCPKEEPNULLS  
 指定檔案中的空資料值在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中是否會轉換為 NULL 值。 當*iValue*為 TRUE 時，空值會在資料表中轉換成 Null [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 預設是將空的值轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中資料行的預設值 (如果有預設值的話)。  
  
 BCPLAST  
 這是要複製的最後一個資料列。 預設是複製所有的資料列；小於 1 的值會將這個選項重設為預設值。  
  
 BCPLASTEX  
 如果是 BCP Out 作業，則指定將資料庫資料表最後一個資料列複製到資料檔案中。  
  
 如果是 BCP In 作業，則指定將資料檔案的最後一個資料列複製到資料庫資料表中。  
  
 *IValue*參數應該是包含值的帶正負號64位整數的位址。 可傳遞至 BCPLASTEX 的最大值是 2^63-1。  
  
 BCPMAXERRS  
 這是在大量複製作業失敗之前所允許的錯誤數目。 預設值為 10;小於1的值會將這個選項重設為預設值。 大量複製會限制 65,535 個錯誤的上限。 如果嘗試將這個選項設為大於 65,535 的值，則該選項會設定為 65,535。  
  
 BCPODBC  
 當為 TRUE 時，指定以字元格式儲存的**datetime**和**Smalldatetime**值將會使用 ODBC 時間戳記 escape 序列前置詞和後置詞。 BCPODBC.BCP 選項僅適用于 DB_OUT。  
  
 若為 FALSE，則會將代表1997年1月1日的**datetime**值轉換成字元字串： 1997-01-01 00：00：00.000。 當為 TRUE 時，相同的**datetime**值會表示為： {ts ' 1997-01-01 00：00： 00.000 '}。  
  
 BCPROWCOUNT  
 傳回受到目前 (或最近) BCP 作業影響的資料列數目。  
  
 BCPTEXTFILE  
 當設定為 TRUE 時，這個選項會指定資料檔為文字檔，而不是二進位檔。 如果檔案為文字檔，則 BCP 會藉由在資料檔的頭 2 個位元組中檢查 Unicode 位元組標記，判斷文字檔是否為 Unicode。  
  
 BCPUNICODEFILE  
 當設定為 TRUE 時，這個選項會指定輸入檔為 Unicode 檔案格式。  
  
 *iValue*  
 這是指定之*eOption*的值。 *iValue*是整數（LONGLONG）值，轉換成 void 指標，以允許未來擴充至64位值。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 此函數會設定各種大量複製作業的控制參數，包含取消大量複製之前所允許的錯誤次數、從資料檔複製的第一個和最後一個資料列的數目，以及批次大小。  
  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量複製 SELECT 的結果集時，這個函數也可用來指定 SELECT 陳述式。 將*eOption*設定為 BCPHINTS，並將*iValue*設定為具有包含 SELECT 語句之 SQLTCHAR 字串的指標。  
  
 只有在使用者檔案和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表之間進行複製時，這些控制項參數才有意義。 控制項參數設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)複製到的資料列不會有任何影響。  
  
## <a name="example"></a>範例  
  
```  
// Variables like henv not specified.  
SQLHDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("address"), _T("address.add"), _T("addr.err"),  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the number of rows per batch.   
if (bcp_control(hdbc, BCPBATCH, (void*) 1000) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set file column count.   
if (bcp_columns(hdbc, 1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the file format.   
if (bcp_colfmt(hdbc, 1, 0, 0, SQL_VARLEN_DATA, '\n', 1, 1)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
printf_s("%ld rows processed by bulk copy.", nRowsProcessed);  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
