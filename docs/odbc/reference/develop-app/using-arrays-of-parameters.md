---
title: 使用參數陣列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf6b5127bac7aedf9e67918d38020c73a4afe186
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079605"
---
# <a name="using-arrays-of-parameters"></a>使用參數陣列
若要使用的應用程式會呼叫的參數陣列**SQLSetStmtAttr**具有*屬性*則 sql_attr_paramset_size 會以指定的參數集數目的引數。 它會呼叫**SQLSetStmtAttr**具有*屬性*SQL_ATTR_PARAMS_PROCESSED_PTR 指定變數的位址中驅動程式可傳回的處理，參數集數目的引數包括錯誤設定。 它會呼叫**SQLSetStmtAttr**具有*屬性*SQL_ATTR_PARAM_STATUS_PTR 指向用來傳回每個資料列的參數值的狀態資訊的陣列引數。 驅動程式會儲存在結構中的陳述式會維護這些位址。  
  
> [!NOTE]  
>  在 ODBC 2。*x*， **SQLParamOptions**呼叫來指定多個參數的值。 在 ODBC 3。*x*，來呼叫**SQLParamOptions**已取代呼叫**SQLSetStmtAttr**設定則 sql_attr_paramset_size 會和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 屬性.  
  
 然後再執行陳述式，應用程式會設定每個繫結陣列的每個元素的值。 當執行陳述式時，驅動程式會使用它來擷取參數值，並將它們傳送至資料來源所儲存的資訊可能的話，驅動程式應該傳送這些值做為陣列。 雖然使用參數陣列的最佳實作陣列與資料來源的單一呼叫中執行的所有參數的 SQL 陳述式中，這項功能目前不廣泛適用於 Dbms。 不過，驅動程式可以模擬它執行 SQL 陳述式多次，每個都具有單一參數集。  
  
 應用程式使用的參數陣列之前，必須確定它們受到應用程式所使用的驅動程式。 有兩種方式可以執行此動作：  
  
-   只要使用驅動程式已知能支援的參數陣列。 應用程式可以硬式編碼的名稱，這些驅動程式，或指示使用者可以使用這些驅動程式。 自訂應用程式和垂直應用程式通常使用一組有限的驅動程式。  
  
-   在執行階段檢查的參數陣列的支援。 如果可將 SQL_ATTR_PARAMSET_SIZE 陳述式屬性的值大於 1，驅動程式將支援參數陣列。 泛型應用程式和垂直應用程式常用的參數陣列的支援在執行階段檢查。  
  
 您可以藉由呼叫判斷資料列計數和參數化的執行中的結果集的可用性**SQLGetInfo**使用 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 針對**插入**，**更新**，並**刪除**陳述式，SQL_PARAM_ARRAY_ROW_COUNTS 選項指出是否要為個別的資料列計數 （一個用於每個參數集）可用 (SQL_PARC_BATCH) 或資料列的計數是否會彙總到一個 (SQL_PARC_NO_BATCH)。 針對**選取**陳述式，SQL_PARAM_ARRAY_SELECTS 選項會指出結果集是否可用於每個參數 (SQL_PAS_BATCH) 集，或只有一個結果集是否可用 (SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列來執行的結果集產生陳述式，SQL_PARAM_ARRAY_SELECTS 傳回 SQL_PAS_NO_SELECT。 是否可以與其他類型的陳述式，使用參數陣列，特別是因為使用這些陳述式中的參數會是資料來源特有的且會遵循 ODBC SQL 文法，這是來源特有的資料。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 陳述式屬性所指陣列可用來忽略的參數資料列。 若陣列項目設定為 SQL_PARAM_IGNORE，一組參數對應至該項目會從排除**SQLExecute**或是**SQLExecDirect**呼叫。 配置及填入應用程式和驅動程式讀取 SQL_ATTR_PARAM_OPERATION_PTR 屬性所指陣列。 如果擷取的資料列做為輸入參數，值的資料列狀態陣列可用參數作業陣列中。  
  
## <a name="error-processing"></a>錯誤處理  
 如果在執行陳述式時發生錯誤，執行函式會傳回錯誤，並將資料列數的變數設定為包含錯誤的資料列數目。 是否所有資料列只不過執行設定 「 錯誤時，或設定 「 錯誤時是否所有資料列 （但不是能晚於） 之前執行，它就會是資料來源特有。 因為它處理的參數集時，驅動程式會設定目前正在處理的資料列數目 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性所指定的緩衝區。 如果所有設定除了執行設定 「 錯誤時，驅動程式將設定這個緩衝區則 sql_attr_paramset_size 會處理所有資料列之後。  
  
 如果尚未設定 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性， **SQLExecute**或是**SQLExecDirect**會傳回*參數狀態陣列，* 其中提供的狀態每個參數集。 參數狀態陣列是由應用程式配置，並填入驅動程式。 其項目會指出是否 SQL 陳述式執行成功的參數資料列，或是否正在處理的參數集時，發生錯誤。 發生錯誤時，驅動程式 SQL_PARAM_ERROR 參數狀態陣列中設定對應的值，並傳回 SQL_SUCCESS_WITH_INFO。 應用程式可以檢查狀態陣列來判斷哪些資料列已處理。 使用資料列數目，應用程式可以經常更正錯誤並繼續處理。  
  
 使用參數狀態陣列的方式取決於呼叫所傳回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項**SQLGetInfo**。 針對**插入**，**更新**，並**刪除**陳述式，參數狀態陣列填入狀態資訊，如果 SQL_PARC_BATCH 會傳回 SQL_PARAM_ARRAY_ROW_COUNTS，但如果 SQL_PARC_NO_BATCH 會傳回。 針對**選取**陳述式，參數狀態陣列填入如果 SQL_PAS_BATCH 會傳回 SQL_PARAM_ARRAY_SELECT，但不是會傳回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT。  
  
## <a name="data-at-execution-parameters"></a>資料在執行中參數  
 如果任何長度/指標陣列中的值為 SQL_DATA_AT_EXEC 或結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集，這些值的資料會傳送具有**SQLPutData**以一般方式。 此程序的下列層面請特殊註解，因為它們不是明顯：  
  
-   當驅動程式會傳回 SQL_NEED_DATA 時，它必須設定資料列數字變數的位址，它需要資料的資料列。 如所示的單一值的情況下，應用程式不能做出任何假設驅動程式會在其中要求單一參數集內的參數值的順序。 如果資料在執行中參數的執行中發生錯誤，SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性所指定的緩衝區會設定為在其發生錯誤，所指定之資料列狀態陣列中的資料列的狀態資料列數目SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性設定為 SQL_PARAM_ERROR 和呼叫**SQLExecute**， **SQLExecDirect**， **SQLParamData**，或**SQLPutData**會傳回 SQL_ERROR。 如果未定義此緩衝區的內容，則**SQLExecute**， **SQLExecDirect**，或**SQLParamData**傳回 SQL_STILL_EXECUTING。  
  
-   因為此驅動程式不會解譯中的值*ParameterValuePtr*引數**SQLBindParameter**資料在執行中參數，如果應用程式提供的指標陣列，如**SQLParamData**不擷取並傳回此陣列項目的應用程式。 相反地，它會傳回純量值的應用程式有提供。 這表示所傳回的值**SQLParamData**才會不足以指定參數為其應用程式需要將資料傳送，應用程式也需要考慮目前的資料列數目。  
  
     當只有一些參數陣列的項目是資料在執行中參數時，應用程式必須通過陣列中的地址*ParameterValuePtr*其中包含所有參數的項目。 這個陣列會被解譯通常不是資料在執行中參數的參數。 資料在執行參數值， **SQLParamData**提供給應用程式，通常無法用來識別資料驅動程式會要求在此情況下，一律為陣列的位址。
