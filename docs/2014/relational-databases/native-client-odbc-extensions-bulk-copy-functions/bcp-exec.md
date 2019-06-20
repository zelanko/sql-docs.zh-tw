---
title: bcp_exec | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_exec
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d5ce458ea8f5874620ea0561eeea5c6ff8e56bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689038"
---
# <a name="bcpexec"></a>bcp_exec
  在資料庫資料表和使用者檔案間執行資料的完整大量複製。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_exec (  
HDBC   
hdbc  
,  
LPDBINT   
pnRowsProcessed  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *pnRowsProcessed*  
 這是 DBINT 的指標。 **Bcp_exec**函式的成功複製的資料列數目填入此 DBINT。 如果*pnRowsProcessed*是 NULL，它會忽略**bcp_exec**。  
  
## <a name="returns"></a>傳回值  
 SUCCEED、SUCCEED_ASYNC 或 FAIL。 **Bcp_exec**函式會傳回 SUCCEED，如果複製所有資料列。 **bcp_exec**如果非同步大量複製作業仍然尚未處理，會傳回 SUCCEED_ASYNC。 **bcp_exec**發生完整失敗，則產生錯誤的資料列數目達到針對 bcpmaxerrs 所使用指定的值，傳回 FAIL [bcp_control](bcp-control.md)。 BCPMAXERRS 預設為 10。 BCPMAXERRS 選項僅會影響提供者在從資料檔讀取資料列 (而非傳送到伺服器的資料列) 時所偵測到的語法錯誤。 伺服器會在偵測到資料列的錯誤時中止批次。 請檢查*pnRowsProcessed*成功複製的資料列數目的參數。  
  
## <a name="remarks"></a>備註  
 此函式會將資料從使用者檔案至資料庫資料表，反之亦然，複製的值而定*eDirection*中的參數[bcp_init](bcp-init.md)。  
  
 然後再呼叫**bcp_exec**，呼叫**bcp_init**具有有效的使用者檔案名稱。 無法執行這項操作時，會發生錯誤。  
  
 **bcp_exec**是唯一大量複製函數很可能是任何長度的時間。 因此，它是唯一支援非同步模式的大量複製函數。 若要設定非同步模式，請使用[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，將 sql_attr_async_enable 設定為 sql_async_enable_on，然後，再呼叫**bcp_exec**。 若要測試是否完成，呼叫**bcp_exec**使用相同的參數。 大量複製尚未完成，如果**bcp_exec**會傳回 SUCCEED_ASYNC。 它也會傳回在*pnRowsProcessed*已傳送至伺服器的資料列數目的狀態計數。 到達批次的結尾之前，不會認可傳送至伺服器的資料列。  
  
 如需中斷變更中大量複製中的開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，請參閱 <<c2> [ 執行大量複製作業&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。</c2>  
  
## <a name="example"></a>範例  
 下列範例示範如何使用**bcp_exec**:  
  
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
if (bcp_init(hdbc, _T("pubs..authors"), _T("authors.sav"), NULL, DB_OUT)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Now, execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   if (nRowsProcessed == -1)  
      {  
      printf_s("No rows processed on bulk copy execution.\n");  
      }  
   else  
      {  
      printf_s("Incomplete bulk copy.   Only %ld row%s copied.\n",  
         nRowsProcessed, (nRowsProcessed == 1) ? "": "s");  
      }  
   return;  
   }  
  
printf_s("%ld rows processed.\n", nRowsProcessed);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
