---
title: SQLGetStmtAttr 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a45674ecbb65fcedd64551af3b7a2440b2b4621
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetStmtAttr**傳回陳述式屬性的目前設定。  
  
> [!NOTE]  
>  如需有關哪些驅動程式管理員將此函式可對應時 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式，請參閱[對應取代函式的應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *屬性*  
 [輸入]要擷取的屬性。  
  
 *ValuePtr*  
 [輸出]這是要傳回的值中指定的屬性中的緩衝區指標*屬性*。  
  
 如果*ValuePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*ValuePtr*。  
  
 *BufferLength*  
 [輸入]如果*屬性*是 ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*屬性*是 ODBC 定義的屬性和\* *ValuePtr*是整數， *Columnsize*會被忽略。 如果中傳回的值 *\*ValuePtr*是 Unicode 字串 (當呼叫**SQLGetStmtAttrW**)、 *Columnsize*引數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*Columnsize*引數。 *Columnsize*可以是下列值：  
  
-   如果 *\*ValuePtr*是字元字串的指標，則*Columnsize*是 SQL_NTS 之字串的長度。  
  
-   如果 *\*ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR 結果 (*長度*) 中的巨集*Columnsize*。 這樣做會放在負值*Columnsize*。  
  
-   如果 *\*ValuePtr*是字元字串或二進位字串以外的值的指標，則*Columnsize*應該有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定長度資料類型，則*Columnsize*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不包括 null 結束字元） 的緩衝區的指標可用來傳回中 *\*ValuePtr*。 如果*ValuePtr*為 null 指標，則會傳回任何長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於或等於*Columnsize*中的資料 *\*ValuePtr*會被截斷成*Columnsize* null 結束字元的長度減而且是以 null 結束的驅動程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetStmtAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*HandleType*的 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetStmtAttr** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|中傳回的資料 *\*ValuePtr*已截斷為*Columnsize*減去 null 結束字元的長度。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|24000|指標狀態無效|引數*屬性*SQL_ATTR_ROW_NUMBER 和資料指標未開啟，或指標置於結果集或結果集的結尾之後開始之前。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**引數中*MessageText*描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLGetStmtAttr**呼叫函式。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|*(DM) \*ValuePtr*是字元字串，但 Columnsize 小於零，但不是等於 SQL_NTS。|  
|HY092|屬性/選項識別碼無效|指定的引數的值*屬性*對 ODBC 驅動程式支援的版本無效。|  
|HY109|無效的資料指標位置|*屬性*引數以前是 SQL_ATTR_ROW_NUMBER 和已刪除或無法讀取的資料列。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*的 ODBC 版本支援的驅動程式，但不支援此驅動程式是有效的 ODBC 陳述式屬性。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 一般陳述式屬性的詳細資訊，請參閱[陳述式屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 呼叫**SQLGetStmtAttr**中傳回 *\*ValuePtr*陳述式中指定的屬性值*屬性*。 該值可以是 SQLULEN 值或 null 結尾字元字串。 如果值是 SQLULEN 值時，有些驅動程式可能只會寫入較低的 32 位元或 16 位元的緩衝區並保留不變的更高序位位元。 因此，應用程式應該使用 SQLULEN 的緩衝區，並初始化為 0 的值之前呼叫這個函式。 此外， *Columnsize*和*StringLengthPtr*不使用引數。 應用程式如果值是以 null 結束的字串，指定在該字串的最大長度*Columnsize*引數，以及驅動程式會傳回在該字串的長度 *\*StringLengthPtr*緩衝區。  
  
 若要允許應用程式呼叫**SQLGetStmtAttr**才能使用 ODBC 2。*x*驅動程式、 呼叫**SQLGetStmtAttr**會對應到在驅動程式管理員**SQLGetStmtOption**。  
  
 下列陳述式屬性是唯讀，因此可以藉由擷取**SQLGetStmtAttr**，但未設定**SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 如需可設定及擷取屬性的清單，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
