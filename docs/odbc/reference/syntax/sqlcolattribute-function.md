---
title: SQLCol屬性函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94de3dfc7036277f8be56c401326cdab07a9606
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301288"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLColAttribute**傳回結果集中列的描述符資訊。 描述符資訊將作為字串、描述符相關值或整數值返回。  
  
> [!NOTE]  
>  有關驅動程式管理員將此功能映射到 ODBC 3 時的詳細資訊。*x*應用程式使用 ODBC 2。*x*驅動程式,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *ColumnNumber*  
 [輸入]要從中檢索欄位值的 IRD 中的記錄數。 此參數對應於結果數據的列數,按增加列順序順序排序,從 1 開始。 列可以按任意順序描述。  
  
 列 0 可以在此參數中指定,但除SQL_DESC_TYPE和SQL_DESC_OCTET_LENGTH之外的所有值都將返回未定義的值。  
  
 *FieldIdentifier*  
 [輸入]描述符句柄。 此句柄定義應查詢 IRD 中的哪個欄位(例如,SQL_COLUMN_TABLE_NAME)。  
  
 *CharacterAttributePtr*  
 【輸出]指標指向要返回 IRD*的「列編號*」行*的欄位識別字*段中的值的緩衝區,如果該欄位是字串。 否則,該欄位將未使用。  
  
 如果*字元屬性Ptr*為 NULL,*則 StringLengthPtr*仍將返回字元*屬性Ptr*指向的緩衝區中可用於返回的位元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*Field 識別碼*是 ODBC 定義的欄位,而*字串屬性 Ptr*指向字串或二進位緩衝區,\*則此參數應為*字元屬性 Ptr*的長度。 如果*字段識別碼*是 ODBC 定義\*的欄位, 而*字元屬性*Ptr 是整數,則忽略此欄位。 如果*\*字元屬性Ptr*是 Unicode 字串(在呼叫**SQLColAttributeW**時),*緩衝區長度*參數必須是偶數。 如果*Field 識別碼*是驅動程式定義的欄位,則應用程式透過設定*BufferLength*參數向驅動程式管理員指示該欄位的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*字元屬性Ptr*是指向指標的指標,*則緩衝區長度*應具有SQL_IS_POINTER值。  
  
-   如果*字元屬性Ptr*是指向字串的指標,則*緩衝區長度*是緩衝區的長度。  
  
-   如果*字元屬性Ptr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*字元屬性Ptr*是指向固定長度數據類型的指標,*則緩衝區長度*必須是以下類型之一:SQL_IS_INTEGER、SQL_IS_UNINTEGER、SQL_SMALLINT 或 SQLUSMALLINT。  
  
 *字串長度 Ptr*  
 【輸出]指向一個緩衝區的指標,其中返回可用於在 #*字元屬性Ptr*中返回的位元組總數(不包括字元資料的空終止字節)。  
  
 對於字元數據,如果可供返回的位元組數大於或等於*BufferLength,*\**則字元屬性 Ptr*中的描述符資訊將被截斷為*BufferLength*減去空終止字元的長度,並且由驅動程式終止。  
  
 對於所有其他類型的數據,將忽略*BufferLength*的值,驅動程式假定 #*字元屬性Ptr*的大小為 32 位元。  
  
 *數位屬性Ptr*  
 【輸出]指標指向整數緩衝區,用於在其中返回 IRD*的「列編號*」行的*欄位識別符*欄位中的值,如果該欄位是數位描述符類型(如SQL_DESC_COLUMN_LENGTH)。 否則,該欄位將未使用。 請注意,某些驅動程式可能只寫入緩衝區的下 32 位元或 16 位元,並且保持高階位不變。 因此,應用程式在調用此函數之前應初始化該值為 0。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColAttribute**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT*Handle*的*句柄類型*和*語句句柄*。 下表列出了**SQLColAttribute**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\**字元屬性Ptr*不夠大,無法返回整個字串值,因此字串值被截斷。 未壓縮字串值的長度在 #*StringLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07005|已準備好的語句不是*游標規範*|與*語句句柄*關聯的語句未返回結果集,*並且欄位標識符*未SQL_DESC_COUNT。 沒有要描述的列。|  
|07009|不合法的描述符索引|(DM) 為*列編號*指定的值等於 0,並且SQL_ATTR_USE_BOOKMARKS語句屬性SQL_UB_OFF。<br /><br /> 為參數*ColumnNumber*指定的值大於結果集中的列數。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagField**從診斷數據結構返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQLColAttribute 時,此 aynchronous 函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 在調用**SQLPrepare、SQLExecDirect**或*語句句柄*的目錄函數之前**SQLPrepare**調用函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM)*\*字元屬性Ptr*是一個字元字串,*緩衝區長度*小於 0 但不等於SQL_NTS。|  
|HY091|不合法的字段識別碼|為參數*FieldIdentifier*指定的值不是定義的值之一,不是實現定義的值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|驅動程式無法|驅動程式不支援為參數*欄位識別符*指定的值。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
 在**SQLPrepare**之後和**SQLExecute**之前調用時 **,SQLColAttribute**可以傳回**SQLPrepare**或**SQLExecute**可以傳回的任何 SQLSTATE,具體取決於資料源何時計算與*語句句柄*關聯的 SQL 語句。  
  
 出於性能原因,應用程式在執行語句之前不應調用**SQLColAttribute。**  
  
## <a name="comments"></a>註解  
 有關應用程式如何使用**SQLColAttribute**傳回的資訊的資訊,請參閱[結果集元資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**\*傳回*數位屬性Ptr*或\**字元屬性Ptr*中的資訊。 整數資訊在\**數位屬性Ptr*中作為SQLLEN值返回;所有其他格式的資訊都返回\*在*字元屬性Ptr*中。 在\**數字屬性Ptr*中傳回資訊時,驅動程式會忽略*字串屬性的Ptr、**緩衝區長度*與*字串長度Ptr*。 當在\**字元屬性Ptr*中傳回資訊時,驅動程式會忽略*數字屬性的Ptr*。  
  
 **SQLColAttribute**從 IRD 的描述符欄位返回值。 函數使用語句句柄而不是描述符句柄調用。 **SQLColAttribute**為本節後面列出的*欄位識別碼*值返回的值也可以透過使用適當的 IRD 句柄呼叫**SQLGetDescField**來檢索。  
  
 當前定義的描述符位、引入它們的 ODBC 版本以及為其返回資訊的參數在本節的後面部分顯示;驅動程式可以定義更多的描述符類型,以利用不同的數據來源。  
  
 ODBC 3.*x*驅動程式必須為每個描述符欄位返回一個值。 如果描述字段不適用於驅動程式或資料來源,除非另有說明,否則驅動程式在\**StringLengthPtr*中傳回 0 或在 #*字元屬性 Ptr*中傳回一個空字串。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 ODBC 3.*x*函數**SQLColAttribute**替換已棄用的 ODBC 2。*x*函數**SQLColattributes**。 將**SQLColattributes**映射到**SQLColattribute**時(當 ODBC 2 時)。*x*應用程式使用 ODBC 3。*x*驅動程式),或將**SQLColattribute**映射到**SQLColattributes(** 當 ODBC 3 時)。*x*應用程式使用 ODBC 2。*x*驅動程式),驅動程式管理員傳遞*欄位識別碼*的值,將其映射到新值,或傳回錯誤,如下所示:  
  
> [!NOTE]  
>  ODBC 3 中*字段識別碼*中使用的前置碼。*x*已從 ODBC 2 中使用的更改。*x*. . 新首碼為"SQL_DESC";新首碼為"SQL_DESC";如果 "SQL_DESC",則為"SQL_DESC"舊首碼為"SQL_COLUMN"  
  
-   如果 **#defineODBC** 2的值。*x* *字段識別碼*與 ODBC 3**的#define**值相同。*x* *字段標識碼*,函數調用中的值剛剛傳遞。  
  
-   ODBC 2**的值#define。***x* *字段識別碼*SQL_COLUMN_LENGTH、SQL_COLUMN_PRECISION和SQL_COLUMN_SCALE與 ODBC 3**的#define**值不同。*x* *字段標識符*SQL_DESC_PRECISION、SQL_DESC_SCALE 和SQL_DESC_LENGTH。 ODBC 2.*x*驅動程式僅支援 ODBC 2。*x*值。 ODBC 3.*x*驅動程式必須同時支援這三個*字段標識符*的"SQL_COLUMN"和"SQL_DESC"值。 這些值不同,因為在 ODBC 3 中定義精度、比例和長度的方式不同。*x*比在ODBC 2中。*x*. . 有關詳細資訊,請參閱[列大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果 **#defineODBC** 2的值。*x* *字段識別碼*不同於 ODBC 3**的#define**值。*x* *欄位識別碼*,與 COUNT、NAME 和 NULLABLE 值一樣,函數呼叫中的值映射到相應的值。 例如,SQL_COLUMN_COUNT映射到SQL_DESC_COUNT,並且SQL_DESC_COUNT映射到SQL_COLUMN_COUNT,具體取決於映射的方向。  
  
-   如果*字段識別碼*是 ODBC 3 中的新值。*x*,ODBC 2 中沒有相應的值。*x*,當 ODBC 3 時不會映射它。*x*應用程式在 ODBC 2 中呼叫**SQLColAttribute**時使用它。*x*驅動程式,並且調用將返回 SQLSTATE HY091(無效描述符欄位識別碼)。  
  
 下表列出了**SQLColAttribute**傳回的描述符類型。 *數字屬性Ptr*值的類型是**SQLLEN \* **。  
  
|*FieldIdentifier*|資訊<br /><br /> 返回|描述|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*數位屬性Ptr*|如果列是自動遞增列,則SQL_TRUE。<br /><br /> 如果列不是自動增量列或不是數位,則SQL_FALSE。<br /><br /> 此欄位僅適用於數位資料類型列。 應用程式可以將值插入到包含自動增量列的行中,但通常無法更新列中的值。<br /><br /> 當將插入到自動增量列中時,在插入時將一個唯一值插入到列中。 增量未定義,但特定於數據源。 應用程式不應假定自動增量列從任何特定點開始,或由任何特定值增量。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|結果集列的基本列名稱。 如果基本列名稱不存在(如表達式的列),則此變數包含一個空字串。<br /><br /> 此資訊從 IRD 的SQL_DESC_BASE_COLUMN_NAME記錄欄位返回,該記錄欄位是唯讀欄位。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|包含列的基表的名稱。 如果無法定義基表名稱或不適用,則此變數包含一個空字串。<br /><br /> 此資訊從 IRD 的SQL_DESC_BASE_TABLE_NAME記錄欄位返回,該記錄欄位是唯讀欄位。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*數位屬性Ptr*|SQL_TRUE該列是否被視為區分大小寫(用於排序和比較)。<br /><br /> SQL_FALSE如果列不被視為區分大小寫(用於排序規則和比較)或非字元。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含列的表的目錄。 如果列是表達式或列是視圖的一部分,則返回的值是實現定義的。 如果數據來源不支援目錄或無法確定目錄名稱,則傳回一個空字串。 此 VARCHAR 記錄欄位不限於 128 個字元。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*數位屬性Ptr*|簡潔的數據類型。<br /><br /> 對於日期時間和間隔數據類型,此欄位返回簡潔的數據類型;例如,SQL_TYPE_TIME或SQL_INTERVAL_YEAR。 (有關詳細資訊,請參閱附錄 D 中的[資料類型識別碼和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md):資料類型。<br /><br /> 此資訊從 IRD 的SQL_DESC_CONCISE_TYPE記錄欄位返回。|  
|SQL_DESC_COUNT (ODBC 1.0)|*數位屬性Ptr*|結果集中可用的列數。 如果結果集中沒有列,則返回 0。 將忽略*列編號*參數中的值。<br /><br /> 此資訊從 IRD 的SQL_DESC_COUNT標頭欄位返回。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*數位屬性Ptr*|顯示列中資料所需的最大字元數。 關於顯示大小的詳細資訊,請參閱附錄 D:資料型態中的[欄位、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*數位屬性Ptr*|如果列具有特定於數據源的固定精度和非零比例,SQL_TRUE。<br /><br /> 如果列沒有特定於數據源的固定精度和非零比例,則SQL_FALSE。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|列標籤或標題。 例如,名為 EmpName 的列可能標記為「員工姓名」,或者可能標有別名。<br /><br /> 如果列沒有標籤,則返回列名稱。 如果列未標記且未命名,則返回一個空字串。|  
|SQL_DESC_LENGTH (ODBC 3.0)|*數位屬性Ptr*|一個數值,它是字串或二進位資料類型的最大或實際字元長度。 它是固定長度數據類型的最大字元長度,或可變長度數據類型的實際字元長度。 其值始終排除結束字串的空終止位元組。<br /><br /> 此資訊從 IRD 的SQL_DESC_LENGTH記錄欄位返回。<br /><br /> 有關長度的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位包含驅動程式識別為此數據類型文本的前置字元。 此欄位包含不適用於文本前置的資料類型的空字串。 有關詳細資訊,請參閱[文字前置字串與後綴](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位包含驅動程式識別為此數據類型文本的後綴的字元或字元。 此欄位包含不適用於文本後綴的資料類型的空字串。 有關詳細資訊,請參閱[文字前置字串與後綴](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位包含數據類型可能與數據類型的常規名稱不同的任何當地語系化(母語)名稱。 如果沒有當地語系化名稱,則返回一個空字串。 此欄位僅用於顯示目的。 字串的字元集與區域設置相關,通常是伺服器的預設字元集。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|列別名(如果適用)。 如果列別名不適用,則返回列名稱。 在這兩種情況下,SQL_DESC_UNNAMED設置為SQL_NAMED。 如果沒有列名或列別名,則返回一個空字串,並將SQL_DESC_UNNAMED設置為SQL_UNNAMED。<br /><br /> 此資訊從 IRD SQL_DESC_NAME記錄欄位返回。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*數位屬性Ptr*|如果列可以具有 NULL 值,則SQL_ NULLABLE;如果列沒有 NULL 值,則SQL_NO_NULLS;如果列沒有 NULL 值,則為或SQL_NULLABLE_UNKNOWN如果不知道列是否接受 NULL 值。<br /><br /> 此資訊從 IRD 的SQL_DESC_NULLABLE記錄欄位返回。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*數位屬性Ptr*|如果SQL_DESC_TYPE欄位中的數據類型是近似數值數據類型,則此 SQLINTEGER 欄位包含值 2,因為SQL_DESC_PRECISION欄位包含位數。 如果SQL_DESC_TYPE欄位中的數據類型是精確的數位資料類型,則此欄位包含值 10,因為SQL_DESC_PRECISION欄位包含小數位數。 此欄位設置為 0,用於所有非數位數據類型。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*數位屬性Ptr*|字串或二進位數據類型的長度(以位元組為單位)。 對於固定長度字元或二進位類型,這是以位元組為單位的實際長度。 對於可變長度字元或二進位類型,這是以位元組為單位的最大長度。 此值不包括空終止符。<br /><br /> 此資訊從 IRD 的SQL_DESC_OCTET_LENGTH記錄欄位返回。<br /><br /> 有關長度的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*數位屬性Ptr*|數位數據類型表示適用精度的數值。 對於SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP和所有表示時間間隔的間隔數據類型,其值是小數秒元件的適用精度。<br /><br /> 此資訊從 IRD SQL_DESC_PRECISION記錄欄位返回。|  
|SQL_DESC_SCALE (ODBC 3.0)|*數位屬性Ptr*|數值,是數值數據類型的適用比例。 對於 DECIMAL 和數位數據類型,這是定義的比例。 它是未定義的所有其他數據類型。<br /><br /> 此資訊從 IRD 的 SCALE 記錄欄位返回。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含列的表的架構。 如果列是表達式或列是視圖的一部分,則返回的值是實現定義的。 如果數據源不支援架構或無法確定架構名稱,則返回一個空字串。 此 VARCHAR 記錄欄位不限於 128 個字元。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*數位屬性Ptr*|如果列不能在 WHERE 子句中使用,則SQL_PRED_NONE。 (這與 ODBC 2 中的SQL_UNSEARCHABLE值相同。*x*.)<br /><br /> SQL_PRED_CHAR該列是否可以在 WHERE 子句中使用,但只能與 LIKE 謂詞一起使用。 (這與 ODBC 2 中的SQL_LIKE_ONLY值相同。*x*.)<br /><br /> SQL_PRED_BASIC該列是否可以在 WHERE 子句中使用,所有比較運算符(LIKE 除外)。 (這與 ODBC 2 中的SQL_EXCEPT_LIKE值相同。*x*.)<br /><br /> SQL_PRED_SEARCHABLE該列是否可以在任何比較運算符的 WHERE 子句中使用。<br /><br /> 類型SQL_LONGVARCHAR和SQL_LONGVARBINARY的列通常返回SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行之資料表的名稱。 如果列是表達式或列是視圖的一部分,則返回的值是實現定義的。<br /><br /> 如果無法確定表名稱,則返回一個空字串。|  
|SQL_DESC_TYPE (ODBC 3.0)|*數位屬性Ptr*|指定 SQL 資料類型的數值。<br /><br /> 當*列號*等於 0 時,將返回可變長度書籤SQL_BINARY,並為固定長度書籤返回SQL_INTEGER。<br /><br /> 對於日期時間和間隔數據類型,此欄位返回詳細數據類型:SQL_DATETIME或SQL_INTERVAL。 (有關詳細資訊,請參閱附錄 D 中的[資料類型識別碼和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md):資料類型。<br /><br /> 此資訊從 IRD SQL_DESC_TYPE記錄欄位返回。 **註:** 對抗ODBC 2。*x*驅動程式,而是使用SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|與數據源相關的數據類型名稱;例如,"CHAR","VARCHAR","金錢","長VARBINARY",或"CHAR ( ) BIT 數據"。<br /><br /> 如果類型未知,則返回一個空字串。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*數位屬性Ptr*|SQL_NAMED或SQL_UNNAMED。 如果 IRD 的SQL_DESC_NAME欄位包含列別名或列名稱,則返回SQL_NAMED。 如果沒有列名稱或列別名,則返回SQL_UNNAMED。<br /><br /> 此資訊從 IRD 的SQL_DESC_UNNAMED記錄欄位返回。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*數位屬性Ptr*|如果列是無符號的(或不是數位),SQL_TRUE。<br /><br /> 如果對列進行簽名,則SQL_FALSE。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*數位屬性Ptr*|列由定義的常量的值描述:<br /><br /> SQL_ATTR_READONLYSQL_ATTR_WRITESQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE描述結果集中列的升數據度,而不是基表中的列。 結果集列所基於的基礎列的升數據度可能與此欄位中的值不同。 列是否可更新可以基於數據類型、使用者許可權和結果集本身的定義。 如果不清楚列是否可更新,則應返回SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**是**SQLDescribeCol**的可擴充替代方法。 **SQLDescribeCol**傳回一組基於 ANSI-89 SQL 的固定描述符資訊。 **SQLColAttribute**允許造訪 ANSI SQL-92 和 DBMS 供應商擴展中提供的更廣泛的描述符資訊集。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得多行資料|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>範例  
 以下示例代碼不釋放句柄和連接。 有關代碼範例以釋放句柄和語句,請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md),[例的 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)與[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
