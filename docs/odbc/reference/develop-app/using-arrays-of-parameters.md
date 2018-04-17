---
title: 使用參數陣列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acdcf9e1c21773240c03204608f73a4d2174fba5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-arrays-of-parameters"></a>使用參數陣列
若要使用的應用程式會呼叫的參數陣列**SQLSetStmtAttr**與*屬性*則 sql_attr_paramset_size 會以指定的參數集數目的引數。 它會呼叫**SQLSetStmtAttr**與*屬性*SQL_ATTR_PARAMS_PROCESSED_PTR 以指定的位址變數中的驅動程式可以傳回的處理，參數的集合數目的引數包括錯誤設定。 它會呼叫**SQLSetStmtAttr**與*屬性*SQL_ATTR_PARAM_STATUS_PTR 指向用來傳回每個資料列的參數值的狀態資訊的陣列的引數。 驅動程式會將這些位址儲存在它所維護的陳述式的結構。  
  
> [!NOTE]  
>  在 ODBC 2。*x*， **SQLParamOptions**呼叫來指定多個參數的值。 在 ODBC 3。*x*，呼叫**SQLParamOptions**已由呼叫取代**SQLSetStmtAttr**設定則 sql_attr_paramset_size 會和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 屬性.  
  
 再執行陳述式，應用程式會設定每個繫結陣列的每個元素的值。 當執行陳述式時，驅動程式會使用擷取參數值，並將它們傳送至資料來源，儲存的資訊可能的話，驅動程式應該傳送這些值做為陣列。 雖然參數陣列使用最佳實作陣列所使用的資料來源的單一呼叫中執行的所有參數的 SQL 陳述式中，這項功能不廣泛適用於 Dbms 今天。 不過，驅動程式即可模擬它執行 SQL 陳述式多次，每個都有單一參數集。  
  
 應用程式使用的參數陣列之前，必須確定它們支援的應用程式所使用的驅動程式。 有兩種方式可以執行此動作：  
  
-   使用僅已知支援的參數陣列的驅動程式。 應用程式可以硬式編碼的名稱，這些驅動程式，或指示使用者可以使用這些驅動程式。 自訂應用程式和垂直應用程式通常使用一組有限的驅動程式。  
  
-   在執行階段檢查的參數陣列的支援。 最好是盡可能設 SQL_ATTR_PARAMSET_SIZE 陳述式屬性的值大於 1，驅動程式支援參數的陣列。 泛型應用程式和垂直應用程式通常檢查支援的參數陣列在執行階段。  
  
 您可以判斷資料列計數和在執行中參數化的結果集的可用性，藉由呼叫**SQLGetInfo**與 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 如**插入**，**更新**，和**刪除**陳述式，SQL_PARAM_ARRAY_ROW_COUNTS 選項指出是否要為個別的資料列計數 （一個用於每個參數集）可用 (SQL_PARC_BATCH) 或資料列計數是否會彙總到一個 (SQL_PARC_NO_BATCH)。 如**選取**陳述式，SQL_PARAM_ARRAY_SELECTS 選項指出結果集是否可供每個參數 (SQL_PAS_BATCH) 集，或者只有一個結果集是否為可用 (SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列來執行的結果集 – 產生陳述式，SQL_PARAM_ARRAY_SELECTS 傳回 SQL_PAS_NO_SELECT。 是否能夠使用參數陣列與其他類型的陳述式，尤其是因為使用這些陳述式中的參數會是資料來源專用並不會遵循 ODBC SQL 文法，它可以是資料來源專用。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 陳述式屬性所指陣列可用來忽略的參數資料列。 如果陣列項目設定為 SQL_PARAM_IGNORE，排除一組參數對應至該項目**SQLExecute**或**SQLExecDirect**呼叫。 配置和填入應用程式和驅動程式讀取 SQL_ATTR_PARAM_OPERATION_PTR 屬性所指陣列。 如果擷取的資料列會當做輸入參數，資料列狀態陣列的值可以使用參數作業陣列中。  
  
## <a name="error-processing"></a>錯誤處理  
 如果執行陳述式時發生錯誤，執行函式會傳回錯誤，且資料列數字變數設定為包含錯誤的資料列數。 是否所有資料列除了錯誤組執行或所有資料列之前 （但不是能晚於） 是否會執行設定 「 錯誤時，它可以是資料來源專用。 因為它處理集合參數時，驅動程式會設定目前正在處理的資料列數 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性所指定的緩衝區。 如果所有將除了執行設定 「 錯誤時，驅動程式將這個緩衝區則 sql_attr_paramset_size 會處理所有資料列之後。  
  
 如果已設定 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性， **SQLExecute**或**SQLExecDirect**傳回*參數狀態陣列，*這樣會提供狀態每個參數集。 參數狀態陣列是由應用程式配置，並填入的驅動程式。 其項目會指出是否在 SQL 陳述式執行成功的參數資料列，或是否處理時發生錯誤的參數集。 如果發生錯誤，驅動程式 SQL_PARAM_ERROR 參數狀態陣列中設定對應的值，並傳回 SQL_SUCCESS_WITH_INFO。 應用程式可以檢查狀態陣列來判斷哪些資料列已處理。 使用資料列號碼，應用程式可以通常更正錯誤並繼續處理。  
  
 如何使用參數狀態陣列由呼叫所傳回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項**SQLGetInfo**。 如**插入**，**更新**，和**刪除**陳述式，參數狀態陣列填入狀態資訊，如果針對 SQL_PARAM_ARRAY_ 傳回 SQL_PARC_BATCHROW_COUNTS，但不是如果 SQL_PARC_NO_BATCH 傳回。 如**選取**陳述式，參數狀態陣列會自動填入如果 SQL_PAS_BATCH 就會傳回 SQL_PARAM_ARRAY_SELECT，但未傳回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT。  
  
## <a name="data-at-execution-parameters"></a>資料在執行中參數  
 如果任何長度/指標陣列中的值為 SQL_DATA_AT_EXEC 或結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，這些值的資料傳送與**SQLPutData**以一般方式。 此程序的下列層面用戶須自行特殊的註解，因為它們不是明顯：  
  
-   當驅動程式會傳回 SQL_NEED_DATA 時，它必須將資料列數字變數的位址設定，它需要資料的資料列。 如同的單一值的情況，應用程式無法對任何假設所在驅動程式會要求單一參數集內的參數值的順序。 如果資料在執行中參數的執行中發生錯誤，SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性所指定的緩衝區會設定為在發生錯誤，所指定之資料列狀態陣列中的資料列的狀態的資料列數SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性設定為 SQL_PARAM_ERROR，且呼叫**SQLExecute**， **SQLExecDirect**， **SQLParamData**，或**SQLPutData**會傳回 SQL_ERROR。 如果這個緩衝區的內容會有未定義**SQLExecute**， **SQLExecDirect**，或**SQLParamData**傳回 SQL_STILL_EXECUTING。  
  
-   驅動程式不會解譯中的值因為*ParameterValuePtr*引數的**SQLBindParameter**資料在執行中參數，如果應用程式提供的指標陣列，如**SQLParamData**不擷取，這個陣列的項目並返回應用程式。 相反地，它會傳回純量值的應用程式有提供。 這表示所傳回的值**SQLParamData**足夠的參數指定的應用程式需要將資料傳送; 應用程式也需要考慮目前的資料列數目。  
  
     當只有一些參數陣列的項目資料在執行中參數，應用程式必須傳遞陣列中的位址*ParameterValuePtr* ，其中包含所有參數的項目。 這個陣列會被解譯通常不是資料在執行中參數的參數。 資料在執行參數值的**SQLParamData**提供給應用程式，通常無法用來識別驅動程式會要求在這個下的資料，一律為陣列的位址。
