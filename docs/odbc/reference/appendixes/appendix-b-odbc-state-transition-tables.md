---
title: 附錄 B:ODBC 狀態過渡表 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302882"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附錄 B：ODBC 狀態轉換資料表
本附錄中的表顯示了 ODBC 函數如何導致環境、連接、語句和描述符狀態的轉換。 環境、連接、語句或描述符的狀態通常規定何時可以調用使用相應句柄類型的函數(環境、連接、語句或描述符)。 環境、連接、語句和描述符狀態大致重疊,如下圖所示。 例如,連接狀態 C5 和 C6 以及語句的準確重疊狀態 S1 到 S12 依賴於數據源,因為事務在不同的數據源上從不同時間開始,並且描述符狀態 D1i(隱式分配的描述符)取決於與描述符關聯的語句的狀態,而狀態 D1e(顯式分配的描述符)獨立於任何語句的狀態。 有關每個狀態的說明,請參考此附錄後面的[環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)、[連線轉換](../../../odbc/reference/appendixes/connection-transitions.md)、[敘述轉換](../../../odbc/reference/appendixes/statement-transitions.md)與[描述符轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)。  
  
 環境和連接狀態重疊如下:  
  
 ![環境及連接狀態重疊](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 連接和語句狀態重疊如下:  
  
 ![連接及陳述式狀態重疊](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 語句和描述符狀態重疊如下:  
  
 ![陳述式及描述項狀態重疊](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 連線與描述符狀態重疊如下:  
  
 ![連接及描述項狀態重疊](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 過渡表中的每個項目可以是以下值之一:  
  
-   **--**-執行函數后狀態保持不變。  
  
-   **E**  

     **_n_** n、C_n_、S_n_ 或**D_n_** - 環境、連接、語句或描述符狀態移動**C_n_****S_n_** 到指定狀態。  
 
-   **(IH)** - 將無效句柄傳遞給函數。 如果句柄是空句柄或錯誤類型的有效句柄(例如,在需要語句句柄時傳遞連接句柄)函數返回SQL_INVALID_HANDLE;否則,行為是未定義的,可能是致命的。 僅當此錯誤是以指定狀態調用函數的唯一可能結果時,才會顯示此錯誤。 此錯誤不會更改狀態,並且始終由驅動程式管理器檢測到,如括弧所示。  
  
-   **NS** - 下一個州。 語句轉換與語句未通過異步狀態相同。 例如,假設創建結果集的語句從狀態 S1 進入狀態 S11,因為**SQLExecDirect**返回SQL_STILL_EXECUTING。 狀態 S11 中的 NS 表示法意味著語句的轉換與創建結果集的狀態 S1 中的語句的轉換相同。 如果 SQLExecDirect 傳回錯誤,則文句將保持狀態為 S1;如果**SQLExecDirect**傳回錯誤,則文句將保持在狀態 S1 狀態。如果成功,語句將移動到狀態 S5;如果成功,則語句將移動到"S5"狀態。如果需要數據,語句將移動到狀態 S8;如果需要數據,則語句將移動到"S8"狀態。如果它仍在執行,它將保持在狀態 S11。  

-   **_XXXXX_** 或 **(*XXXXX*)** - 與轉換表相關的 SQLSTATE;驅動程式管理員檢測到的 SQLSTAT 包含在括弧中。 函數返回SQL_ERROR和指定的 SQLSTATE,但狀態不會更改。 例如,如果在**SQLPrepare**之前呼叫**SQLExecute,** 它將傳回 SQLSTATE HY010(函數序列錯誤)。  

> [!NOTE]  
>  這些表不顯示與不更改狀態的過渡表無關的錯誤。 例如,當**SQLAllocHandle**在環境狀態 E1 中調用並返回 SQLSTATE HY001(記憶體分配錯誤)時,環境將保持在狀態 E1;當 SQLAllocHandle 在環境狀態 E1 中調用時,環境將保持在 E1 狀態中。這未顯示在**SQLAllocHandle**的環境轉換表中。  
  
 如果環境、連接、語句或描述符可以移動到多個狀態,則顯示每個可能的狀態,並且一個或多個腳註解釋每次轉換發生的條件。 以下腳註可能出現在任何表中。  
  
|註腳|意義|  
|--------------|-------------|  
|b|之前或之後。 游標位於結果集開始之前或結果集結束之後。|  
|c|當前函數。 當前函數以異步方式執行。|  
|d|需要數據。 函數返回SQL_NEED_DATA。|  
|e|錯誤。 函數返回SQL_ERROR。|  
|i|無效行。 游標位於結果集中的一行上,該行已被刪除,或者該行的操作中發生錯誤。 如果存在行狀態陣列,則該行行狀態陣列中的值SQL_ROW_DELETED或SQL_ROW_ERROR。 (行狀態數組由SQL_ATTR_ROW_STATUS_PTR語句屬性指向。|  
|nf|找不到。 函數返回SQL_NO_DATA。 當**SQLExecDirect、SQLExecute****SQLExecute**或**SQLParamData**在執行搜尋的更新或刪除語句後返回SQL_NO_DATA時,這不適用。|  
|np|未準備好。 聲明沒有編寫。|  
|nr|無結果。 語句不會或未創建結果集。|  
|o|其他函數。 另一個函數正在異步執行。|  
|p|準備。 聲明是編寫的。|  
|r|結果。 語句將創建或確實創建一個(可能為空)結果集。|  
|s|成功。 函數返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS。|  
|v|有效行。 游標位於結果集中的一行上,並且該行已成功插入、成功更新,或者該行上的另一個操作已成功完成。 如果存在行狀態陣列,則該行行狀態陣列中的值SQL_ROW_ADDED、SQL_ROW_SUCCESS或SQL_ROW_UPDATED。 (行狀態數組由SQL_ATTR_ROW_STATUS_PTR語句屬性指向。|  
|x|執行中。 函數返回SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此示例中,當*HandleType* SQL_HANDLE_ENV時 **,SQLFreeHandle**的環境狀態轉換表中的行如下所示。  
  
|E0<br /><br /> 未配置|E1<br /><br /> 已配置|E2<br /><br /> Connection|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 如果**SQLFreeHandle**在環境狀態 E0 中調用,*句柄類型*設置為SQL_HANDLE_ENV,則驅動程式管理器將返回SQL_INVALID_HANDLE。 如果在狀態 E1 中調用它,*並且 HandleType*設置為SQL_HANDLE_ENV,則如果函數成功,環境將移動到狀態 E0,如果函數失敗,則環境將移動到狀態 E0,並在函數失敗時保持狀態 E1。 如果在狀態 E2 中調用,*句柄類型*設置為SQL_HANDLE_ENV,則驅動程式管理器始終返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤),並且環境保持狀態為 E2。  
  
 要瞭解狀態轉換表,必須瞭解它們引用的項(環境、連接、語句或描述符)。 假設函數接受 X 型項的句柄。該函數的 X 狀態轉換表描述使用類型 X 項的句柄調用函數如何影響該項。 例如 **,SQLDisconnect**接受連接句柄。 **SQLDisconnect**的連接狀態轉換表描述了**SQLDISCONNECT**如何影響調用它的連接的狀態。  
  
 假設函數接受 Y 類型的項的句柄,其中 Y 不等於 X。該函數的 X 狀態轉換表描述呼叫函數(具有與 Y 類型的項關聯的 X 類型的句柄)如何影響 Y 類型的項。例如 **,SQLDisconnect**的語句狀態轉換表描述了 SQLDisconnect 與語句關聯的連接句柄調用時**SQLDisconnect**如何影響語句的狀態。  
  
 本附錄包含以下主題。  
  
-   [環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [狀態轉換](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述項轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)
