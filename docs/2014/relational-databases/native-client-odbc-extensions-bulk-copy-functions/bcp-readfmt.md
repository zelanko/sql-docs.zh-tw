---
title: bcp_readfmt |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76ccc4271877b81ae103a89b5df727b74017d9ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62688664"
---
# <a name="bcp_readfmt"></a>bcp_readfmt
  從指定的格式檔案讀取資料檔格式定義。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *szFormatFile*  
 這是包含資料檔格式值之檔案的路徑和檔案名稱。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 在`bcp_readfmt`讀取格式值之後，它會對[bcp_columns](bcp-columns.md)和[bcp_colfmt](bcp-colfmt.md)進行適當的呼叫。 您不需要剖析格式檔案，也不需要進行這些呼叫。  
  
 若要保存格式檔案，請呼叫[bcp_writefmt](bcp-writefmt.md)。 對的`bcp_readfmt`呼叫可以參考儲存的格式。 如需詳細資訊，請參閱[bcp_init](bcp-init.md)。  
  
 或者，大量複製公用程式（**bcp**）可以將使用者定義的資料格式儲存在可供`bcp_readfmt`參考的檔案中。 如需**bcp**公用程式和**bcp**資料格式檔案結構的詳細資訊，請參閱[大量匯入和匯出資料 &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
 Bcp_control `BCPDELAYREADFMT`的*eOption*參數值會修改[bcp_control](bcp-control.md) bcp_readfmt 的行為。  
  
> [!NOTE]  
>  格式檔案必須已由**bcp**公用程式的4.2 或更新版本所產生。  
  
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
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
