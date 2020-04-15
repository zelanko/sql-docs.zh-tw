---
title: 使用參數陣列 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306799"
---
# <a name="using-arrays-of-parameters"></a>使用參數陣列
要使用參數陣列,應用程式將**SQLSetStmtAttr**調用*屬性參數為*SQL_ATTR_PARAMSET_SIZE,以指定參數集的數量。 它調用**SQLSetStmtAttr,***屬性*參數為 SQL_ATTR_PARAMS_PROCESSED_PTR,以指定變數的位址,其中驅動程式可以返回處理的參數集數,包括錯誤集。 它調用**SQLSetStmtAttr,***屬性參數為*SQL_ATTR_PARAM_STATUS_PTR,以指向一個陣列,其中返回每行參數值的狀態資訊。 驅動程式將這些位址存儲在它為語句維護的結構中。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*調用**SQLParamOptions**來為參數指定多個值。 在 ODBC 3 中。*x*,對**SQLParamOptions 的**調用已替換為對**SQLSetStmtAttr**的調用,以設置SQL_ATTR_PARAMSET_SIZE和SQL_ATTR_PARAMS_PROCESSED_ARRAY屬性。  
  
 在執行語句之前,應用程式設置每個綁定陣列的每個元素的值。 執行語句時,驅動程式使用它存儲的資訊來檢索參數值並將其發送到數據源;如果可能,驅動程式應將這些值作為陣列發送。 儘管參數陣列的使用最好通過執行 SQL 語句與陣列中的所有參數執行,對數據源進行單個調用,但此功能在 DBMS 中目前並不廣泛可用。 但是,驅動程式可以通過多次執行 SQL 語句來類比它,每個語句都使用一組參數。  
  
 在應用程式使用參數陣列之前,必須確保應用程式使用的驅動程式支援它們。 作法有二：  
  
-   僅使用已知支援參數陣列的驅動程式。 應用程式可以對這些驅動程式的名稱進行硬編碼,也可以指示使用者僅使用這些驅動程式。 自定義應用程式和垂直應用程式通常使用一組有限的驅動程式。  
  
-   檢查在運行時對參數陣列的支援。 如果可以將SQL_ATTR_PARAMSET_SIZE語句屬性設置為大於 1 的值,則驅動程式支援參數陣列。 通用應用程式和垂直應用程式通常在運行時檢查參數陣列的支援。  
  
 可以通過使用SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS選項調用**SQLGetInfo**來確定參數化執行中的行計數和結果集的可用性。 對於**INSERT、****更新**和**刪除**語句,SQL_PARAM_ARRAY_ROW_COUNTS 選項指示單個行計數(每個參數集一個)是否可用(SQL_PARC_BATCH),還是將行計數匯總為一個(SQL_PARC_NO_BATCH)。 對於**SELECT**語句,SQL_PARAM_ARRAY_SELECTS 選項指示結果集是否可用於每組參數(SQL_PAS_BATCH),還是只有一個結果集可用(SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列執行結果集生成語句,則SQL_PARAM_ARRAY_SELECTS返回SQL_PAS_NO_SELECT。 參數陣列是否可以與其他類型的語句一起使用,這是特定於數據源的,特別是因為在這些語句中使用參數是特定於數據源的,並且不會遵循 ODBC SQL 語法。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 語句屬性指向的陣列可用於忽略參數行。 如果陣列的元素設置為SQL_PARAM_IGNORE,則與該元素對應的參數集將從 SQLExecute 或**SQLExecDirect**調用中**SQLExecDirect**排除。 SQL_ATTR_PARAM_OPERATION_PTR屬性指向的陣列由應用程式分配和填充並由驅動程式讀取。 如果提取的行用作輸入參數,則行狀態陣列的值可以在參數操作陣列中使用。  
  
## <a name="error-processing"></a>錯誤處理  
 如果在執行語句時發生錯誤,執行函數將返回一個錯誤,並將行號變數設置為包含錯誤的行數。 它是特定於數據源的,無論是執行除錯誤集之外的所有行,還是執行錯誤集之前(但不是之後)之前的所有行。 由於驅動程式處理參數集,因此驅動程式將SQL_ATTR_PARAMS_PROCESSED_PTR語句屬性指定的緩衝區設置為當前正在處理的行數。 如果執行除錯誤集之外的所有集,則驅動程式將此緩衝區設置為處理所有行后SQL_ATTR_PARAMSET_SIZE。  
  
 如果設置了SQL_ATTR_PARAM_STATUS_PTR語句屬性 **,SQLExecute**或**SQLExecDirect**將返回*參數狀態陣列,該陣列*提供每組參數的狀態。 參數狀態數組由應用程式分配並由驅動程式填充。 其元素指示 SQL 語句是否已成功執行參數行,或者在處理參數集時是否發生錯誤。 如果發生錯誤,驅動程式將參數狀態陣列中的相應值設置為SQL_PARAM_ERROR並返回SQL_SUCCESS_WITH_INFO。 應用程式可以檢查狀態陣列以確定已處理的行。 使用行號,應用程式通常可以更正錯誤並恢復處理。  
  
 參數狀態陣列的使用方式由調用**SQLGetInfo**傳回SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS選項決定。 對於**INSERT、****更新**和**刪除**語句,如果為SQL_PARAM_ARRAY_ROW_COUNTS返回SQL_PARC_BATCH,則參數狀態陣列將填充狀態資訊,但如果返回SQL_PARC_NO_BATCH則不填寫。 對於**SELECT**語句,如果返回SQL_PAS_BATCHSQL_PARAM_ARRAY_SELECT,則填充參數狀態陣列,但如果返回SQL_PAS_NO_BATCH或SQL_PAS_NO_SELECT則不填寫參數狀態陣列。  
  
## <a name="data-at-execution-parameters"></a>執行時的資料參數  
 如果長度/指示器陣列中的任何值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC(*長度*) 宏的結果,則這些值的數據將通常隨**SQLPutData**一起發送。 這一進程的以下方面有特別的評論,因為它們並不十分明顯:  
  
-   當驅動程式返回SQL_NEED_DATA時,它必須將行號變數的位址設置為需要數據的行。 與單值情況一樣,應用程式不能對驅動程式在單個參數集中請求參數值的順序進行任何假設。 如果在執行執行數據時發生數據執行參數時發生錯誤,SQL_ATTR_PARAMS_PROCESSED_PTR語句屬性指定的緩衝區將設置為發生錯誤的行數,SQL_ATTR_PARAM_STATUS_PTR語句屬性指定的行狀態陣列中行的狀態設置為SQL_PARAM_ERROR,對 SQLExecute、SQLExecDirect、SQLParamData 或**SQLPutData**的調用**SQLExecute****SQLExecDirect****SQLParamData**將返回SQL_ERROR。 如果**SQLExecute、SQLExecDirect****SQLExecute**或**SQLParamData**返回SQL_STILL_EXECUTING,則此緩衝區的內容將未定義。  
  
-   由於驅動程式不解釋**SQLBind 參數**的*參數中*用於執行時資料參數的值,因此,如果應用程式提供指向陣列的指標,**則 SQLParamData**不會提取此陣列的元素並將其傳回給應用程式。 相反,它返回應用程式提供的標量值。 這意味著**SQLParamData**傳回的值不足以指定應用程式需要發送數據的參數;應用程式還需要考慮當前行號。  
  
     當參數陣列的某些元素是執行時的數據參數時,應用程式必須通過*參數ValuePtr*中包含所有參數元素的陣列的位址。 此陣列對於不是執行時的數據參數進行正常解釋。 對於執行時的數據參數 **,SQLParamData**向應用程式提供的值始終是陣列的位址,該值通常可用於標識驅動程式此時請求的數據。
