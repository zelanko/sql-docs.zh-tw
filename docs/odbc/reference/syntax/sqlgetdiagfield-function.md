---
title: SQLGetDiagfield 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285428"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函數

**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetDiagField**傳回包含錯誤、警告和狀態資訊的診斷資料結構記錄欄位(與指定句柄關聯)的當前值。  
  
## <a name="syntax"></a>語法  
  
```cpp

SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]描述需要診斷的句柄類型的句柄類型標識符。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄僅由驅動程式管理器和驅動程式使用。 應用程式不應使用此句柄類型。 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]診斷數據結構的句柄,由*HandleType*指示的類型。 如果*HandleType*是SQL_HANDLE_ENV,*則句柄*可以是共用環境句柄,也可以是非共用環境句柄。  
  
 *RecNumber*  
 [輸入]指示應用程式從中查找資訊的狀態記錄。 狀態記錄從 1 編號。 如果*DiagIdentifier*參數指示診斷標頭的任何欄位,則*忽略 RecNumber。* 如果不是,它應該大於 0。  
  
 *診斷器識別碼*  
 [輸入]指示要返回其值的診斷欄位。 有關詳細資訊,請參閱"註釋"中的"*診斷標識符*參數"部分。  
  
 *迪亞格福普*  
 【輸出]指向用於返回診斷資訊的緩衝區的指標。 數據類型取決於*Diag識別子*的值。 如果*DiagInfoPtr*是整數類型,則應用程式應使用 SQLULEN 的緩衝區,並在調用此函數之前將值初始化為 0,因為某些驅動程式可能只寫入緩衝區的較低 32 位元或 16 位元,並且保持高階位不變。  
  
 如果*DiagInfoPtr*為 NULL,*則 StringLengthPtr*仍將傳回在*DiagInfoPtr*指向的緩衝區中傳回的位元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*DiagIdentifier*是 ODBC 定義的診斷,並且*DiagInfoPtr*指向字元字串或二進位緩衝區\*,則此參數應為*DiagInfoPtr*的長度。 如果*Diag 識別碼*是 ODBC\*定義的欄位,而*DiagInfoPtr*是整數,則忽略*緩衝區長度*。 如果*\*DiagInfoPtr*中的值是 Unicode 字串(在調用**SQLGetDiagFieldW**時),*則緩衝區長度*參數必須是偶數。  
  
 如果*DiagIdentifier*是驅動程式定義的欄位,則應用程式通過設置*BufferLength*參數向驅動程式管理器指示該欄位的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*DiagInfoPtr*是指向字串的指標,*則緩衝區長度*是字串的長度或SQL_NTS。  
  
-   如果*DiagInfoPtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*DiagInfoPtr*是指向字串或二進位元字串以外的值的指標,則*BufferLength*應具有該值SQL_IS_POINTER。  
  
-   如果*\*DiagInfoPtr*包含固定長度的數據類型,則*緩衝區長度*將根據需要SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT。  
  
 *字串長度 Ptr*  
 【輸出]指向緩衝區的指標,用於傳回字元資料的位元組總數(不包括空終止字元所需的位元), 可用於在\**DiagInfoPtr*中傳回。 如果可用於返回的位元組數大於或等於*BufferLength,*\**則 DiagInfoPtr*中的文本將被截斷為 *「緩衝區長度*」減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE或SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagField**不會自行發佈診斷記錄。 它使用以下返回值來報告其自身執行的結果:  
  
-   SQL_SUCCESS:該功能已成功返回診斷資訊。  
  
-   \* *SQL_SUCCESS_WITH_INFO:DiagInfoPtr*太小,無法容納請求的診斷欄位。 因此,診斷欄位中的數據被截斷。 要確定發生截斷,應用程式必須將*BufferLength*與實際可用位元組數進行比較,該位元組數寫入 **StringLengthPtr*。  
  
-   *SQL_INVALID_HANDLE:HandleType*和*Handle*指示的句柄不是有效的句柄。  
  
-   SQL_ERROR: 發生了以下情況之一:  
  
    -   *Diag識別符參數*不是有效值之一。  
  
    -   *DiagIdentifier 參數*SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE 或SQL_DIAG_ROW_COUNT,但*Handle*不是語句句柄。 (驅動程式管理員返回此診斷。  
  
    -   當*Diag識別碼*指示診斷記錄中的欄位時 *,RecNumber*參數為負數或 0。 對於標頭欄位,將忽略*RecNumber。*  
  
    -   要求的值是字串,*緩衝區長度*小於零。  
  
    -   使用非同步通知時,句柄上的非同步操作未完成。  
  
-   SQL_NO_DATA: *RecNumber*大於*在 Handle*中指定的句柄存在的診斷記錄數。 如果*Handle*沒有診斷記錄,則函數還會返回任何正*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>註解  
 應用程式通常呼叫**SQLGetDiagField**來實現三個目標之一:  
  
1.  在函數調用返回SQL_ERROR或SQL_SUCCESS_WITH_INFO(或**SQL_NEED_DATA SQLBrowseConnect**函數)時獲取特定的錯誤或警告資訊。  
  
2.  確定資料來源使用呼叫**SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos(** 從SQL_DIAG_ROW_COUNT標頭欄位**SQLExecDirect**)執行的資料來源中受影響的行數,或者如果驅動程式可以提供此資訊(從SQL_DIAG_CURSOR_ROW_COUNT標頭字段)。  
  
3.  確定哪個函數是通過調用**SQLExecDirect**或**SQLExecute(** 從SQL_DIAG_DYNAMIC_FUNCTION和SQL_DIAG_DYNAMIC_FUNCTION_CODE標頭欄位)執行的。  
  
 任何 ODBC 函數每次調用時都可以發佈零個或多個診斷記錄,因此應用程式可以在任何 ODBC 函數調用後調用**SQLGetDiagField。** 任何一次可以存儲的診斷記錄數量沒有限制。 **SQLGetDiagField**僅檢索最近與*Handle*參數中指定的診斷數據結構關聯的診斷資訊。 如果應用程式呼叫的 ODBC 函數不是**SQLGetDiagField**或**SQLGetDiagRec,** 則以前具有相同句柄的調用中的任何診斷資訊都丟失。  
  
 只要**SQLGetDiagField**傳回SQL_SUCCESS,應用程式就可以透過增加*RecNumber*來掃描所有診斷記錄。 狀態記錄數在SQL_DIAG_NUMBER頁標題欄位中指示。 對**SQLGetDiagField 的**調用對標頭和記錄欄位沒有破壞性。 應用程式可以稍後再次調用**SQLGetDiagField**從記錄中檢索欄位,只要臨時未調用診斷函數以外的函數,該函數將在同一句柄上發佈記錄。  
  
 應用程式可以調用**SQLGetDiagField**隨時返回任何診斷欄位,但SQL_DIAG_CURSOR_ROW_COUNT或SQL_DIAG_ROW_COUNT除外,如果*Handle*不是語句句柄,則返回SQL_ERROR。 如果未定義任何其他診斷欄位,則對**SQLGetDiagField**的調用將返回SQL_SUCCESS(前提是未遇到其他診斷),並為該欄位返回未定義的值。  
  
 有關詳細資訊,請參閱使用[SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) [並實現 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 調用非同步執行的 API 以外的 API 將生成 HY010"函數序列錯誤" 但是,在異步操作完成之前無法檢索錯誤記錄。  
  
## <a name="handletype-argument"></a>句柄類型參數  
 每個句柄類型都可以具有與其關聯的診斷資訊。 *句柄型態*參數指示*句柄類型的句柄*。  
  
 無法為環境、連接、語句和描述符句柄返回某些標頭和記錄欄位。 以下"標題欄位"和"記錄欄位"部分中指示欄位不適用的句柄。  
  
 如果*HandleType*是SQL_HANDLE_ENV,*則句柄*可以是共用環境句柄,也可以是非共用環境句柄。  
  
 不應將特定於驅動程序的標頭診斷欄位與環境句柄關聯。  
  
 為描述符句柄定義的唯一診斷標頭欄位是SQL_DIAG_NUMBER和SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>診斷參數  
 此參數指示診斷數據結構所需的欄位的標識碼。 如果*RecNumber*大於或等於 1,則欄位中的數據將描述函數返回的診斷資訊。 如果*RecNumber*為 0,則該欄位位於診斷資料結構的標頭中,因此包含與返回診斷資訊的函數調用相關的數據,而不是特定資訊的數據。  
  
 驅動程式可以在診斷數據結構中定義特定於驅動程序的標頭和記錄欄位。  
  
 使用 ODBC 2 *.x*驅動程式的 ODBC 3 *.x*應用程式只能使用 SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME或SQL_DIAG_SQLSTATE的*Diag標識符*參數呼叫**SQLGetDiagField。** 所有其他診斷欄位將返回SQL_ERROR。  
  
## <a name="header-fields"></a>標題欄位  
 下表中列出的標頭欄位可以包含在*DiagIdentifier*參數中。  
  
|診斷器識別碼|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此欄位包含游標中的行數。 其語義取決於 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2和 SQL_STATIC_CURSOR_ATTRIBUTES2的**SQLGetInfo**資訊類型,它們指示每種游標類型(在SQL_CA2_CRC_EXACT和SQL_CA2_CRC_APPROXIMATE位)可用的行計數。<br /><br /> 此欄位的內容僅為語句句柄定義,並且僅在調用**SQLExecute、SQLExecDirect**或**SQLMore 結果**之後。 **SQLExecute** 呼叫**SQLGetDiagField**時,在語句句柄之外,使用 SQL_DIAG_CURSOR_ROW_COUNT的*Diag 標識符*將返回SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR ||這是一個字串,用於描述基礎函數執行的 SQL 語句。 (有關特定值,請參閱本節後面的"動態函數位段的值"。此欄位的內容僅為語句句柄定義,並且僅在調用**SQLExecute、SQLExecDirect**或**SQLMore****SQLExecute**結果 後定義。 呼叫**SQLGetDiagField**時,在語句句柄之外,使用SQL_DIAG_DYNAMIC_FUNCTION的*Diag 標識符*將返回SQL_ERROR。 在調用 SQLExecute 或**SQLExecDirect**之前**SQLExecDirect**,此欄位的值未定義。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|這是描述基礎函數執行的 SQL 語句的數位碼。 (有關特定值,請參閱本節後面的"動態函數位段的值"。此欄位的內容僅為語句句柄定義,並且僅在調用**SQLExecute、SQLExecDirect**或**SQLMore****SQLExecute**結果 後定義。 呼叫**SQLGetDiagField**時,在語句句柄之外,使用 SQL_DIAG_DYNAMIC_FUNCTION_CODE的*Diag 標識符*將返回SQL_ERROR。 在調用 SQLExecute 或**SQLExecDirect**之前**SQLExecDirect**,此欄位的值未定義。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可用於指定句柄的狀態記錄數。|  
|SQL_DIAG_RETURNCODE|SQL 傳回|返回函數返回的代碼。 有關退貨代碼的清單,請參閱[退貨代碼](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驅動程式不必實現SQL_DIAG_RETURNCODE;它始終由驅動程式管理器實現。 如果*句柄*上尚未調用任何函數,則SQL_DIAG_RETURNCODE將返回SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|受**SQLExecute、SQLExecDirect、SQLBulk****SQLExecute****操作**或**SQLSetPos**執行的插入、刪除或更新影響的行數。 在執行*遊標規範*后,它是驅動程式定義的。 此欄位的內容僅為語句句柄定義。 調用**SQLGetDiagField**時,在語句句柄之外,使用 SQL_DIAG_ROW_COUNT的*Diag 標識符*將返回SQL_ERROR。 此欄位中的數據也會在**SQLRowCount**的*RowCountPtr*參數中返回。 此欄位中的數據在每個非診斷函數調用後重置,而**SQLRowCount**返回的行計數保持不變,直到語句返回到已準備或分配的狀態。|  
  
## <a name="record-fields"></a>記錄欄位  
 下表中列出的記錄欄位可以包含在*DiagIdentifier*參數中。  
  
|診斷器識別碼|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR ||指示在此記錄中定義 SQLSTATE 值的類部分的文檔的字串。 其值為"ISO 9075",適用於開放組和 ISO 調用級介面定義的所有 SQLSTAT。 對於特定於 ODBC 的 SQLSTATEs(所有其 SQLSTATE 類為"IM"的 SQLSTATEs),其值為"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果SQL_DIAG_ROW_NUMBER欄位是行集中的有效行號或一組參數,則此欄位包含表示結果集中的列數的值或參數集中的參數編號。 結果集列數始終從 1 開始;結果集列數始終從 1 開始。如果此狀態記錄與書籤列相關,則該欄位可以為零。 參數編號從 1 開始。 如果狀態記錄未與列號或參數編號關聯,則具有值SQL_NO_COLUMN_NUMBER。 如果驅動程式無法確定此記錄關聯的列號或參數編號,則此欄位具有值SQL_COLUMN_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容僅為語句句柄定義。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR ||指示診斷記錄相關的連接名稱的字串。 此欄位是驅動程式定義的。 對於與環境句柄關聯的診斷數據結構以及與任何連接無關的診斷,此欄位為零長度字串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR ||有關錯誤或警告的資訊性消息。 此欄位的格式為[診斷消息](../../../odbc/reference/develop-app/diagnostic-messages.md)中所述。 診斷消息文本沒有最大長度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驅動程式/資料源特定的本機錯誤代碼。 如果沒有本機錯誤代碼,驅動程式返回 0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此欄位包含行集中的行號,或參數集中的參數編號,與狀態記錄關聯。 行號和參數編號以 1 開頭。 如果此狀態記錄未與行號或參數編號關聯,則此欄位具有值SQL_NO_ROW_NUMBER。 如果驅動程式無法確定此記錄關聯的行號或參數編號,則此欄位具有值SQL_ROW_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容僅為語句句柄定義。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR ||指示診斷記錄與之相關的伺服器名稱的字串。 它與使用SQL_DATA_SOURCE_NAME選項調用**SQLGetInfo**返回的值相同。 對於與環境句柄關聯的診斷數據結構以及與任何伺服器無關的診斷,此欄位為零長度字串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR ||五個字元的 SQLSTATE 診斷代碼。 有關詳細資訊,請參閱[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR ||具有與SQL_DIAG_CLASS_ORIGIN相同的格式和有效值的字串,用於識別 SQLSTATE 代碼子類部分的定義部分。 傳回「ODBC 3.0」的特定於 ODBC 的 SQLAA 包括以下內容:<br /><br /> 01S00、 01S01、 01S02、 01S06, 01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42S01、42S02、42S12、42S21、42S22、HY095、HY097、HY098、HY099、 HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM IM01、IM002、IM003、IM004、IM005、IM006、IM007、IM008、IM010、IM0111、IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動態函數字段的值  
 下表描述了適用於呼叫 SQLExecute 或**SQLExecDirect**執行的每種類型的 SQL 語句**SQLExecDirect**的SQL_DIAG_DYNAMIC_FUNCTION和SQL_DIAG_DYNAMIC_FUNCTION_CODE的值 。 驅動程式可以將驅動程式定義的值添加到列出的值。  
  
|SQL 陳述式<br /><br /> 執行| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*變更欄位句*|"ALTER 域"|SQL_DIAG_ALTER_DOMAIN|  
|*變更表語句*|"更改表"|SQL_DIAG_ALTER_TABLE|  
|*斷言定義*|"創建斷言"|SQL_DIAG_CREATE_ASSERTION|  
|*字元集定義*|"創建字元集"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*排序規則定義*|"創建排序規則"|SQL_DIAG_CREATE_COLLATION|  
|*網域定義*|"創建域"|SQL_DIAG_CREATE_DOMAIN|
|*建立索引敘述*|"創建索引"|SQL_DIAG_CREATE_INDEX|  
|*建立表語片*|"創建表"|SQL_DIAG_CREATE_TABLE|  
|*建立-檢視語句*|"創建視圖"|SQL_DIAG_CREATE_VIEW|  
|*游標規格*|選擇游標"|SQL_DIAG_SELECT_CURSOR|  
|*刪除敘述*|"動態刪除游標"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*刪除敘述搜尋*|"刪除位置"|SQL_DIAG_DELETE_WHERE|  
|*丟棄斷言語句*|"丟棄斷言"|SQL_DIAG_DROP_ASSERTION|  
|*放置字元集-stmt*|"丟棄字元集"|SQL_DIAG_DROP_CHARACTER_SET|  
|*丟棄排序規則語句*|"丟棄排序規則"|SQL_DIAG_DROP_COLLATION|  
|*刪除欄位句*|"DROP 域"|SQL_DIAG_DROP_DOMAIN|  
|*丟棄索引語句*|"下降指數"|SQL_DIAG_DROP_INDEX|  
|*刪除架構敘述*|"丟棄模式"|SQL_DIAG_DROP_SCHEMA|  
|*下放表語句*|"掉落表"|SQL_DIAG_DROP_TABLE|  
|*刪除翻譯語句*|"滴翻譯"|SQL_DIAG_DROP_TRANSLATION|  
|*放置檢視敘述*|"下降視圖"|SQL_DIAG_DROP_VIEW|  
|*贈款報表*|"格蘭特"|SQL_DIAG_GRANT|
|*插入敘述*|"插入"|SQL_DIAG_INSERT|  
|*ODBC-程式延伸*|"呼叫"|SQL_DIAG_呼叫|  
|*復原聲明*|"撤銷"|SQL_DIAG_REVOKE|  
|*架構定義*|"創建架構"|SQL_DIAG_CREATE_SCHEMA|  
|*翻譯定義*|"創建翻譯"|SQL_DIAG_CREATE_TRANSLATION|  
|*更新敘述*|"動態更新游標"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*更新敘述搜尋*|"更新位置"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空字串*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>狀態記錄的順序

 狀態記錄根據行號和診斷類型按順序定位。 驅動程式管理員確定返回它生成的狀態記錄的最終順序。 驅動程序確定返回其生成的狀態記錄的最終順序。  
  
 如果診斷記錄由駕駛員經理和驅動程式過帳,則駕駛員經理負責訂購。  
  
 如果有兩個或多個狀態記錄,則記錄的順序首先由行號確定。 以下規則適用於按行確定診斷紀錄的順序:  
  
-   不對應於任何行的記錄將顯示在對應於特定行的記錄前面,因為SQL_NO_ROW_NUMBER定義為 -1。  
  
-   行號未知的記錄顯示在所有其他記錄的前面,因為SQL_ROW_NUMBER_UNKNOWN定義為 -2。  
  
-   對於與特定行相關的所有記錄,記錄按SQL_DIAG_ROW_NUMBER欄位中的值排序。 列出受影響的第一行的所有錯誤和警告,然後列出受影響的下一行的所有錯誤和警告,等等。  
  
> [!NOTE]
>  如果 SQLSTATE 01S01(行中的錯誤)由 ODBC 2 *.x*驅動程式返回,或者在調用**SQLExtendedFetch**時由 ODBC 3 .x 驅動程式傳回 SQLSTATE 01S01(行中的錯誤 **),則**ODBC 3 *.x*驅動程式管理器不會在診斷佇列中訂購狀態**記錄。** * *  
  
 在每行中,或對於與行不對應或行號未知的所有記錄,或者對於行號等於SQL_NO_ROW_NUMBER的所有記錄,使用一組排序規則確定列出的第一個記錄。 在第一條記錄之後,影響行的其他記錄的順序未定義。 應用程式不能假定錯誤在第一條記錄之後的警告之前。 應用程式應掃描完整的診斷數據結構,以獲取有關對函數調用不成功的完整資訊。  
  
 以下規則用於確定行中的第一個記錄。 排名最高的記錄是第一條記錄。 在排名記錄時,不考慮記錄的來源(驅動程式管理器、驅動程式、閘道等)。  
  
-   **錯誤**描述錯誤的狀態記錄的排名最高。 以下規則套用於錯誤進行排序:  
  
    -   指示事務失敗或可能事務失敗的記錄比所有其他記錄都多。  
  
    -   如果兩個或多個記錄描述相同的錯誤條件,則由開放組 CLI 規範定義的 SQLSTAT(類 03 到 HZ)比 ODBC 和驅動程式定義的 SQLSTATEs 高。  
  
-   **設定定義的無資料值**描述驅動程式定義的無資料值(類 02)的狀態記錄具有第二高的排名。  
  
-   **警告**描述警告的狀態記錄(類 01)的排名最低。 如果兩個或多個記錄描述相同的警告條件,則警告由開放組 CLI 規範定義的 SQLSTAT 比 ODBC 定義和驅動程式定義的 SQLSTATEs 高。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷資料結構的多個字段|[SQLGetDiagRec 函式](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
