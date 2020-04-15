---
title: SQLGetData 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285504"
---
# <a name="sqlgetdata-function"></a>SQLGetData 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetData**在**SQLParamData**返回SQL_PARAM_DATA_AVAILABLE後檢索結果集中的單個列或單個參數的數據。 可以多次調用它來檢索零件中的可變長度數據。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *Col_or_Param_Num*  
 [輸入]對於檢索列數據,它是要返回數據的列數。 結果集列按從 1 開始的列順序增加編號。 書簽列是列編號 0;書簽列為 0。"僅當啟用了書籤時,才能指定此選項。  
  
 對於檢索參數數據,它是參數的元數,從 1 開始。  
  
 *目標型態*  
 [輸入]**目標價值Ptr*緩衝區的 C 資料類型的類型識別碼。 有關有效的 C 資料類型和類型識別碼的清單,請參閱附錄 D:資料類型中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)部分。  
  
 如果*TargetType* SQL_ARD_TYPE,則驅動程式使用 ARD SQL_DESC_CONCISE_TYPE 欄位中指定的類型標識符。 如果*目標類型***SQL_APD_TYPE,SQLGetData**將使用**SQLBind 參數**中指定的相同 C 數據類型。 否則 **,SQLGetData**中指定的 C 數據類型將覆蓋**SQLBind 參數**中指定的 C 資料類型。 如果SQL_C_DEFAULT,驅動程式將基於源的 SQL 數據類型選擇預設 C 資料類型。  
  
 您還可以指定延伸的 C 資料類型。 關於詳細資訊,請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *目標價值Ptr*  
 【輸出]指向要返回數據的緩衝區的指標。  
  
 *目標價值 Ptr*不能為 NULL。  
  
 *緩衝區長度*  
 [輸入]**目標ValuePtr*緩衝區的長度(以位元組為單位)。  
  
 驅動程式使用*BufferLength*來避免在返回可變長\*度數據 (如字元或二進位數據)時寫入*TargetValuePtr*緩衝區的末尾。 請注意,當將字元數據返回到\* *TargetValuePtr*時,驅動程式會計算 null 終止字元。 *因此 *,TargetValuePtr*必須包含 null 終止字元的空間,否則驅動程式將截截數據。  
  
 當驅動程式返回固定長度數據(如整數或日期結構)時,驅動程式將忽略*BufferLength*並假定緩衝區足夠大以容納數據。 因此,應用程式為固定長度數據分配足夠大的緩衝區非常重要,否則驅動程式將寫入緩衝區的末尾。  
  
 當*緩衝區長度*小於 0,但當緩衝區長度為 0 時 **,SQLGetData**返回 SQLSTATE HY090(無效字串或緩衝區長度),但當*緩衝區長度*為 0 時,則返回 SQLSTATE HY090(無效字串或緩衝區長度)。  
  
 *StrLen_or_IndPtr*  
 【輸出]指向要返回長度或指示器值的緩衝區的指標。 如果這是空指標,則不返回長度或指標值。 當提取的資料為 NULL 時,這將傳回錯誤。  
  
 **SQLGetData**可以在長度/指示器緩衝區中傳回以下值:  
  
-   可供傳回的資料的長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 有關詳細資訊,請參閱本主題[中使用長度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和"註釋"。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetData**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT*Handle*的*句柄類型*和*敘述句柄*。 下表列出了**SQLGetData**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|並非所有指定列的數據 *(Col_or_Param_Num*)都可以在單個調用函數中檢索。 SQL_NO_TOTAL或當前調用**SQLGetData**之前在指定列中剩餘數據的\*長度*StrLen_or_IndPtr返回。* (函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> 有關對單個列使用多次調用**SQLGetData**的詳細資訊,請參閱"註釋」。。|  
|01S07|分數截斷|為一個或多個列返回的數據被截斷。 對於數位數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|結果集中欄的數據值不能轉換為參數*TargetType*指定的 C 資料類型。|  
|07009|不合法的描述符索引|為參數*Col_or_Param_Num*指定的值為 0,並且SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF。<br /><br /> 為參數*Col_or_Param_Num*指定的值大於結果集中的欄數。<br /><br /> *Col_or_Param_Num*值不等於可用參數的位數。<br /><br /> (DM) 指定的列已綁定。 此說明不適用於在**SQLGetInfo**中傳回 SQL_GETDATA_EXTENSIONSSQL_GD_BOUND位掩碼SQL_GD_BOUND的驅動程式。<br /><br /> (DM) 指定列的數量小於或等於最高綁定列的數量。 此說明不適用於在**SQLGetInfo**中返回SQL_GD_ANY_COLUMN位掩碼SQL_GETDATA_EXTENSIONS驅動程式。<br /><br /> (DM) 應用程式已為當前行調用**SQLGetData;** 當前調用中指定的列數小於前一個調用中指定的列數;並且驅動程式不返回**SQLGetInfo**中SQL_GETDATA_EXTENSIONS選項的SQL_GD_ANY_ORDER位掩碼。<br /><br /> (DM)*目標類型*參數SQL_ARD_TYPE,並且 ARD 中的*Col_or_Param_Num*描述符記錄未通過一致性檢查。<br /><br /> (DM)*目標類型*參數SQL_ARD_TYPE,ARD SQL_DESC_COUNT欄位中的值小於*Col_or_Param_Num*參數。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22002|需要指標變數,但未提供|*StrLen_or_IndPtr*為空指標,並檢索 NULL 資料。|  
|22003|數值超範圍|返回列的數值(作為數位或字串)將導致數字的整個部分(而不是小數)被截斷。<br /><br /> 關於詳細資訊,請參閱附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|不合法日期時間格式|結果集中的字元列綁定到 C 日期、時間或時間戳結構,並且列中的值分別為無效的日期、時間或時間戳。 關於詳細資訊,請參閱附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|除零|返回算術表達式中導致除以零的值。|  
|22015|間隔欄位溢出|從精確數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位丟失。<br /><br /> 將數據返回到間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。|  
|22018|強制轉換規範的不合法字元值|結果集中的字元列返回到字元 C 緩衝區,該列包含緩衝區的字元集中沒有表示的字元。<br /><br /> C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。|  
|24000|指標狀態無效|(DM) 調用函數時,無需首先調用**SQLFetch**或**SQLFetchScroll**即可將游標定位到所需的數據行上。<br /><br /> (DM)*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。<br /><br /> 在*語句句柄*上打開一個游標,並調用**SQLFetch**或**SQLFetchScroll,** 但游標位於結果集開始之前或結果集結束之後。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY003|程式型別範圍|(DM) 參數*TargetType*不是有效的數據類型,SQL_C_DEFAULT、SQL_ARD_TYPE(檢索列數據)或SQL_APD_TYPE(在檢索參數數據的情況下)。<br /><br /> (DM) 參數*Col_or_Param_Num*為 0,並且參數*TargetType*不SQL_C_BOOKMARK固定長度書籤或可變長度書籤的SQL_C_VARBOOKMARK。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**在*語句句柄*上調用 ,然後在*語句句柄*上再次調用該函數。<br /><br /> 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**從多線程應用程式中的不同線程調用*了語句句柄*,然後在*語句句柄*上再次調用該函數。|  
|HY009|不合法的空白指標|(DM) 參數*TargetValuePtr*是一個空指標。|  
|HY010|函式序列錯誤|(DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLGetData**函數時,此異步函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM)*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。<br /><br /> 對**SQLExeceute、SQLExecDirect**或**SQLMore 結果**的呼叫SQL_PARAM_DATA_AVAILABLE返回,但呼叫**SQLGetData**而不是**SQLExecDirect****SQLParamData**。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength*指定的值小於 0。<br /><br /> 為參數*BufferLength*指定的值小於*4,Col_or_Param_Num*參數設置為 0,驅動程式為 ODBC 2 *.x*驅動程式。|  
|HY109|游標位置無效|游標被定位在已刪除或無法提取的行上(由 SQLSetPos、SQLFetch、SQLFetchScroll 或**SQLBulk 操作)。** **SQLSetPos** **SQLFetch** **SQLFetchScroll**<br /><br /> 游標是僅前進的游標,行集大小大於 1。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援在**SQLFetchScroll**中使用具有多行的**SQLGetData。** 此說明不適用於在**SQLGetInfo**中傳回SQL_GETDATA_EXTENSIONS選項的SQL_GD_BLOCK位掩碼的驅動程式。<br /><br /> 驅動程式或資料來源不支援*由 TargetType*參數和相應列的 SQL 資料類型的組合指定的轉換。 僅當列的 SQL 資料類型映射到特定於驅動程式的 SQL 資料類型時,此錯誤才適用。<br /><br /> 驅動程式僅支援 ODBC 2 *.x*,參數*TargetType*是以下參數之一:<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 和附錄 D 中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)中列出的任何間隔 C 資料類型:資料類型。<br /><br /> 驅動程式僅支援 3.50 之前的 ODBC 版本,並且參數*TargetType* SQL_C_GUID。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*對應的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLGetData**傳回指定列中的數據。 **SQLGetData**只能在從**SQLFetch、SQLFetchScroll**或**SQL 擴展獲取**集的結果集中**SQLFetchScroll**獲取一個或多個行後才能調用。 如果可變長度數據太大,無法在**SQLGetData**的單個調用中返回(由於應用程式中的限制 **),SQLGetData**可以分部分檢索它。 可以綁定一行中的某些列,併為其他列調用**SQLGetData,** 儘管這受一些限制。 有關詳細資訊,請參閱[獲取長資料](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 有關使用具有串流式輸出參數的**SQLGetData**的資訊,請參考[使用 SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGet 資料  
 如果驅動程式不支援**SQLGetData**的擴展,則函數只能返回數位大於最後一個綁定列的未綁定列的數據。 此外,在一行數據中,對**SQLGetData**的每個調用中*Col_or_Param_Num*參數的值必須大於或等於上一個調用中*Col_or_Param_Num*的值;也就是說,必須按增加列號順序檢索數據。 最後,如果沒有支援擴展,則如果行集大小大於 1,則無法調用**SQLGetData。**  
  
 司機可以放寬任何這些限制。 要確定驅動程式放寬的限制,應用程式使用以下任意SQL_GETDATA_EXTENSIONS選項呼叫**SQLGetInfo:**  
  
-   可以調用 SQL_GD_OUTPUT_PARAMS = **SQLGetData**來傳回輸出參數值。 有關詳細資訊,請參閱使用[SQLGetData 檢索輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN 如果返回此選項,則可以為任何未綁定列(包括最後一個綁定列之前的列)調用**SQLGetData。**  
  
-   SQL_GD_ANY_ORDER 如果返回此選項,則可以按任意順序為未綁定列調用**SQLGetData。**  
  
-   SQL_GD_BLOCK 如果**SQLGetInfo**為SQL_GETDATA_EXTENSIONS InfoType 傳回此選項,則當行集大小大於 1 時,驅動程式支援對**SQLGetData**的呼叫,並且應用程式可以使用 SQL_POSITION 選項呼叫**SQLSetPos,** 在呼叫**SQLGetData**之前將游標定位在正確的行上。  
  
-   SQL_GD_BOUND 如果返回此選項,則可以為綁定列和無綁定列調用**SQLGetData。**  
  
 這些限制有兩個例外,一個司機可以放鬆這些限制。 首先,當行集大小大於 1 時,不應為僅轉發游標調用**SQLGetData。** 其次,如果驅動程式支援書籤,它必須始終支援為列 0 調用**SQLGetData**的能力,即使它不允許應用程式在最後一個綁定列之前為其他列調用**SQLGetData。** (當應用程式使用 ODBC 2 *.x*驅動程式時 **,SQLGetData**將在調用**SQLFetch**後*以等於*0 的Col_or_Param_Num調用時成功返回書籤,因為**SQLFetch**由 ODBC 3 *.x*驅動程式管理器映射到具有 SQL_FETCH_NEXT的*提取方向*的**SQLExtendedFetch,** 並且具有*Col_or_Param_Num* 0 的**SQLGetData**由 ODBC 3 *.x*驅動程式管理器映射到**SQLGetStmtOption,** 該驅動程式具有 SQL_GET_BOOKMARK 選項。 *fOption*  
  
 **SQLGetData**不能用於檢索剛剛插入的行的書籤,該行使用SQL_ADD選項調用**SQLBulk 操作**,因為游標未定位在行上。 應用程式可以通過綁定列 0 檢索此類行的書籤,然後再使用 SQL_ADD調用**SQLBulk 操作**,在這種情況下**SQLBulk 操作**將返回綁定緩衝區中的書籤。 然後,可以使用SQL_FETCH_BOOKMARK調用**SQLFetchScroll,** 以重新置放該行上的游標。  
  
 如果*TargetType*參數是間隔數據類型,則分別用於資料中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中設置的預設間隔前導精度 (2) 和預設間隔秒精度 (6)。 如果*TargetType*參數是SQL_C_NUMERIC數據類型,則數據將使用在 ARD SQL_DESC_PRECISION和SQL_DESC_SCALE欄位中設置的預設精度(驅動程式定義)和預設比例 (0)。 如果任何預設精度或比例不合適,應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置相應的描述符欄位。 它可以將SQL_DESC_CONCISE_TYPE欄位設置為SQL_C_NUMERIC,並將**SQLGetData**與*SQL_ARD_TYPE的 TargetType*參數調用,這將導致使用描述符欄位中的精度和縮放值。  
  
> [!NOTE]
>  在 ODBC 2 *.x*中,應用程式將*TargetType*設置為SQL_C_DATE、SQL_C_TIME或SQL_C_TIMESTAMP,以指示\* *TargetValuePtr*是日期、時間或時間戳結構。 在 ODBC 3 *.x*中,應用程式將*TargetType*設置為SQL_C_TYPE_DATE、SQL_C_TYPE_TIME或SQL_C_TYPE_TIMESTAMP。 驅動程式管理員根據需要根據應用程式和驅動程式版本進行適當的映射。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>以索零件中的可變長度資料  
 **SQLGetData**可用於從包含部分可變長度數據的列中檢索數據 ,即當列的 SQL 數據類型的標識符為SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY 或變數長度類型的特定於驅動程序的標識符時。  
  
 若要從部分列中檢索數據,應用程式會連續多次為同一列調用**SQLGetData。** 每次調用時 **,SQLGetData**都會返回數據的下一部分。 由應用程式重新組裝零件,注意從字元數據的中間部分中刪除 null 終止字元。 如果有更多的數據要返回或為終止字元分配了足夠的緩衝區 **,SQLGetData**將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004(數據截斷)。 當它返回數據的最後一部分時 **,SQLGetData**返回SQL_SUCCESS。 在從列檢索數據的最後一個有效調用上,不能返回SQL_NO_TOTAL或零,因為應用程式隨後無法知道應用程式緩衝區中有多少數據有效。 如果在此之後調用**SQLGetData,** 它將返回SQL_NO_DATA。 有關詳細資訊,請參閱下一節"使用 SQLGetData 檢索數據"。  
  
 可變長度書籤可以通過**SQLGetData**以零件返回。 與其他數據一樣,調用**SQLGetData**返回部分中的可變長度書籤將返回 SQLSTATE 01004(字串數據,右截斷),並在要返回的數據更多時返回SQL_SUCCESS_WITH_INFO。 這與對**SQLFetch**或**SQLFetchScroll**的調用截斷可變長度書籤的情況不同,後者返回SQL_ERROR和 SQLSTATE 22001(字串數據,右截斷)。  
  
 **SQLGetData**不能用於返回零件中的固定長度數據。 如果**SQLGetData**在一行中為包含固定長度數據的列調用了多個次,則它將返回第一個長度數據之後的所有調用SQL_NO_DATA。  
  
## <a name="retrieving-streamed-output-parameters"></a>檢索流輸出參數  
 如果驅動程式支援流式輸出參數,應用程式可以多次使用小緩衝區調用**SQLGetData**以檢索較大的參數值。 有關流輸出參數的詳細資訊,請參閱使用[SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 的索資料  
 要返回指定欄的資料 **,SQLGetData**將執行以下步驟序列:  
  
1.  如果已返回列的所有數據,則返回SQL_NO_DATA。  
  
2.  如果\*資料為 NULL,則將*StrLen_or_IndPtr*集SQL_NULL_DATA。 如果數據為 NULL,並且*StrLen_or_IndPtr*為空指標 **,SQLGetData**將返回 SQLSTATE 22002(需要指標變數,但未提供)。  
  
     如果列的數據不是**NULL,SQLGetData**將繼續執行步驟 3。  
  
3.  如果SQL_ATTR_MAX_LENGTH語句屬性設置為非零值,則如果列包含字元或二進位資料,並且以前未為列調用**SQLGetData,** 則數據將被截斷為SQL_ATTR_MAX_LENGTH位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH語句屬性旨在減少網路流量。 它通常由數據源實現,數據源在通過網路返回數據之前會截截數據。 驅動程序和數據源不需要支援它。 因此,為了保證數據被截斷到特定大小,應用程式應分配該大小的緩衝區,並在*BufferLength 參數*中指定大小。  
  
4.  將資料轉換為*TargetType*中指定的類型。 數據為該數據類型的預設精度和縮放。 如果*TargetType* SQL_ARD_TYPE,則使用 ARD SQL_DESC_CONCISE_TYPE欄位中的數據類型。 如果*SQL_ARD_TYPE TargetType,* 則根據SQL_DESC_CONCISE_TYPE欄位中的數據類型,在 ARD 的SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION和SQL_DESC_SCALE欄位中為數據提供精度和縮放。 如果任何預設精度或比例不合適,應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置相應的描述符欄位。  
  
5.  如果資料轉換為可變長度資料型態(如字元或二進位 **),SQLGetData**將檢查資料的長度是否超過*BufferLength*。 如果字元數據的長度(包括空終止字元)超過**BufferLength,SQLGetData**會截截到*緩衝區長度*,減去空終止字元*BufferLength*的長度。 然後,它將終止數據。 如果二進位數據的長度超過數據緩衝區的長度 **,SQLGetData**會將其截截為*緩衝區長度*位元組。  
  
     如果提供的數據緩衝區太小,無法容納 null 終止字元,則**SQLGetData**將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004。  
  
     **SQLGetData**從不截截轉換為固定長度數據類型的數據;它總是假定 **目標價值Ptr*的長度是數據類型的大小。  
  
6.  將轉換(並可能截斷)的資料\*放在*TargetValuePtr 中*。 請注意 **,SQLGetData**無法將數據返回行外。  
  
7.  將資料的長度放在\**StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*為空指標 **,SQLGetData**不會返回長度。  
  
    -   對於字元或二進位數據,這是轉換後和由於*BufferLength*而截斷之前的數據長度。 如果驅動程式無法確定轉換后的數據長度(有時與長數據的情況一樣),它將返回SQL_SUCCESS_WITH_INFO並將長度設置為SQL_NO_TOTAL。 (對**SQLGetData**的最後一次調用必須始終返回數據的長度,而不是零或SQL_NO_TOTAL。如果資料由於SQL_ATTR_MAX_LENGTH語句屬性而被截斷,則此屬性的值(相對於實際長度)將放在\**StrLen_or_IndPtr*。 這是因為此屬性旨在在轉換之前截截伺服器上的數據,因此驅動程式無法確定實際長度。 當**SQLGetData**連續多次調用同一列時,這是當前調用開始時可用數據的長度;也就是說,每次後續調用的長度都會降低。  
  
    -   對於所有其他數據類型,這是轉換后的數據長度;也就是說,它是數據轉換到的類型的大小。  
  
8.  如果在轉換過程中將數據截斷而不丟失顯著性(例如,當轉換為整數 1 時,實際數位 1.234 被截斷),或者由於*BufferLength*太小(例如,字串"abcdef"放置在 4 位元組緩衝區中 **),SQLGetData**返回 SQLSTATE 01004(數據截斷)並SQL_SUCCESS_WITH_INFO。 如果數據被截斷,而不會因SQL_ATTR_MAX_LENGTH語句屬性而丟失顯著性 **,SQLGetData**將返回SQL_SUCCESS,並且不返回 SQLSTATE 01004(數據截斷)。  
  
 如果**SQLGetData**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則綁定數據緩衝區的內容(如果在綁定列上調用**SQLGetData)** 和長度/ 指示器緩衝區未定義。  
  
 對**SQLGetData**的連續調用將從請求的最後一列檢索數據;以前的偏移量無效。 例如,當執行以下序列時:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 對 SQLGetData(icol_n) 的第二次調用從 n 列的開頭檢索數據。 由於以前調用該列的**SQLGetData,** 資料中的任何偏移量都不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述符與 SQLGetData  
 **SQLGetData**不直接與任何描述符欄位互動。  
  
 如果*TargetType* SQL_ARD_TYPE,則使用 ARD SQL_DESC_CONCISE_TYPE欄位中的數據類型。 如果*TargetType*是SQL_ARD_TYPE或SQL_C_DEFAULT,則根據SQL_DESC_CONCISE_TYPE欄位中的數據類型,在 ARD 的SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION和SQL_DESC_SCALE字段中為數據提供精度和比例。  
  
## <a name="code-example"></a>程式碼範例  
 在下面的示例中,應用程式執行**SELECT**語句,以返回按名稱、ID 和電話號碼排序的客戶 ID、名稱和電話號碼的結果集。 對於每行數據,它會調用**SQLFetch**將游標定位到下一行。 它調用**SQLGetData**來檢索提取的數據;在調用**SQLGetData**中指定了數據的緩衝區和返回的位元組數。 最後,它列印每個員工的姓名、ID 和電話號碼。  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|為結果集中的列配置儲存|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行與區塊游標位置無關的批次操作|[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|解除敘述處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 語句|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以只轉寄方向取得資料或資料區塊|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在執行時傳送參數資料|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位游標、刷新列集中中的資料或更新或移除列集中中的資料|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
