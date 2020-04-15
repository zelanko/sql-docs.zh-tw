---
title: SQLMore 結果函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304739"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLMore結果**確定在包含**SELECT、UPDATE、****插入**或**SELECT** **DELETE**語句的語句上是否提供更多結果,如果是,則初始化這些結果的處理。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLMore 結果**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的**句柄*。 下表列出了**SQLMore 結果**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|處理批處理時,語句屬性的值已更改。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 **SQLMore結果**函數被呼叫,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**調用了*敘述的句柄*。 然後在*語句句柄*上再次調用**SQLMore 結果**函數。<br /><br /> **SQLMore結果**函數被呼叫,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**從多線程式中的不同線程調用了*語句處理*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLMore 結果**函數時,此異步函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **選擇**語句返回結果集。 **更新**、**插入**與**刪除**敘述傳回受影響的行的計數。 如果對這些語句中的任何一個進行批處理,並且使用參數陣列(按增加參數順序編號、按批處理中顯示的順序)或過程中提交,它們可以返回多個結果集或行計數。 有關參數的敘述與陣列的批次處理的資訊,請參閱 SQL[語句的批次處理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)與[參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 執行批處理後,應用程式將定位在第一個結果集中。 該應用程式可以在第一個或任何後續結果集中調用**SQLBindCol、SQLBulk****操作**、SQLFetch、SQLGetData、SQLFetchScroll、SQLSetPos 和所有元數據函數,就像只有單個結果**SQLFetch****SQLGetData****SQLFetchScroll****SQLSetPos**集一樣。 使用第一個結果集完成後,應用程式將調用**SQLMoreResult**移動到下一個結果集。 如果另一個結果集或計數可用 **,SQLMoreResult**將返回SQL_SUCCESS並初始化結果集或計數以進行其他處理。 如果任何行計數生成語句出現在結果集生成語句之間,則可以通過調用**SQLMoreResult**來逐步結束這些語句。呼叫**SQLMore 結果**進行**更新**、**插入**或**移除**敘述後,應用程式可以呼叫**SQLRowCount**。  
  
 如果存在當前結果集,其中行未提取 **,SQLMoreResult**將丟棄該結果集,並使下一個結果集或計數可用。 如果處理了所有結果 **,SQLMore 結果**將返回SQL_NO_DATA。 對於某些驅動程式,在處理了所有結果集和行計數之前,輸出參數和返回值不可用。 對於此類驅動程式,當**SQLMore 結果**返回SQL_NO_DATA時,輸出參數和返回值將可用。  
  
 為上一個結果集建立的任何綁定仍然有效。 如果此結果集的列結構不同,則調用**SQLFetch**或**SQLFetchScroll**可能會導致錯誤或截斷。 為了防止這種情況,應用程式必須調用**SQLBindCol**以根據需要顯式重新綁定(或者通過設置描述符欄位來執行此操作)。 或者,應用程式可以使用SQL_UNBIND*選項*調用**SQLFreeStmt**以取消綁定所有列緩衝區。  
  
 語句屬性的值(如游標類型、游標併發、鍵集大小或最大長度)可能會隨著應用程式通過調用**SQLMore 結果**在批處理中導航而更改。 如果發生這種情況 **,SQLMore結果**將返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02(選項值已更改)。  
  
 調用**SQLCloseCursor**或*Option***SQLFreeStmt**的選項SQL_CLOSE,將丟棄執行批次處理後可用的所有結果集和行計數。 語句句柄返回到已分配或準備的狀態。 調用**SQLCancel**以在已執行批處理且語句句柄處於執行、游標定位或異步狀態時取消非同步執行功能,這將導致在取消調用成功時丟棄的批次處理生成的所有結果集和行計數。 然後,語句返回到已準備或分配的狀態。  
  
 如果一批語句或過程將其他 SQL 語句與**SELECT、****更新**,**插入**與**DELETE**語句混合在一起,則這些其他語句不會影響**SQLMore 結果**。  
  
 有關詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜索的更新、插入或刪除一批語句中的語句不會影響數據源中的任何行 **,SQLMore結果**將返回SQL_SUCCESS。 這與透過**SQLExecDirect、SQLExecute**或**SQLParamData**執行的搜尋更新**SQLExecute**、插入或刪除語句的情況不同,如果該語句不影響數據來源上的任何行,則返回SQL_NO_DATA。 如果應用程式調用**SQLRowCount**以檢索對**SQLMore 結果**的調用後檢索行計數,則**SQLRowCount**將返回SQL_NO_DATA。  
  
 有關結果處理函數的有效排序的其他資訊,請參閱[附錄 B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有關SQL_PARAM_DATA_AVAILABLE和串流式輸出參數的詳細資訊,請參閱使用[SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>行計數可用性  
 當批處理包含多個連續行計數生成語句時,這些行計數可能僅匯總到一行計數中。 例如,如果批處理有五個插入語句,則某些數據源能夠返回五個單獨的行計數。 某些其他數據源僅返回一個表示五個單獨行計數總和的行計數。  
  
 當批處理包含結果集生成語句和行計數生成語句的組合時,行計數可能根本不可用,也可能不可用。 驅動程式在行計數可用性方面的行為在通過調用**SQLGetInfo**提供的SQL_BATCH_ROW_COUNT資訊類型中枚舉。 例如,假設批次處理包含**SELECT**,後跟兩個**INSERT**和另一個**SELECT**。 然後,以下情況是可能的:  
  
-   與兩個**INSERT**語句對應的行計數根本不可用。 對**SQLMore 結果**的第一次調用將您定位在第二個**SELECT**語句的結果集中。  
  
-   對應於兩個**INSERT**語句的行計數單獨可用。 (對**SQLGetInfo**的呼叫不會返回SQL_BATCH_ROW_COUNT資訊類型的SQL_BRC_ROLLED_UP位。對**SQLMore 結果**的第一個調用將定位您在第一個**INSERT**的行計數上,第二個調用將您定位在第二個**INSERT**的行計數上。 對**SQLMore 結果**的第三次調用將定位您在第二個**SELECT**語句的結果集中。  
  
-   對應於兩個**INSERT 的**行計數將匯總為一個可用的行計數。 (對**SQLGetInfo**的呼叫返回SQL_BATCH_ROW_COUNT資訊類型的SQL_BRC_ROLLED_UP位。對**SQLMore 結果**的第一個調用將您定位在匯總行計數上,而對**SQLMore 結果**的第二個調用將您定位在第二個**SELECT**的結果集中。  
  
 某些驅動程式使行計數僅適用於顯式批處理,而不適用於存儲過程。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料欄的一部份或全部|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
