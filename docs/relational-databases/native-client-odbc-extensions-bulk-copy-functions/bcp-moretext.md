---
title: bcp_moretext |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
ms.openlocfilehash: e225a6d8f3dcc73102778f93775e5d2057c046d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431267"
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
 是從所參考的資料複製到 SQL Server 資料的位元組數字*pData*。 SQL_NULL_DATA 的值表示 NULL。  
  
 *pData*  
 這是要傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之支援的長型、變動長度資料區塊的指標。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 此函式可以用於搭配[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)並[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) long、 可變長度的資料將值複製到 SQL Server，在幾個較小的區塊。 **bcp_moretext**可以搭配具有下列的 SQL Server 資料類型的資料行：**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，使用者定義型別 (UDT) 和 XML。 **bcp_moretext**不支援資料轉換，提供的資料必須符合目標資料行的資料類型。  
  
 如果**bcp_bind**呼叫具有非 NULL *pData*所支援的資料型別參數**bcp_moretext**， **bcp_sendrow**傳送整個資料值，而不論長度為何。 如果，不過， **bcp_bind**有 NULL *pData*支援的資料類型的參數**bcp_moretext**可立即在成功傳回時從之後複製資料**bcp_sendrow**指出已經處理的資料存在任何繫結資料行。  
  
 如果您使用**bcp_moretext**傳送一個支援的資料類型資料行的資料列中，您也必須使用它來傳送資料列中的所有其他支援的資料類型資料行。 不能略過任何資料行。 支援的資料類型為 SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT 和 SQLXML。 如果此資料行分別為 varchar(max)、nvarchar(max) 或 varbinary(max)，則 SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY 和 SQLVARBINARY 也會列入這個類別目錄。  
  
 呼叫**bcp_bind**或是[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)設定所有的資料部分複製到 SQL Server 資料行的總長度。 嘗試傳送更多的位元組，比對的呼叫中所指定的 SQL Server **bcp_bind**或是**bcp_collen**會產生錯誤。 此錯誤，就會發生，例如使用應用程式中**bcp_collen**來設定適用於 SQL Server 的可用資料的長度**文字**資料行，為 4500，然後呼叫**bcp_moretext**五次，並同時指出每次呼叫資料緩衝區長度是 1000 個位元組。  
  
 如果複製的資料列都包含一個以上的長型、 變動長度資料行， **bcp_moretext**序數編號最低其資料的資料行，後面跟著 [下一步] 的第一個傳送最低序數編號的資料行，依此類推。 更正預期資料的總長度設定是很重要的一件事。 除了使用長度設定以外，沒有任何方法可以指示大量複製已經收到資料行的所有資料。  
  
 當**var(max)** 值傳送到伺服器，使用 bcp_sendrow 和 bcp_moretext，不需要呼叫 bcp_collen 來設定資料行長度。 相反地，僅限這些類型的值便會終止呼叫 bcp_sendrow 長度為零。  
  
 應用程式通常會呼叫**bcp_sendrow**並**bcp_moretext**內迴圈，用來傳送資料的資料列數目。 以下是如何執行此動作包含兩個資料表概述**文字**資料行：  
  
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
 此範例示範如何使用**bcp_moretext**具有**bcp_bind**並**bcp_sendrow**:  
  
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
  
  
