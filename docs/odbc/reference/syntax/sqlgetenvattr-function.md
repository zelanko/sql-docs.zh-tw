---
title: SQLGetEnvAttr 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70fe1ca95f5160f801eaf3528e625116705eda6d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203807"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**傳回環境屬性的目前設定。  
  
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
 [輸出]在其中傳回所指定之屬性的目前值之緩衝區的指標*屬性*。  
  
 如果*ValuePtr*為 NULL，就*StringLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回中指向緩衝區*ValuePtr*。  
  
 *BufferLength*  
 [輸入]如果*ValuePtr*指向的字元字串，這個引數應該是長度\* *ValuePtr*。 如果\* *ValuePtr*是一個整數， *Columnsize*會被忽略。 如果 *\*ValuePtr*是 Unicode 字串 (呼叫時**SQLGetEnvAttrW**)，則*Columnsize*引數必須是偶數。 如果屬性值不是字元字串， *Columnsize*未使用。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不包括 null 結束字元） 緩衝區的指標來傳回在可用 *\*ValuePtr*。 如果*ValuePtr*為 null 指標，會傳回任何長度。 如果屬性值是字元字串，可用來傳回的位元組數目大於或等於*Columnsize*中的資料\* *ValuePtr*會被截斷成*BufferLength*減去 null 結束字元的長度，是以 null 終止的驅動程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetEnvAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_ENV 並*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetEnvAttr** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|中傳回的資料\* *ValuePtr*被截斷成會*Columnsize*減去之 null 結束字元。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) **SQL_ATTR_ODBC_VERSION**尚未設定透過**SQLSetEnvAttr**。 您不需要設定**SQL_ATTR_ODBC_VERSION**如果您使用，明確**SQLAllocHandleStd**。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY092|屬性/選項識別碼無效|指定的引數的值*屬性*ODBC 驅動程式支援的版本無效。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*的驅動程式支援的 ODBC 版本，但不是支援此驅動程式是有效的 ODBC 環境屬性。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*EnvironmentHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如需屬性的清單，請參閱 < [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 沒有驅動程式特有的環境屬性。 如果*屬性*指定的屬性會傳回字串， *ValuePtr*必須在其中傳回的字串緩衝區的指標。 將會包含 null 結束位元組的字串的最大長度*Columnsize*位元組。  
  
 **SQLGetEnvAttr**可在配置和釋放環境控制代碼之間的任何時間加以呼叫。 已成功設定環境的應用程式的所有環境屬性一直都保存到**SQLFreeHandle**上呼叫*EnvironmentHandle*使用*HandleType*SQL_HANDLE_ENV。 可以同時配置一個以上的環境控制代碼，在 ODBC 3 *.x*。 已配置另一個環境時，不會影響一個環境的環境屬性。  
  
> [!NOTE]
>  符合標準的應用程式支援 SQL_ATTR_OUTPUT_NTS 環境屬性。 當**SQLGetEnvAttr**呼叫時，ODBC 3 *.x*驅動程式管理員一定會傳回 SQL_TRUE 這個屬性。 SQL_ATTR_OUTPUT_NTS 可以只藉由呼叫設定為 SQL_TRUE **SQLSetEnvAttr**。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
