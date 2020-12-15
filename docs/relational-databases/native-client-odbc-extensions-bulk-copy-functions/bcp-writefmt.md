---
description: bcp_writefmt
title: bcp_writefmt |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_writefmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_writefmt function
ms.assetid: cb4c1d37-667d-4bcd-b13c-eb638bcc9b69
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f1288057763d60154016524dcd62302498b8c71
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483279"
---
# <a name="bcp_writefmt"></a>bcp_writefmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  建立包含目前大量複製資料檔格式之描述的格式檔。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_writefmt (  
        HDBC hdbc,  
        LPCTSTR szFormatFile);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *szFormatFile*  
 這是用來接收資料檔格式值之使用者檔案的路徑和檔案名稱。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 格式檔案會指定大量複製所建立之資料檔的資料格式。 [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)和[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)的呼叫會定義資料檔案的格式。 **bcp_writefmt** 將此定義儲存在 *szformatfile 中* 所參考的檔案中。 如需詳細資訊，請參閱 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)。  
  
 如需 **bcp** 資料格式檔案結構的詳細資訊，請參閱 [使用 bcp 公用程式匯入和匯出大量資料 &#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)。  
  
 若要載入已儲存的格式檔案，請使用 [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)。  
  
> [!NOTE]  
>  只有使用7.0 版和更新版本散發的 **bcp** 公用程式版本才支援 **bcp_writefmt** 所產生的格式檔案 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="example"></a>範例  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_OUT) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_columns(hdbc, 3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
bcp_colfmt(hdbc, 1, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 1);  
bcp_colfmt(hdbc, 2, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 2);  
bcp_colfmt(hdbc, 3, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 3);  
  
if (bcp_writefmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   printf_s("%ld rows copied from SQL Server\n", nRowsProcessed);  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
