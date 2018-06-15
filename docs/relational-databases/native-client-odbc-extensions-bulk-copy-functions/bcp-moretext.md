---
title: bcp_moretext |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_moretext
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e64f445788e35563120c357b93395fcfede50410
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946293"
---
# <a name="bcpmoretext"></a>bcp_moretext
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  將長的變動長度資料類型值的一部分傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_moretext (  
        HDBC hdbc,  
        DBINT cbData,  
        LPCBYTE pData);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *cbData*  
 是從參考的資料複製到 SQL Server 資料的位元組數目*pData*。 SQL_NULL_DATA 的值表示 NULL。  
  
 *pData*  
 這是要傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之支援的長型、變動長度資料區塊的指標。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 此函式可以用於搭配[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) long、 可變長度的資料將值複製到 SQL Server 中的較小的區塊數。 **bcp_moretext**可以搭配具有下列的 SQL Server 資料類型的資料行：**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，使用者定義型別 (UDT) 和 XML。 **bcp_moretext**不支援資料轉換，請提供的資料必須符合目標資料行的資料類型。  
  
 如果**bcp_bind**呼叫具有非 NULL *pData*所支援的資料型別參數**bcp_moretext**， **bcp_sendrow**傳送整個資料值，而不論長度為何。 如果，不過， **bcp_bind**有 NULL *pData*支援的資料類型的參數**bcp_moretext**可用來從成功傳回之後，立即複製資料**bcp_sendrow**指出已經處理任何具有資料繫結的資料行。  
  
 如果您使用**bcp_moretext**傳送一個支援的資料類型資料行的資料列中，您必須也將它傳送的資料列中的所有其他支援的資料類型資料行。 不能略過任何資料行。 支援的資料類型為 SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT 和 SQLXML。 如果此資料行分別為 varchar(max)、nvarchar(max) 或 varbinary(max)，則 SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY 和 SQLVARBINARY 也會列入這個類別目錄。  
  
 呼叫**bcp_bind**或[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)設定所有的資料部分複製到 SQL Server 資料行的總長度。 嘗試傳送更多的位元組比對的呼叫中所指定的 SQL Server **bcp_bind**或**bcp_collen**會產生錯誤。 這個錯誤，就會發生，例如在應用程式使用**bcp_collen**可用資料的長度設定為 SQL Server**文字**資料行，為 4500，然後呼叫**bcp_moretext**五次時指出每次呼叫資料緩衝區長度 1000 個位元組。  
  
 如果複製的資料列都包含一個以上的長型、 變動長度資料行， **bcp_moretext**第一個傳送資料到最低序數編號的資料行，接著是最低序數編號的資料行，以此類推。 更正預期資料的總長度設定是很重要的一件事。 除了使用長度設定以外，沒有任何方法可以指示大量複製已經收到資料行的所有資料。  
  
 當**var(max)** 值都會傳送到使用 bcp_sendrow 和 bcp_moretext 伺服器，則不需要呼叫 bcp_collen 設定資料行的長度。 相反地，僅限這些類型的值便會終止呼叫 bcp_sendrow 長度為零。  
  
 應用程式通常會呼叫**bcp_sendrow**和**bcp_moretext**內傳送的資料列數目的迴圈。 以下是如何執行此動作包含兩個資料表的外框**文字**資料行：  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>範例  
 這個範例示範如何使用**bcp_moretext**與**bcp_bind**和**bcp_sendrow**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
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
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
