---
title: bcp_bind | Microsoft Docs
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.reviewer: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 99da52886b15cf89b693fdfb5f1cc5d039e64905
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707729"
---
# <a name="bcp_bind"></a>bcp_bind

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  將程式變數中的資料繫結至資料表資料行，以便在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中進行大量複製。  

## <a name="syntax"></a>語法

```  
  
RETCODE bcp_bind (  
        HDBC hdbc,
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>引數

 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *pData*  
 這是已複製之資料的指標。 如果*eDataType*為 SQLTEXT、SQLNTEXT、SQLXML、SQLUDT、SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY、SQLNCHAR 或 SQLIMAGE，則*PDATA*可以是 Null。 Null *pData*表示 long 資料值將使用[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)以區區塊轉送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 只有當對應到使用者系結欄位的資料行是 BLOB 資料行時，使用者才應該將*pData*設定為 Null，否則**bcp_bind**將會失敗。  
  
 如果這些指標出現在資料中，它們會直接出現在資料前的記憶體中。 在此情況下， *pData*參數會指向指標變數，而大量複製會使用指標的寬度（ *cbIndicator*參數）來正確處理使用者資料。  
  
 *cbIndicator*  
 這是資料行的資料內，長度或 Null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2、4 或 8。 指標會直接出現在任何資料前的記憶體中。 例如，下列結構類型定義可用於使用大量複製，將整數值插入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表：  
  
```
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 在範例案例中， *pData*參數會設定為結構的已宣告實例位址，也就是 BCPBOUNDINT *iIndicator*結構成員的位址。 *CbIndicator*參數會設定為整數（sizeof （int））的大小，而*cbData*參數則會再次設定為整數（sizeof （int））的大小。 若要將資料列大量複製到包含系結資料行之 Null 值的伺服器，實例的*iIndicator*成員值應該設定為 SQL_Null_DATA。  
  
 *cbData*  
 這是資料在程式變數中的位元組計數，不包括任何長度或 Null 指標或結束字元的長度。  
  
 將*cbData*設定為 SQL_Null_DATA，表示複製到伺服器的所有資料列都包含資料行的 Null 值。  
  
 將*cbData*設定為 SQL_VARLEN_DATA 表示系統會使用字串結束字元或其他方法來判斷複製的資料長度。  
  
 對於整數之類的固定長度資料類型，此資料類型會指出系統之資料的長度。 因此，如果是固定長度的資料類型， *cbData*可以安全地 SQL_VARLEN_DATA 或資料的長度。  
  
 對於 @no__t 0 字元和二進位資料類型而言， *cbData*可以是 SQL_VARLEN_DATA、SQL_Null_DATA、某個正值或0。 如果*cbData*為 SQL_VARLEN_DATA，則系統會使用長度/null 指標（如果有的話）或結束字元序列來決定資料的長度。 如果同時提供兩者，系統會使用導致複製最少量資料者。 如果*cbData*是 SQL_VARLEN_DATA，資料行的資料類型是 @no__t 1 個字元或二進位類型，而且長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。  
  
 如果*cbData*為0或正值，則系統會使用*cbData*做為資料長度。 不過，如果除了正的*cbData*值之外，也提供長度指標或結束字元序列，系統會使用導致複製最少量資料的方法來決定資料長度。  
  
 *CbData*參數值表示資料的位元組計數。 如果字元資料是以 Unicode 寬字元表示，則正*cbData*參數值代表字元數乘以每個字元的大小（以位元組為單位）。  
  
 *pTerm*  
 這是位元組模式的指標 (如果有的話)，可標示此程式變數的結尾。 例如，ANSI 和 MBCS C 字串通常有 1 個位元組的結束字元 (\0)。  
  
 如果變數沒有結束字元，請將*pTerm*設定為 Null。  
  
 您可以使用任何空字串 ("") 來指定 C Null 結束字元，做為程式變數的結束字元。 因為以 null 結束的空字串構成單一位元組（結束字元位元組本身），所以請將*cbTerm*設定為1。 例如，表示*szName*中的字串是以 null 終止，而且應該使用結束字元來表示長度：  
  
```
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```

 這個範例的 nonterminated 表單可能表示從*szName*變數複製15個字元到系結資料表的第二個數據行：  

```
bcp_bind(hdbc, szName, 0, 15,
   NULL, 0, SQLCHARACTER, 2)  
```

 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請確認結束字元位元組字串與位元組字串長度的設定正確。 例如，若要指出*szName*中的字串是 unicode 寬字元字串，請以 unicode null 結束字元值結束：  
  
```  
bcp_bind(hdbc, szName, 0,
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 如果系結的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行是寬字元，則不會在[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)上執行任何轉換。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行為 MBCS 字元類型，當資料傳送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，會執行寬字元到多位元組字元的轉換。  
  
 *cbTerm*  
 這是出現在程式變數之結束字元中的位元組計數 (如果有的話)。 如果變數沒有結束字元，請將*cbTerm*設定為0。  

*eDataType*這是程式變數的 C 資料類型。 程式變數中的資料會轉換為資料庫資料行的類型。 如果此參數為 0，則不會執行任何轉換。  

*EDataType*參數是由 sqlncli 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型 token 所列舉，而不是 ODBC C 資料類型枚舉器。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLINT2 來指定兩個位元組的整數 ODBC 類型 SQL_C_SHORT。  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 在 **_eDataType_** 參數中引進了 SQLXML 和 SQLUDT 資料類型標記的支援。  

下表列出有效的列舉資料類型和對應的 ODBC C 資料類型。

|eDataType|C 類型|
|-----------------------|------------|  
|SQLTEXT|char *|  
|SQLNTEXT|wchar_t *|  
|SQLCHARACTER|char *|  
|SQLBIGCHAR|char *|  
|SQLVARCHAR|char *|  
|SQLBIGVARCHAR|char *|  
|SQLNCHAR|wchar_t *|  
|SQLNVARCHAR|wchar_t *|  
|SQLBINARY|unsigned char *|  
|SQLBIGBINARY|unsigned char *|  
|SQLVARBINARY|unsigned char *|  
|SQLBIGVARBINARY|unsigned char *|  
|SQLBIT|char|  
|SQLBITN|char|  
|SQLINT1|char|  
|SQLINT2|short int|  
|SQLINT4|int|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1：SQLINT1<br /> 2：SQLINT2<br /> 4：SQLINT4<br /> 8SQLINT8|  
|SQLFLT4|float|  
|SQLFLT8|float|  
|SQLFLTN|*cbIndicator*<br /> 4：SQLFLT4<br /> 8SQLFLT8|  
|SQLDECIMALN|SQL_NUMERIC_STRUCT|  
|SQLNUMERICN|SQL_NUMERIC_STRUCT|  
|SQLMONEY|DBMONEY|  
|SQLMONEY4|DBMONEY4|  
|SQLMONEYN|*cbIndicator*<br /> 4：SQLMONEY4<br /> 8SQLMONEY|  
|SQLTIMEN|SQL_SS_TIME2_STRUCT|  
|SQLDATEN|SQL_DATE_STRUCT|  
|SQLDATETIM4|DBDATETIM4|  
|SQLDATETIME|DBDATETIME|  
|SQLDATETIMN|*cbIndicator*<br /> 4：SQLDATETIM4<br /> 8SQLDATETIME|  
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|  
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|  
|SQLIMAGE|unsigned char *|  
|SQLUDT|unsigned char *|  
|SQLUNIQUEID|SQLGUID|  
|SQLVARIANT|*除了下列以外的任何資料類型：*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|  
|SQLXML|*支援的 C 資料類型：*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|  

*並將 idxservercol*這是要將資料複製到其中的資料庫資料表中，資料行的序數位置。 資料表中的第一個資料行是資料行 1。 資料行的序數位置是由[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)所報告。  
  
## <a name="returns"></a>傳回值

 SUCCEED 或 FAIL。

## <a name="remarks"></a>備註

使用**bcp_bind**以快速且有效率的方式，將程式變數中的資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料表。  

請先呼叫[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) ，再呼叫此或任何其他大量複製函數。 呼叫**bcp_init**會設定用於大量複製的 @no__t 1 目標資料表。 呼叫**bcp_init**以搭配**bcp_bind**和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)使用時，表示資料檔案的**bcp_init** _szDataFile_參數會設定為 Null;**bcp_init**_eDirection_參數設定為 DB_IN。  

針對您要複製的 @no__t 1 資料表中的每個資料行，進行個別的**bcp_bind**呼叫。 進行必要的**bcp_bind**呼叫之後，請呼叫**bcp_sendrow** ，將資料列從您的程式變數傳送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不支援重新繫結資料行。

每當您想要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認可已收到的資料列時，請呼叫[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)。 例如，針對每個插入的1000資料列或在任何其他間隔呼叫**bcp_batch**一次。  

當沒有要插入的資料列時，請呼叫[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)。 無法執行這項操作時，會發生錯誤。

以[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)指定的控制項參數設定不會影響**bcp_bind**資料列傳輸。  

如果資料行的*pData*是設為 Null，因為呼叫[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)會提供它的值，任何後續資料行的*EDATATYPE*設定為 SQLTEXT、SQLNTEXT、SQLXML、SQLUDT、SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY、SQLNCHAR 或 SQLIMAGE 也必須與設定為 Null 的*pData*系結，而且其值也必須透過呼叫來提供給**bcp_moretext**。  

對於新的大數數值型別（例如**Varchar （max）** 、 **Varbinary （max）** 或**Nvarchar （max））** ，您可以使用 SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY 和 SQLNCHAR 作為*eDataType*參數中的類型指標。  

如果*cbTerm*不是0，任何值（1、2、4或8）對前置詞（*cbIndicator*）都是有效的。 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 將會搜尋結束字元、計算結束字元（*i*）的資料長度，並將*cbData*設定為較小的 i 值和前置詞的值。  

如果*cbTerm*為0，而*cbIndicator* （前置詞）不是0，則*cbIndicator*必須是8。 8位元組前置詞可以採用下列值：  

- 0xFFFFFFFFFFFFFFFF 表示欄位的 Null 值  

- 0xFFFFFFFFFFFFFFFE 會被視為特殊的前置詞值，可用來有效率地將區塊中的資料傳送至伺服器。 包含此特殊前置詞之資料的格式為：  

- < SPECIAL_PREFIX > \<0 或更多資料區塊 > < ZERO_CHUNK > 位置：  

- SPECIAL_PREFIX 是 0xFFFFFFFFFFFFFFFE  

- DATA_CHUNK 是包含區塊長度的4位元組前置詞，後面接著以4位元組前置詞指定其長度的實際資料。  

- ZERO_CHUNK 是4個位元組的值，其中包含表示資料結尾的所有零（00000000）。  

- 任何其他有效的8位元組長度都會被視為一般資料長度。  

 使用**bcp_bind**時呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)會導致錯誤。  
  
## <a name="bcp_bind-support-for-enhanced-date-and-time-features"></a>bcp_bind 支援增強的日期和時間功能

如需有關搭配日期/時間類型的*eDataType*參數使用之類型的詳細資訊，請參閱[OLE DB 和&#40;ODBC&#41;的增強型日期和時間類型的大量複製變更](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  

如需詳細資訊，請參閱[日期和&#40;時間&#41;改善 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  

## <a name="example"></a>範例
  
```
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>另請參閱

 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)