---
title: 附錄 B： ODBC 狀態轉換資料表 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ceb128aec3a4cbe5ef7180483eb2a033ae57138
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996248"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附錄 B：ODBC 狀態轉換資料表
本附錄中的表格顯示 ODBC 函數如何導致環境、連接、語句和描述項狀態的轉換。 環境、連接、語句或描述項的狀態通常會在呼叫使用對應類型之控制碼的函式（環境、連接、語句或描述項）時決定。 環境、連接、語句和描述項狀態會大致重迭，如下列圖例所示。 例如，線上狀態 C5 和 C6 和語句狀態 S1 到 S12 的確切重迭與資料來源相關，因為交易是在不同資料來源的不同時間開始，而描述項狀態 D1i （隱含配置的描述元）相依于與描述元相關聯的語句狀態，而狀態 D1e （明確配置的描述項）則與任何語句的狀態無關。 如需每個狀態的說明，請參閱本附錄稍後的[環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)、[連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)、[語句轉換](../../../odbc/reference/appendixes/statement-transitions.md)和[描述項轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)。  
  
 環境和線上狀態會重迭如下：  
  
 ![環境及連接狀態重疊](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 連接和語句的狀態會重迭如下：  
  
 ![連接及陳述式狀態重疊](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 語句和描述項的狀態會重迭如下：  
  
 ![陳述式及描述項狀態重疊](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 連接和描述項的狀態會重迭如下：  
  
 ![連接及描述項狀態重疊](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 轉換資料表中的每個專案都可以是下列其中一個值：  
  
-   **--**-在執行函數之後，狀態會保持不變。  
  
-   **版**  

     **_n_** 、 **C_n_**、 **S_n_** 或**D_n_** -環境、連接、語句或描述項狀態會移到指定的狀態。  
 
-   **（IH）** -傳遞給函式的控制碼無效。 如果控制碼為 null 控制碼，或為錯誤類型的有效控制碼（例如，當需要語句控制碼時，會傳遞連接控制碼），則函式會傳回 SQL_INVALID_HANDLE;否則，行為會是未定義的，而且可能是嚴重的。 只有在指定的狀態下呼叫函數的唯一可能結果時，才會顯示此錯誤。 此錯誤不會變更狀態，而且驅動程式管理員一律會偵測到，如括弧所示。  
  
-   **NS** -下一個狀態。 語句的轉換與語句不會通過非同步狀態相同。 例如，假設建立結果集的語句從狀態 S1 進入狀態 S11，因為**SQLExecDirect**傳回 SQL_STILL_EXECUTING。 State S11 中的 NS 標記法表示語句的轉換與在建立結果集的狀態 S1 中的語句相同。 如果**SQLExecDirect**傳回錯誤，語句會保留在狀態 S1 中;如果成功，語句就會移至狀態 S5。如果需要資料，語句會移至狀態 S8;如果它仍在執行中，它會維持在狀態 S11 中。  

-   **_Xxxxx_** 或 **（*XXXXX*）** -與轉換資料表相關的 SQLSTATE;驅動程式管理員偵測到的 SQLSTATEs 會括在括弧中。 函數傳回 SQL_ERROR 和指定的 SQLSTATE，但狀態不會變更。 例如，如果在**SQLPrepare**之前呼叫**SQLExecute** ，它會傳回 SQLSTATE HY010 （函數序列錯誤）。  

> [!NOTE]  
>  資料表不會顯示與不會變更狀態的轉換資料表無關的錯誤。 例如，當在環境狀態 E1 中呼叫**SQLAllocHandle** ，並傳回 SQLSTATE HY001 （記憶體配置錯誤）時，環境會保持狀態 e1;這不會顯示在**SQLAllocHandle**的環境轉換表中。  
  
 如果環境、連接、語句或描述項可以移至多個狀態，則會顯示每個可能的狀態，而且有一或多個註腳說明每個轉換發生的條件。 下列註腳可能會出現在任何資料表中。  
  
|註腳|意義|  
|--------------|-------------|  
|b|之前或之後。 資料指標位於結果集開頭之前或結果集結尾的後面。|  
|c|目前的函式。 目前的函式是以非同步方式執行。|  
|d|需要資料。 函數傳回 SQL_NEED_DATA。|  
|e|錯誤。 函數傳回 SQL_ERROR。|  
|i|不正確資料列。 資料指標位於結果集中的資料列，而且資料列已被刪除或資料列的作業中發生錯誤。 如果資料列狀態陣列存在，表示資料列的資料列狀態陣列中的值是 SQL_ROW_DELETED 或 SQL_ROW_ERROR。 （資料列狀態陣列會由 SQL_ATTR_ROW_STATUS_PTR 語句屬性指向）。|  
|nf-e|找不到。 函數傳回 SQL_NO_DATA。 當**SQLExecDirect**、 **SQLExecute**或**SQLParamData**在執行搜尋的 update 或 delete 語句之後傳回 SQL_NO_DATA 時，不適用這種情況。|  
|np|未備妥。 語句尚未備妥。|  
|nr|無結果。 語句將不會或不會建立結果集。|  
|o|其他函數。 另一個函式是以非同步方式執行。|  
|p|製作. 已準備語句。|  
|r|結果。 語句會建立（可能是空的）結果集。|  
|s|成功。 函數傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|v|有效的資料列。 資料指標位於結果集中的資料列，而且資料列已成功插入、成功更新，或資料列上的另一個作業已成功完成。 如果資料列狀態陣列存在，表示資料列的資料列狀態陣列中的值是 SQL_ROW_ADDED、SQL_ROW_SUCCESS 或 SQL_ROW_UPDATED。 （資料列狀態陣列會由 SQL_ATTR_ROW_STATUS_PTR 語句屬性指向）。|  
|x|執行中。 函數傳回 SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此範例中，當*HandleType*為 SQL_HANDLE_ENV 時，環境狀態轉換表中的資料列會**SQLFreeHandle** ，如下所示。  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|HY010|  
  
 如果在環境狀態 E0 中呼叫**SQLFreeHandle** ，並將*HandleType*設為 SQL_HANDLE_ENV，驅動程式管理員會傳回 SQL_INVALID_HANDLE。 如果在狀態 E1 中呼叫它，並將*HandleType*設為 SQL_HANDLE_ENV，則環境會在函式成功時移至狀態 E0，如果函式失敗，則會維持狀態 e1。 如果在*HandleType*設為 SQL_HANDLE_ENV 的狀態 E2 中呼叫它，驅動程式管理員一律會傳回 SQL_ERROR 和 SQLSTATE HY010 （函式序列錯誤），而且環境會維持在狀態 E2。  
  
 若要瞭解狀態轉換資料表，必須瞭解它們所參考的專案（環境、連接、語句或描述項）。 假設函式接受 X 類型專案的控制碼。該函式的 X 狀態轉換表描述如何以 X 類型的專案控制碼呼叫函式，會影響該專案。 例如， **SQLDisconnect**會接受連接控制碼。 **SQLDisconnect**的連接狀態轉換表描述**SQLDisconnect**如何影響呼叫它的線上狀態。  
  
 假設函數接受 Y 類型專案的控制碼，其中 Y 不等於 X。該函式的 X 狀態轉換表描述如何呼叫函式，以及與 Y 類型的專案相關聯之類型 X 的控制碼，會影響 Y 類型的專案。例如， **SQLDisconnect**的語句狀態轉換表描述當使用與語句相關聯之連接的控制碼呼叫時， **SQLDisconnect**會如何影響語句的狀態。  
  
 本附錄包含下列主題。  
  
-   [環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [連線轉換](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述項轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)
