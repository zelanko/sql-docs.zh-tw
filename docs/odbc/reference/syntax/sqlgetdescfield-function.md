---
title: SQLGetDescField 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a590e66bbbe205a7aa218ce03b0d88ed9f940318
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538059"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetDescField**傳回的目前設定或值的單一欄位的描述項記錄。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述項控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的描述項記錄。 描述項記錄編號為 0，0 表示書籤記錄的記錄號碼。 如果*FieldIdentifier*引數會指出標頭欄位中， *RecNumber*會被忽略。 如果*RecNumber*小於或等於 SQL_DESC_COUNT，但資料列不包含資料的資料行或參數，呼叫**SQLGetDescField**會傳回欄位的預設值。 (如需詳細資訊，請參閱 [初始設定的描述元的欄位] 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *FieldIdentifier*  
 [輸入]表示要傳回其值的描述元的欄位。 如需詳細資訊，請參閱 「*FieldIdentifier*引數 」 一節[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 *ValuePtr*  
 [輸出]在其中傳回描述元資訊的緩衝區指標。 資料類型而定的值*FieldIdentifier*。  
  
 如果*ValuePtr*是整數類型、 應用程式應該使用的緩衝區 SQLULEN 和一些驅動程式呼叫此函式之前初始化為 0 的值可能只寫入較低的 32 位元或 16 位元的緩衝區和保留的較高順序位元保持不變。  
  
 如果*ValuePtr*為 NULL，就*StringLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回中指向緩衝區*ValuePtr*。  
  
 *BufferLength*  
 [輸入]如果*FieldIdentifier*是 ODBC 定義欄位並*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*FieldIdentifier*是 ODBC 定義欄位並\* *ValuePtr*是一個整數， *Columnsize*會被忽略。 如果中的值 *\*ValuePtr* Unicode 資料類型 (呼叫時**SQLGetDescFieldW**)，則*Columnsize*引數必須是偶數。  
  
 如果*FieldIdentifier*驅動程式定義的欄位，應用程式設定指出欄位給驅動程式管理員性質*Columnsize*引數。 *BufferLength*可以有下列值：  
  
-   如果 *\*ValuePtr*是字元字串的指標，則*Columnsize*是 sql_nts; 之字串的長度。  
  
-   如果 *\*ValuePtr*是二進位的緩衝區的指標，則應用程式會放 SQL_LEN_BINARY_ATTR 的結果 (*長度*) 中的巨集*Columnsize*。 這會放在負值*Columnsize*。  
  
-   如果 *\*ValuePtr*是字元字串或二進位字串，以外的值的指標，則*Columnsize*應有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定長度資料類型，則*Columnsize*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT，還是 SQL_IS_USMALLINT，適當地。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不包括 null 結束字元所需的位元組數） 的緩衝區指標可用來傳回中 **ValuePtr*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 sql_no_data 之後或 SQL_INVALID_HANDLE。  
  
 如果，則會傳回 SQL_NO_DATA *RecNumber*大於目前的描述項記錄的數目。  
  
 如果，則會傳回 SQL_NO_DATA *DescriptorHandle* IRD 的控制代碼和陳述式是在已備妥或已執行的狀態，但沒有任何與其相關聯的開啟資料指標。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescField**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetDescField** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *ValuePtr*仍不夠大，無法傳回完整的描述項欄位，因此欄位已遭截斷。 中會傳回未截斷的描述項欄位的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|描述項索引無效|(DM) *RecNumber*引數等於 0，SQL_ATTR_USE_BOOKMARK 陳述式屬性是 SQL_UB_OFF，而*DescriptorHandle*引數為 IRD 控制代碼。 （這項錯誤可以被傳回明確配置描述項的描述元與陳述式控制代碼相關聯時，才）。<br /><br /> *FieldIdentifier*引數就是 [記錄] 欄位中， *RecNumber*引數為 0，而*DescriptorHandle*引數為 IPD 控點。<br /><br /> *RecNumber*引數為小於 0。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY007|尚未備妥相關聯的陳述式|*DescriptorHandle*與相關聯*StatementHandle* IRD，以及相關聯的陳述式控制代碼必須尚未準備或執行。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與建立關聯*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和仍在呼叫此函式時所執行。<br /><br /> (DM) *DescriptorHandle*與建立關聯*StatementHandle*讓**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已呼叫且傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*DescriptorHandle*。 此非同步函式仍在執行時**SQLGetDescField**呼叫函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY021|不一致的描述元資訊|電子郵件地址 和 SQL_DESC_DATETIME_INTERVAL_CODE SQL_DESC_TYPE 欄位並非來自有效的 ODBC SQL 類型、 有效驅動程式特定 SQL 的型別 （Ipd) 或有效的 ODBC C 類型 （適用於 Apd 或 ARDs）。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*是字元字串，以及*Columnsize*小於零。|  
|HY091|無效的描述項欄位識別碼|*FieldIdentifier*不是 ODBC 定義的欄位，而並沒有實作定義的值。<br /><br /> *FieldIdentifier*已針對未定義*DescriptorHandle*。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLGetDescField**傳回描述項記錄的單一欄位的值。 呼叫**SQLGetDescField**可以傳回任何描述項類型，包括標頭欄位中，記錄的欄位和書籤欄位中的任何欄位的設定。 應用程式可以取得相同或不同的描述，以任意順序，在多個欄位的設定，藉由重複的呼叫**SQLGetDescField**。 **SQLGetDescField**也可以呼叫以傳回驅動程式定義的描述項欄位。  
  
 基於效能考量，應用程式不應該呼叫**SQLGetDescField**的 IRD 之前執行的陳述式。  
  
 描述的名稱、 資料類型和資料行或參數資料的儲存體的多個欄位的設定也可以在單一呼叫中擷取**SQLGetDescRec**。 **SQLGetStmtAttr**可以呼叫以傳回單一欄位的設定，同時也是陳述式屬性描述項標頭中。 **SQLColAttribute**， **SQLDescribeCol**，以及**SQLDescribeParam**傳回記錄或書籤的欄位。  
  
 當應用程式呼叫**SQLGetDescField**擷取未定義特定的描述元類型欄位的值，此函式都會傳回 SQL_SUCCESS，但是傳回欄位的值會是未定義。 例如，呼叫**SQLGetDescField** APD 或 ARD 與 SQL_DESC_NAME 或 SQL_DESC_NULLABLE 欄位將會傳回 SQL_SUCCESS，但未定義欄位的值。  
  
 當應用程式呼叫**SQLGetDescField**若要擷取特定的描述元類型定義但沒有預設值而且尚未設定欄位的值，則函數會傳回 SQL_SUCCESS 不過傳回的值欄位會定義。 描述項欄位和描述欄位的初始化資訊，請參閱 [初始設定的描述元的欄位]，在[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需有關描述項的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一的描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
