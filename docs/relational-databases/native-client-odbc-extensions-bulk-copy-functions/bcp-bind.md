---
title: bcp_bind |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ae1ad6aabc87d1cf0d7d92da5b97092c23bc02d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511928"
---
# <a name="bcpbind"></a>bcp_bind
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
 這是已複製之資料的指標。 如果*eDataType*為 SQLTEXT、 SQLNTEXT、 SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE， *pData*可以是 NULL。 NULL *pData*表示 long 資料值將會傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用的區塊[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。 使用者只需要將設定*pData*為 NULL，如果資料行對應到使用者繫結欄位的 BLOB 資料行否則**bcp_bind**將會失敗。  
  
 如果這些指標出現在資料中，它們會直接出現在資料前的記憶體中。 *PData*參數會指向指標變數，在此情況下和指標，寬度*cbIndicator*正確參數，用來處理使用者資料的大量複製。  
  
 *cbIndicator*  
 這是資料行的資料內，長度或 Null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2、4 或 8。 指標會直接出現在任何資料前的記憶體中。 例如，下列結構類型定義可用於使用大量複製，將整數值插入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表：  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 在範例案例中， *pData*參數會設定為結構的一部分，也就是 BCPBOUNDINT 的地址宣告執行個體的位址*iIndicator*結構成員。 *CbIndicator*參數會設定大小的整數 (sizeof，而*cbData*參數會重新設定大小的整數 (sizeof。 大量複製資料列包含 null 值的伺服器加入值的繫結的資料行的執行個體的值來*iIndicator*成員應該設定為 SQL_NULL_DATA。  
  
 *cbData*  
 這是資料在程式變數中的位元組計數，不包括任何長度或 Null 指標或結束字元的長度。  
  
 設定*cbData*為 SQL_NULL_DATA 表示複製到伺服器的所有資料列包含資料行的 NULL 值。  
  
 設定*cbData*為 SQL_VARLEN_DATA 表示系統會使用字串結束字元，或複製的其他方法，來判斷資料的長度。  
  
 對於整數之類的固定長度資料類型，此資料類型會指出系統之資料的長度。 因此，對於固定長度資料類型*cbData*可以安全地成為 SQL_VARLEN_DATA 或資料的長度。  
  
 針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元和二進位資料類型*cbData*可以是 SQL_VARLEN_DATA、 SQL_NULL_DATA、 某個正值或 0。 如果*cbData*為 SQL_VARLEN_DATA，系統會使用長度 /null 指標 （如果有的話） 或結束字元順序來決定資料的長度。 如果同時提供兩者，系統會使用導致複製最少量資料者。 如果*cbData*為 SQL_VARLEN_DATA，資料行的資料類型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元或二進位類型，而且沒有長度指標和結束字元順序指定，則系統會傳回錯誤訊息。  
  
 如果*cbData*為 0 或正值，則系統會使用*cbData*當做資料長度。 不過，如果除了正*cbData*值，提供長度指標或結束字元順序，系統會使用產生最少量複製資料的方法來決定資料長度。  
  
 *CbData*參數值表示資料的位元組計數。 如果字元資料以 Unicode 寬字元，則正*cbData*參數值表示乘以的大小，以位元組為單位的每個字元的字元數。  
  
 *pTerm*  
 這是位元組模式的指標 (如果有的話)，可標示此程式變數的結尾。 例如，ANSI 和 MBCS C 字串通常有 1 個位元組的結束字元 (\0)。  
  
 如果變數沒有結束字元，請設定*pTerm*為 NULL。  
  
 您可以使用任何空字串 ("") 來指定 C Null 結束字元，做為程式變數的結束字元。 因為 null 結束的空字串會構成單一位元組 （結束字元位元組本身），設定*cbTerm*為 1。 例如，若要表示中的字串*szName*是以 null 終止和結束字元，應該用來表示長度：  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 未結束此範例的形式可能表示 15 個字元會從複製*szName*變數繫結的資料表的第二個資料行：  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請確認結束字元位元組字串與位元組字串長度的設定正確。 例如，若要表示中的字串*szName*為 Unicode 寬字元字串，以 Unicode null 結束字元值結束：  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 如果繫結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行的寬字元，在執行任何轉換[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行為 MBCS 字元類型，當資料傳送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，會執行寬字元到多位元組字元的轉換。  
  
 *cbTerm*  
 這是出現在程式變數之結束字元中的位元組計數 (如果有的話)。 如果變數沒有結束字元，請設定*cbTerm*設為 0。  
  
 *eDataType*  
 這是程式變數的 C 資料類型。 程式變數中的資料會轉換為資料庫資料行的類型。 如果此參數為 0，則不會執行任何轉換。  
  
 *EDataType*參數會列舉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlncli.h 中的資料類型 token，不 ODBC C 資料類型列舉值列舉。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLINT2 來指定兩個位元組的整數 ODBC 類型 SQL_C_SHORT。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入 SQLXML 和 SQLUDT 資料類型語彙基元中的支援**_eDataType_** 參數。  
 
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
|SQLINT4|ssNoversion|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1：SQLINT1<br /> 2：SQLINT2<br /> 4：SQLINT4<br /> 8:SQLINT8|  
|SQLFLT4|FLOAT|  
|SQLFLT8|FLOAT|  
|SQLFLTN|*cbIndicator*<br /> 4：SQLFLT4<br /> 8:SQLFLT8|  
|SQLDECIMALN|SQL_NUMERIC_STRUCT|  
|SQLNUMERICN|SQL_NUMERIC_STRUCT|  
|SQLMONEY|DBMONEY|  
|SQLMONEY4|DBMONEY4|  
|SQLMONEYN|*cbIndicator*<br /> 4：SQLMONEY4<br /> 8:SQLMONEY|  
|SQLTIMEN|SQL_SS_TIME2_STRUCT|  
|SQLDATEN|SQL_DATE_STRUCT|  
|SQLDATETIM4|DBDATETIM4|  
|SQLDATETIME|DBDATETIME|  
|SQLDATETIMN|*cbIndicator*<br /> 4：SQLDATETIM4<br /> 8:SQLDATETIME|  
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|  
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|  
|SQLIMAGE|unsigned char *|  
|SQLUDT|unsigned char *|  
|SQLUNIQUEID|SQLGUID|  
|SQLVARIANT|*除了下列以外的任何資料類型：*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|  
|SQLXML|*支援的 C 資料類型：*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|  
  
 *idxServerCol*  
 這是資料庫資料表中要將資料複製到其中之資料行的序數位置。 資料表中的第一個資料行是資料行 1。 資料行的序數位置由報告[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 使用**bcp_bind**快速、 有效率的方法，來將資料從程式變數複製到資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 呼叫[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)之前呼叫這個或其他任何大量複製函數。 呼叫**bcp_init**設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]大量複製的目標資料表。 呼叫時**bcp_init**搭配**bcp_bind**並[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)，則**bcp_init** *szDataFile*參數，指出資料檔中，設定為 NULL，**bcp_init**_eDirection_參數設定為 DB_IN。  
  
 個別**bcp_bind**呼叫中的每個資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要複製的資料表。 必要後**bcp_bind**呼叫已被設，然後呼叫**bcp_sendrow**若要從程式變數来傳送的資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不支援重新繫結資料行。  
  
 每當您想要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要認可已經收到的資料列，請呼叫[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)。 例如，呼叫**bcp_batch**一次插入每 1000 個資料列或在其他任何間隔。  
  
 要插入其他資料列時，呼叫[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)。 無法執行這項操作時，會發生錯誤。  
  
 控制使用指定的參數設定[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)，不會影響**bcp_bind**傳輸的資料列。  
  
 如果*pData*的資料行設為 NULL，因為其值會提供呼叫[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)，與任何後續的資料行*eDataType*設定為 SQLTEXT、 SQLNTEXT，SQLXML、 SQLUDT、 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY、 SQLNCHAR 或 SQLIMAGE 必須也繫結與*pData*設定為 NULL，和其值也必須提供藉由呼叫**bcp_moretext**.  
  
 對於新的大數值類型，例如**varchar （max)**， **varbinary （max)**，或**nvarchar （max)**，您可以使用 SQLCHARACTER、 SQLVARCHAR、 SQLVARBINARY、 SQLBINARY 和中的類型指標為 SQLNCHAR *eDataType*參數。  
  
 如果*cbTerm*是不是 0，任何值 （1、 2、 4 或 8） 都是有效的前置詞 (*cbIndicator*)。 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端會搜尋結束字元、 計算結束字元的資料長度 (*我*)，並將*cbData*以較小的 i 值與值前置詞。  
  
 如果*cbTerm*為 0 並*cbIndicator* （前置詞） 不是 0， *cbIndicator*必須是 8。 8 位元組前置詞可以採用下列值：  
  
-   0xFFFFFFFFFFFFFFFF 表示欄位的 Null 值  
  
-   0xFFFFFFFFFFFFFFFE 會視為特殊的前置詞值，用於將區塊中的資料有效傳送到伺服器。 包含此特殊前置詞之資料的格式為：  
  
-   < SPECIAL_PREFIX > \<0 或更多的資料區塊 >< ZERO_CHUNK > 其中：  
  
-   SPECIAL_PREFIX 是 0xFFFFFFFFFFFFFFFE  
  
-   DATA_CHUNK 是包含區塊長度的 4 位元組前置詞，後面接著以 4 位元組前置詞指定其長度的實際資料。  
  
-   ZERO_CHUNK 是包含全部零 (00000000) 的 4 位元組值，表示資料的結尾。  
  
-   其他任何有效的 8 位元組長度會視為一般資料長度。  
  
 呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)使用時**bcp_bind**會導致錯誤。  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>bcp_bind 支援增強的日期和時間功能  
 如需搭配使用的型別*eDataType*參數的日期/時間類型，請參閱[增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
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
  
  
