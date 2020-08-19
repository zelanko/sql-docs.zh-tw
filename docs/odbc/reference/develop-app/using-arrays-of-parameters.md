---
description: 使用參數陣列
title: 使用參數的陣列 |Microsoft Docs
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
ms.openlocfilehash: 1a592131165e7dc2370ab1d22a3d9eba5f9609dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424410"
---
# <a name="using-arrays-of-parameters"></a>使用參數陣列
若要使用參數的陣列，應用程式會使用 SQL_ATTR_PARAMSET_SIZE 的*屬性*引數來呼叫**SQLSetStmtAttr** ，以指定參數集的數目。 它會使用 SQL_ATTR_PARAMS_PROCESSED_PTR 的*屬性*引數來呼叫**SQLSetStmtAttr** ，以指定可供驅動程式傳回已處理參數集數目的變數位址，包括錯誤集。 它會呼叫 **SQLSetStmtAttr** ，並以 SQL_ATTR_PARAM_STATUS_PTR 的 *屬性* 引數來指向陣列，以傳回參數值每個資料列的狀態資訊。 驅動程式會將這些位址儲存在針對語句所維護的結構中。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，呼叫 **SQLParamOptions** 來指定參數的多個值。 在 ODBC 3 中。*x*，呼叫 **SQLParamOptions** 已被 **SQLSetStmtAttr** 的呼叫取代，以設定 SQL_ATTR_PARAMSET_SIZE 和 SQL_ATTR_PARAMS_PROCESSED_ARRAY 屬性。  
  
 在執行語句之前，應用程式會設定每個系結陣列的每個元素的值。 當語句執行時，驅動程式會使用它所儲存的資訊來取出參數值，並將其傳送至資料來源;可能的話，驅動程式應該將這些值以陣列的形式傳送。 雖然使用參數陣列的最佳方式，是藉由對資料來源進行單一呼叫，以陣列中的所有參數執行 SQL 語句，這項功能目前不會在 Dbms 中廣泛提供。 不過，驅動程式可以藉由多次執行 SQL 語句來模擬它，每個都有一組參數。  
  
 在應用程式使用參數陣列之前，必須確定應用程式所使用的驅動程式支援這些參數。 作法有二：  
  
-   僅使用已知支援參數陣列的驅動程式。 應用程式可以硬式編碼這些驅動程式的名稱，也可以指示使用者只能使用這些驅動程式。 自訂應用程式和垂直應用程式通常會使用一組有限的驅動程式。  
  
-   檢查執行時間是否支援參數陣列。 如果可以將 SQL_ATTR_PARAMSET_SIZE 語句屬性設定為大於1的值，則驅動程式支援參數陣列。 一般應用程式和垂直應用程式通常會在執行時間檢查參數陣列的支援。  
  
 您可以使用 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項來呼叫 **SQLGetInfo** ，來判斷資料列計數和結果集在參數化執行中的可用性。 若為 **INSERT**、 **UPDATE**和 **DELETE** 語句，SQL_PARAM_ARRAY_ROW_COUNTS 選項會指出個別的資料列計數是否 (一個用於每個參數集) 可用於 (SQL_PARC_BATCH) 或資料列計數是否匯總成一個 (SQL_PARC_NO_BATCH) 。 針對 **SELECT** 語句，SQL_PARAM_ARRAY_SELECTS 選項會指出每組參數的結果集是否可用 (SQL_PAS_BATCH) 或只有一個結果集可供 (SQL_PAS_NO_BATCH) 使用。 如果驅動程式不允許使用參數陣列來執行結果集產生的語句，SQL_PARAM_ARRAY_SELECTS 會傳回 SQL_PAS_NO_SELECT。 無論參數陣列是否可搭配其他類型的語句使用，尤其是因為在這些語句中使用參數會是資料來源，且不會遵循 ODBC SQL 文法，這是資料來源特有的。  
  
 SQL_ATTR_PARAM_OPERATION_PTR 語句屬性所指向的陣列可以用來忽略參數的資料列。 如果陣列的元素設定為 SQL_PARAM_IGNORE，則會從 **SQLExecute** 或 **SQLExecDirect** 呼叫中排除對應至該專案的參數集。 由應用程式所指向的 SQL_ATTR_PARAM_OPERATION_PTR 屬性所指向的陣列，並由驅動程式讀取。 如果使用提取的資料列做為輸入參數，則可在參數作業陣列中使用資料列狀態陣列的值。  
  
## <a name="error-processing"></a>錯誤處理  
 如果執行語句時發生錯誤，執行函數會傳回錯誤，並將資料列編號變數設定為包含錯誤的資料列數目。 無論是否執行錯誤集以外的所有資料列，或是在執行) 錯誤集之後的所有資料列都未 (之前，它都是資料來源特有的。 因為它會處理參數集，所以驅動程式會將 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性指定的緩衝區，設定為目前正在處理的資料列數目。 如果執行了除了錯誤集以外的所有集合，驅動程式會在處理所有資料列之後，將這個緩衝區設定為 SQL_ATTR_PARAMSET_SIZE。  
  
 如果已設定 SQL_ATTR_PARAM_STATUS_PTR 語句屬性， **SQLExecute** 或 **SQLExecDirect** 會傳回 *參數狀態陣列，* 以提供每一組參數的狀態。 參數狀態陣列是由應用程式佈建，並由驅動程式填入。 其元素指出是否已成功針對參數的資料列執行 SQL 語句，或是否在處理參數集時發生錯誤。 如果發生錯誤，驅動程式會將參數狀態陣列中的對應值設定為 SQL_PARAM_ERROR，並傳回 SQL_SUCCESS_WITH_INFO。 應用程式可以檢查狀態陣列，以判斷已處理的資料列。 使用資料列編號，應用程式通常可以更正錯誤並繼續處理。  
  
 參數狀態陣列的使用方式取決於 **SQLGetInfo**呼叫所傳回的 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 針對 **INSERT**、 **UPDATE**和 **DELETE** 語句，如果 SQL_PARAM_ARRAY_ROW_COUNTS 傳回 SQL_PARC_BATCH，則會使用狀態資訊填入參數狀態陣列，但如果傳回 SQL_PARC_NO_BATCH 則為。 針對 **SELECT** 語句，如果 SQL_PARAM_ARRAY_SELECT 傳回 SQL_PAS_BATCH，則會填入參數狀態陣列，但如果傳回 SQL_PAS_NO_BATCH 或 SQL_PAS_NO_SELECT 則為。  
  
## <a name="data-at-execution-parameters"></a>資料執行中參數  
 如果長度/指標陣列中有任何值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果，則這些值的資料會以一般方式傳送 **SQLPutData** 。 這項程式的下列層面會有特殊批註，因為它們並不容易察覺：  
  
-   當驅動程式傳回 SQL_NEED_DATA 時，必須將資料列編號變數的位址設定為需要資料的資料列。 如同在單一值案例中，應用程式無法對驅動程式將在單一參數集內要求參數值的順序進行任何假設。 如果在執行資料執行中參數時發生錯誤，則 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性指定的緩衝區會設定為發生錯誤的資料列數目，SQL_ATTR_PARAM_STATUS_PTR 語句屬性指定的資料列狀態陣列中的資料列狀態會設定為 SQL_PARAM_ERROR，且 **SQLExecute**、 **SQLExecDirect**、 **SQLParamData**或 **SQLPutData** 的呼叫會傳回 SQL_ERROR。 如果 **SQLExecute**、 **SQLExecDirect**或 **SQLParamData** 傳回 SQL_STILL_EXECUTING，則這個緩衝區的內容是未定義的。  
  
-   因為驅動程式不會在**SQLBindParameter**的*ParameterValuePtr*引數中解讀資料執行中參數的值，所以如果應用程式提供陣列的指標，則**SQLParamData**不會將這個陣列的元素解壓縮並傳回給應用程式。 相反地，它會傳回應用程式提供的純量值。 這表示 **SQLParamData** 傳回的值不足以指定應用程式需要傳送資料的參數;應用程式也需要考慮目前的資料列編號。  
  
     只有當參數陣列的部分元素是資料執行中參數時，應用程式必須傳遞 *ParameterValuePtr* 中包含所有參數之元素的陣列位址。 這個陣列通常是針對不是資料執行中參數的參數進行轉譯。 針對資料執行中參數， **SQLParamData** 提供給應用程式的值（通常可用來識別驅動程式在這種情況下所要求的資料）一律是陣列的位址。
