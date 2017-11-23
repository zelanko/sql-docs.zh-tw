---
title: "SQLGetEnvAttr 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetEnvAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetEnvAttr
helpviewer_keywords: SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b7db465aa78dcbcdeb2443d6cb0c859923e4ccb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函式
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**傳回目前的環境屬性設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 [輸入]環境控制代碼。  
  
 *Attribute*  
 [輸入]要擷取的屬性。  
  
 *ValuePtr*  
 [輸出]傳回所指定之屬性的目前值的緩衝區指標*屬性*。  
  
 如果*ValuePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*ValuePtr*。  
  
 *Columnsize*  
 [輸入]如果*ValuePtr*指向字元字串，這個引數應該是長度\* *ValuePtr*。 如果\* *ValuePtr*是整數， *Columnsize*會被忽略。 如果 *\*ValuePtr*是 Unicode 字串 (當呼叫**SQLGetEnvAttrW**)、 *Columnsize*引數必須是偶數。 如果屬性值不是字元字串， *Columnsize*未使用。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不包括 null 結束字元） 的緩衝區的指標可用來傳回中 *\*ValuePtr*。 如果*ValuePtr*為 null 指標，則會傳回任何長度。 如果屬性值是字元字串，可用來傳回的位元組數目大於或等於*Columnsize*中的資料\* *ValuePtr*會被截斷成*Columnsize* null 結束字元的長度減而且是以 null 結束的驅動程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetEnvAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_ENV 和*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetEnvAttr** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|中傳回的資料\* *ValuePtr*已截斷為*Columnsize*減去 null 結束字元。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) **SQL_ATTR_ODBC_VERSION**尚未設定透過**SQLSetEnvAttr**。 您不需要設定**SQL_ATTR_ODBC_VERSION**明確如果您使用**SQLAllocHandleStd**。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY092|屬性/選項識別碼無效|指定的引數的值*屬性*對 ODBC 驅動程式支援的版本無效。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*驅動程式支援 ODBC 的版本，但不支援此驅動程式是有效的 ODBC 環境屬性。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*EnvironmentHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如需屬性的清單，請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 沒有驅動程式專屬環境屬性。 如果*屬性*指定屬性會傳回字串， *ValuePtr*必須是要傳回的字串緩衝區的指標。 將會包含 null 結束位元組的字串的最大長度*Columnsize*位元組。  
  
 **SQLGetEnvAttr**可以在任何時間之間配置和釋放環境控制代碼的呼叫。 已成功設定應用程式環境的所有環境屬性會一直都保存到**SQLFreeHandle**上呼叫*EnvironmentHandle*與*HandleType*利用 SQL_HANDLE_ENV。 可以同時配置一個以上的環境控制代碼，在 ODBC 3*.x*。 已配置另一個環境時，不會影響在一個環境的環境屬性。  
  
> [!NOTE]  
>  符合標準的應用程式支援 SQL_ATTR_OUTPUT_NTS 環境屬性。 當**SQLGetEnvAttr**呼叫時，ODBC 3*.x*驅動程式管理員一律會傳回 SQL_TRUE 這個屬性。 SQL_ATTR_OUTPUT_NTS 可以設定為 SQL_TRUE，只能由呼叫**SQLSetEnvAttr**。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
