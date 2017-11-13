---
title: "附錄 b: ODBC 狀態轉換表 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 775c3d0464443d11b833a230591b94293343086b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-b-odbc-state-transition-tables"></a>附錄 b: ODBC 狀態轉換表
本附錄的表格會顯示如何 ODBC 函數會造成的環境、 連接、 陳述式，以及描述項狀態的轉換。 環境、 連接、 陳述式或描述元的狀態通常會規定使用控制代碼 （環境、 連接、 陳述式或描述元） 的對應類型的函式可以呼叫時。 環境、 連接、 陳述式，以及描述項狀態重疊大約在下圖所示。 例如，完全重疊的連線狀態 C5 和 C6 且陳述式說明 S1 S12 透過資料來源而定，因為交易在不同的時間開始，針對不同的資料來源，並描述項狀態 D1i （隱含地配置描述元） 而定陳述式與描述項相關聯的狀態，而 state D1e （明確配置描述項） 是獨立狀態的任何陳述式。 如需每個狀態的說明，請參閱[環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)，[連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)，[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)，和[描述元轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)稍後在本附錄中。  
  
 環境和連接狀態重疊，如下所示：  
  
 ![環境和連接狀態重疊](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 連接和陳述式狀態重疊，如下所示：  
  
 ![連接和陳述式狀態重疊](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 陳述式及描述項狀態重疊，如下所示：  
  
 ![陳述式及描述項狀態重疊](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 連接及描述項狀態重疊，如下所示：  
  
 ![連接及描述項狀態重疊](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 轉換資料表中的每個項目可以是下列值之一：  
  
-   **--**— 狀態之後執行函式保持不變。  
  
-   **E**  
     ***n*** **C*n***，  **S*n***，或**D*n** *-環境、 連接、 陳述式或描述元的狀態會移到指定的狀態。  
  
-   **(KARTRIS)** -無效的控制代碼傳遞給函式。 如果控制代碼的 null 控制代碼是否有效的控制代碼類型錯誤-需要陳述式控制代碼時，例如，傳遞連接控制代碼 — 函式會傳回 SQL_INVALID_HANDLE;否則行為未定義，而且可能嚴重。 是唯一可能的呼叫函式中指定的狀態結果時，會顯示此錯誤。 此錯誤不會變更狀態，會持續偵測此 dt 由驅動程式管理員，括號所示。  
  
-   **NS** -下一個狀態。 陳述式轉換會與相同的陳述式有尚未通過的非同步狀態。 例如，假設建立結果集的陳述式便會進入狀態 S11 從狀態 S1 因為**SQLExecDirect**傳回 SQL_STILL_EXECUTING。 在狀態 S11 NS 標記法表示陳述式轉換相同狀態 S1 中的陳述式來建立結果集。 如果**SQLExecDirect**傳回錯誤，陳述式維持狀態 S1 陳述式如果成功，會移至狀態 S5; 它需要資料時，如果陳述式會移至狀態 S8; 而如果它仍在執行中，它會維持狀態 S11。  
  
-   ***XXXXX***或 **(*XXXXX*) * *-SQLSTATE 是與 [轉換] 資料表中。Sqlstate 偵測到驅動程式管理員會放在括號。 函式會傳回 SQL_ERROR，並指定的 SQLSTATE，但不會變更狀態。 例如，如果**SQLExecute**之前，會呼叫**SQLPrepare**，它會傳回 SQLSTATE HY010 （函數順序錯誤）。  
  
> [!NOTE]  
>  資料表不會顯示不會變更狀態的轉換資料表不相關的錯誤。 例如，當**SQLAllocHandle**環境狀態 E1 中呼叫，並傳回 SQLSTATE HY001 （記憶體配置錯誤），環境會維持狀態 E1; 這不會顯示在環境轉換資料表**SQLAllocHandle**。  
  
 如果環境、 連接、 陳述式或描述元可以移至多個狀態中，每一可能狀態會顯示，而且一個或多個註腳說明的每個轉換發生的狀況。 下列的註腳可能會出現在任何資料表。  
  
|註腳|意義|  
|--------------|-------------|  
|b|之前或之後。 指標置於結果集或結果集的結尾之後開始之前。|  
|c|目前的函式。 目前的函式以非同步方式執行。|  
|d|需要的資料。 此函式會傳回 SQL_NEED_DATA。|  
|e|錯誤。 此函式會傳回 SQL_ERROR。|  
|i|無效的資料列。 指標置於結果中的資料列集和資料列都已刪除或資料列上的作業中發生錯誤。 如果資料列狀態陣列存在，則資料列的資料列狀態陣列中的值會是 SQL_ROW_DELETED 或 SQL_ROW_ERROR。 （資料列狀態陣列是由指向 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性。）|  
|nf|找不到。 此函式會傳回 sql_no_data 為止。 這不適用時**SQLExecDirect**， **SQLExecute**，或**SQLParamData**傳回 SQL_NO_DATA 之後執行搜尋的 update 或 delete 陳述式。|  
|np|已備妥。 尚未準備陳述式。|  
|編號|沒有結果。 陳述式不會或未建立結果集。|  
|o|其他函式。 另一個函式以非同步方式執行。|  
|p|備妥。 已備妥的陳述式。|  
|r|結果。 將陳述式，或未建立 （也許是空的） 的結果集。|  
|s|成功。 此函式會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|v|有效的資料列。 指標置於結果集中的資料列和資料列已成功插入，已成功更新，或另一個資料列上的作業已順利完成。 如果資料列狀態陣列存在，資料列的資料列狀態陣列中的值就是 SQL_ROW_ADDED、 SQL_ROW_SUCCESS 或 SQL_ROW_UPDATED。 （資料列狀態陣列是由指向 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性。）|  
|x|執行中。 此函式傳回 SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此範例中，環境的狀態轉換中的資料列表的**SQLFreeHandle**時*HandleType*是 SQL_HANDLE_ENV，如下所示。  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|E0|(HY010)|  
  
 如果**SQLFreeHandle**呼叫中使用的環境狀態 E0 *HandleType*設定為 SQL_HANDLE_ENV，驅動程式管理員會傳回 SQL_INVALID_HANDLE。 如果呼叫處於 E1 *HandleType*設定為 SQL_HANDLE_ENV，移至狀態 E0，如果函式成功，而且如果失敗函式維持狀態 E1 的環境。 如果呼叫處於 E2 *HandleType*設定為 SQL_HANDLE_ENV，驅動程式管理員一律會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數順序錯誤），環境會維持在 E2 的狀態。  
  
 若要了解狀態轉換表，就必須了解它們參考到哪一個項目 （環境、 連接、 陳述式或描述項）。 假設函式可接受的類型 X 的項目控制代碼。該函式 X 狀態轉換表會描述如何呼叫函式，以控制代碼類型 X，項目影響該項目。 例如， **SQLDisconnect**接受連接控制代碼。 為連線狀態轉換表**SQLDisconnect**描述如何**SQLDisconnect**會影響它會呼叫其連線的狀態。  
  
 假設函式可接受的控制代碼類型 Y 的項目 Y 不等於 X。該函式 X 狀態轉換表會描述如何呼叫函式的控制代碼的類型 X，Y，類型的項目相關聯影響類型 Y 的項目。例如，陳述式狀態轉換表為**SQLDisconnect**描述如何**SQLDisconnect**會影響陳述式與其連接的控制代碼呼叫時的狀態陳述式會產生關聯。  
  
 本附錄包含下列主題。  
  
-   [環境會轉換](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述元轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)

