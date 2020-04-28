---
title: bcp_moretext |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_moretext
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05d7a6ca9f90439f803032087f4032765cba2f88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73782619"
---
# <a name="bcp_moretext"></a>bcp_moretext
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
 這是要從*pData*所參考的資料中，複製到 SQL Server 的資料位元組數目。 SQL_NULL_DATA 的值表示 NULL。  
  
 *pData*  
 這是要傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之支援的長型、變動長度資料區塊的指標。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 此函式可與[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)搭配使用，以將長的可變長度資料值複製到數個較社區塊中的 SQL Server。 **bcp_moretext**可以與具有下列 SQL Server 資料類型的資料行搭配使用： **text**、 **Ntext**、 **image**、 **Varchar （max）**、 **Nvarchar （max）**、 **VARBINARY （max）**、使用者定義型別（UDT）和 XML。 **bcp_moretext**不支援資料轉換，所提供的資料必須符合目標資料行的資料類型。  
  
 如果針對**bcp_moretext**所支援的資料類型，以非 Null 的*pData*參數來呼叫**bcp_bind** ， **bcp_sendrow**會傳送整個資料值，而不論長度為何。 不過，如果**bcp_bind**針對支援的資料類型具有 Null *pData*參數， **bcp_moretext**可以在成功從**bcp_sendrow**傳回後立即複製資料，表示已處理任何具有資料的綁定欄。  
  
 如果您使用**bcp_moretext**在資料列中傳送一個支援的資料類型資料行，您也必須使用它來傳送資料列中所有其他支援的資料類型資料行。 不能略過任何資料行。 支援的資料類型為 SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT 和 SQLXML。 如果此資料行分別為 varchar(max)、nvarchar(max) 或 varbinary(max)，則 SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY 和 SQLVARBINARY 也會列入這個類別目錄。  
  
 呼叫**bcp_bind**或[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)會設定要複製到 SQL Server 資料行之所有資料部分的總長度。 嘗試傳送 SQL Server 超過**bcp_bind**或**bcp_collen**的呼叫中所指定的位元組數，會產生錯誤。 例如，如果應用程式使用**bcp_collen**將 SQL Server**文字**資料行的可用資料長度設定為4500，則會呼叫**bcp_moretext**五次，並在每次呼叫時指出資料緩衝區長度為1000個位元組。  
  
 如果複製的資料列包含一個以上的長時間可變長度資料行， **bcp_moretext**首先會將其資料傳送到最低的序數編號資料行，後面接著下一個最低的序數編號資料行，依此類推。 更正預期資料的總長度設定是很重要的一件事。 除了使用長度設定以外，沒有任何方法可以指示大量複製已經收到資料行的所有資料。  
  
 當使用 bcp_sendrow 和 bcp_moretext 將**var （max）** 值傳送至伺服器時，不需要呼叫 bcp_collen 來設定資料行長度。 相反地，針對這些類型，值會藉由呼叫長度為零的 bcp_sendrow 來終止。  
  
 應用程式通常會呼叫**bcp_sendrow** ，並在迴圈內**bcp_moretext**來傳送多個資料列。 以下概述如何針對包含兩個**文字**資料行的資料表執行這項操作：  
  
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
 這個範例示範如何使用**bcp_moretext**搭配**bcp_bind**和**bcp_sendrow**：  
  
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
  
  
