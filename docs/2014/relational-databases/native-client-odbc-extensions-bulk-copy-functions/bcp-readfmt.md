---
title: bcp_readfmt |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3d700f752a3194821065dc21ddd6ab96fa6a8f26
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136147"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
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
 之後`bcp_readfmt`讀取格式值，它會適當地呼叫[bcp_columns](bcp-columns.md)和[bcp_colfmt](bcp-colfmt.md)。 您不需要剖析格式檔案，也不需要進行這些呼叫。  
  
 若要保存格式檔案，呼叫[bcp_writefmt](bcp-writefmt.md)。 呼叫`bcp_readfmt`可以參考已儲存的格式。 如需詳細資訊，請參閱[bcp_init](bcp-init.md)。  
  
 或者，大量複製公用程式 (**bcp**) 可以將使用者定義資料格式儲存在檔案可以參考的`bcp_readfmt`。 如需有關**bcp**公用程式和結構**bcp**資料格式檔案，請參閱[大量匯入和匯出的資料&#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
 `BCPDELAYREADFMT`值*eOption*參數[bcp_control](bcp-control.md)修改 bcp_readfmt 的行為。  
  
> [!NOTE]  
>  格式檔案必須已經產生 4.2 版或更新版本的**bcp**公用程式。  
  
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
  
  