---
title: bcp_exec |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- bcp_exec
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ca5a14408a64c595ddbb32b8d57a636c2d8255e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946453"
---
# <a name="bcpexec"></a>bcp_exec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在資料庫資料表和使用者檔案間執行資料的完整大量複製。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_exec (  
        HDBC hdbc,  
        LPDBINT pnRowsProcessed);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *pnRowsProcessed*  
 這是 DBINT 的指標。 **Bcp_exec**函式成功複製的資料列數目填入此 DBINT。 如果*pnRowsProcessed*是 NULL，它會忽略**bcp_exec**。  
  
## <a name="returns"></a>傳回值  
 SUCCEED、SUCCEED_ASYNC 或 FAIL。 **Bcp_exec**函式會傳回 SUCCEED，如果所有資料列被複製。 **bcp_exec**傳回 SUCCEED_ASYNC 如果非同步大量複製作業仍然尚未處理。 **bcp_exec**傳回 FAIL，如果發生完整失敗，或如果產生錯誤的資料列數目達到針對 BCPMAXERRS 使用指定的值[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)。 BCPMAXERRS 預設為 10。 BCPMAXERRS 選項僅會影響提供者在從資料檔讀取資料列 (而非傳送到伺服器的資料列) 時所偵測到的語法錯誤。 伺服器會在偵測到資料列的錯誤時中止批次。 請檢查*pnRowsProcessed*成功複製的資料列數目的參數。  
  
## <a name="remarks"></a>備註  
 此函式會將資料從使用者檔案至資料庫資料表，或反之亦然，複製的值而定*eDirection*中的參數[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)。  
  
 然後再呼叫**bcp_exec**，呼叫**bcp_init**具有有效的使用者檔案名稱。 無法執行這項操作時，會發生錯誤。  
  
 **bcp_exec**是唯一大量複製函數很可能是任何長度的時間。 因此，它是唯一支援非同步模式的大量複製函數。 若要設定非同步模式，請使用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設 SQL_ATTR_ASYNC_ENABLE 請先呼叫**bcp_exec**。 若要測試是否完成，呼叫**bcp_exec**具有相同參數。 如果大量複製尚未完成， **bcp_exec**傳回 SUCCEED_ASYNC。 它也會傳回在*pnRowsProcessed*已傳送至伺服器的資料列數目的狀態計數。 到達批次的結尾之前，不會認可傳送至伺服器的資料列。  
  
 衄壽重大變更中大量複製中開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，請參閱[執行大量複製作業&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
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
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
