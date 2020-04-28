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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306799"
---
# <a name="using-arrays-of-parameters"></a>使用參數陣列
若要使用參數陣列，應用程式會使用 SQL_ATTR_PARAMSET_SIZE 的*屬性*引數來呼叫**SQLSetStmtAttr** ，以指定參數集的數目。 它會使用 SQL_ATTR_PARAMS_PROCESSED_PTR 的*屬性*引數來呼叫**SQLSetStmtAttr** ，以指定變數的位址，而驅動程式可以在其中傳回已處理的參數集數目，包括錯誤集合。 它會使用 SQL_ATTR_PARAM_STATUS_PTR 的*屬性*引數來呼叫**SQLSetStmtAttr** ，以指向要在其中傳回每個參數值資料列之狀態資訊的陣列。 驅動程式會將這些位址儲存在它為語句維護的結構中。  
  
> [!NOTE]  
>  在 ODBC 2 中。已呼叫*x*， **SQLParamOptions**為參數指定多個值。 在 ODBC 3 中。*x*，對**SQLParamOptions**的呼叫已被**SQLSetStmtAttr**的呼叫所取代，以設定 SQL_ATTR_PARAMSET_SIZE 和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 屬性。  
  
 在執行語句之前，應用程式會設定每個系結陣列的每個元素的值。 執行語句時，驅動程式會使用它所儲存的資訊來抓取參數值，並將它們傳送至資料來源。可能的話，驅動程式應該將這些值當做陣列來傳送。 雖然使用參數陣列的最佳做法，是藉由對資料來源的單一呼叫執行包含陣列中所有參數的 SQL 語句，這項功能目前不會在 Dbms 中廣泛提供。 不過，驅動程式可以藉由多次執行 SQL 語句來模擬它，每個都有一組參數。  
  
 在應用程式使用參數陣列之前，必須先確定應用程式所使用的驅動程式支援它們。 作法有二：  
  
-   僅使用已知支援參數陣列的驅動程式。 應用程式可以將這些驅動程式的名稱硬式編碼，或指示使用者只使用這些驅動程式。 自訂應用程式和垂直應用程式通常會使用一組有限的驅動程式。  
  
-   檢查執行時間的參數陣列支援。 如果可以將 SQL_ATTR_PARAMSET_SIZE 語句屬性設定為大於1的值，則驅動程式支援參數的陣列。 一般應用程式和垂直應用程式通常會在執行時間檢查參數陣列的支援。  
  
 在參數化執行中，資料列計數和結果集的可用性可以藉由使用 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項來呼叫**SQLGetInfo**來判斷。 針對**INSERT**、 **UPDATE**和**DELETE**語句，SQL_PARAM_ARRAY_ROW_COUNTS 選項會指出個別資料列計數（每個參數集一個）是否可用（SQL_PARC_BATCH），或資料列計數是否匯總成一個（SQL_PARC_NO_BATCH）。 對於**SELECT**語句，SQL_PARAM_ARRAY_SELECTS 選項會指出每一組參數（SQL_PAS_BATCH）是否有可用的結果集，或是否只有一個可用的結果集（SQL_PAS_NO_BATCH）。 如果驅動程式不允許以參數陣列執行結果集產生的語句，SQL_PARAM_ARRAY_SELECTS 會傳回 SQL_PAS_NO_SELECT。 它是特定資料來源，不論參數陣列是否可以搭配其他類型的語句使用，尤其是因為在這些語句中使用參數會是資料來源特有的，而且不會遵循 ODBC SQL 文法。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 語句屬性所指向的陣列可以用來忽略參數的資料列。 如果陣列的元素設定為 SQL_PARAM_IGNORE，則會從**SQLExecute**或**SQLExecDirect**呼叫中排除對應至該元素的參數集合。 由應用程式佈建並填入 SQL_ATTR_PARAM_OPERATION_PTR 屬性所指向的陣列，並由驅動程式讀取。 如果將提取的資料列當做輸入參數使用，則可以在參數作業陣列中使用資料列狀態陣列的值。  
  
## <a name="error-processing"></a>錯誤處理  
 如果在執行語句時發生錯誤，執行函數會傳回錯誤，並將資料列編號變數設定為包含錯誤的資料列數目。 不論是否執行錯誤集以外的所有資料列，或是否執行錯誤集之前的所有資料列（但不是之後），它都是資料來源特有的。 由於它會處理參數集，因此驅動程式會將 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性所指定的緩衝區設定為目前正在處理的資料列數目。 如果已執行除了錯誤集以外的所有集合，驅動程式會在處理所有資料列之後，將此緩衝區設定為 SQL_ATTR_PARAMSET_SIZE。  
  
 如果已設定 SQL_ATTR_PARAM_STATUS_PTR 語句屬性， **SQLExecute**或**SQLExecDirect**會傳回*參數狀態陣列，* 它會提供每個參數集的狀態。 參數狀態陣列是由應用程式佈建，並由驅動程式填入。 其元素會指出 SQL 語句是否已針對參數的資料列成功執行，或在處理參數集時是否發生錯誤。 如果發生錯誤，驅動程式會將參數狀態陣列中對應的值設定為 SQL_PARAM_ERROR 並傳回 SQL_SUCCESS_WITH_INFO。 應用程式可以檢查狀態陣列，以判斷哪些資料列已處理。 使用資料列編號，應用程式通常可以更正錯誤並繼續處理。  
  
 參數狀態陣列的使用方式取決於**SQLGetInfo**的呼叫所傳回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 針對**INSERT**、 **UPDATE**和**DELETE**語句，如果 SQL_PARAM_ARRAY_ROW_COUNTS 傳回 SQL_PARC_BATCH，參數狀態陣列就會填入狀態資訊，但如果傳回 SQL_PARC_NO_BATCH 則不會。 對於**SELECT**語句，如果 SQL_PARAM_ARRAY_SELECT 傳回 SQL_PAS_BATCH，則會填入參數狀態陣列，但如果傳回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT 則不會。  
  
## <a name="data-at-execution-parameters"></a>資料執行中參數  
 如果長度/指標陣列中的任何值 SQL_DATA_AT_EXEC，或 SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果，則會以一般方式以**SQLPutData**傳送這些值的資料。 此程式的下列層面會擲出特殊的批註，因為它們並不容易察覺：  
  
-   當驅動程式傳回 SQL_NEED_DATA 時，它必須將資料列編號變數的位址設定為它需要資料的資料列。 如同單一值的情況，應用程式無法對驅動程式將在單一參數集內要求參數值的順序做出任何假設。 如果執行資料執行中的參數時發生錯誤，則 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性所指定的緩衝區會設定為發生錯誤之資料列的數目，SQL_ATTR_PARAM_STATUS_PTR 語句屬性所指定之資料列狀態陣列中的資料列狀態會設定為 SQL_PARAM_ERROR，而**SQLExecute**、 **SQLExecDirect**、 **SQLParamData**或**SQLPutData**的呼叫會傳回 SQL_ERROR。 如果**SQLExecute**、 **SQLExecDirect**或**SQLParamData**傳回 SQL_STILL_EXECUTING，此緩衝區的內容會是未定義的。  
  
-   因為驅動程式不會針對資料執行中參數解讀**SQLBindParameter**的*ParameterValuePtr*引數中的值，所以如果應用程式提供陣列的指標， **SQLParamData**就不會將此陣列的元素解壓縮並傳回給應用程式。 相反地，它會傳回應用程式所提供的純量值。 這表示**SQLParamData**所傳回的值不足以指定應用程式需要傳送資料的參數;應用程式也需要考慮目前的資料列數目。  
  
     當只有部分參數陣列的元素是資料執行中參數時，應用程式必須在包含所有參數之專案的*ParameterValuePtr*中傳遞陣列的位址。 此陣列會針對不是資料執行中參數的參數，正常地加以解讀。 針對資料執行中的參數， **SQLParamData**提供給應用程式的值（通常可用來識別驅動程式在此情況下所要求的資料）一律是陣列的位址。
