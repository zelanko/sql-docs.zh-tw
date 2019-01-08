---
title: 附錄 B：狀態轉換資料表 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 82c19931073aa96eb045f574e8670068f3d3c659
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541066"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>附錄 B：狀態轉換資料表
本附錄中的表格會顯示如何 ODBC 函式會造成的環境、 連接、 陳述式，以及描述項狀態轉換。 環境、 連接、 陳述式，或描述元的狀態通常會規定，使用對應的型別控制代碼 （環境、 連接、 陳述式或描述元） 的函式可以呼叫時的位置。 環境、 連接、 陳述式，以及描述項狀態重疊大致如下列圖例所示。 比方說，C5，C6，確切的重疊的連線狀態和陳述式指出 S12 透過 S1 會是資料來源而異，因為交易開始在不同的資料來源上不同的時間，並描述項狀態 D1i （隱含配置描述元） 而定陳述式與描述元相關聯的狀態，狀態 D1e （明確配置描述項） 時都無關的任何陳述式的狀態。 如需每個狀態的描述，請參閱 <<c0> [ 環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)，[連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)，[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)，和[描述項轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)稍後在本附錄中。  
  
 環境和連接狀態重疊，如下所示：  
  
 ![環境和連接狀態重疊](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 連接和陳述式狀態重疊，如下所示：  
  
 ![連接和陳述式狀態重疊](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 陳述式，並描述項狀態重疊，如下所示：  
  
 ![陳述式，並描述項狀態重疊](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 連接及描述項狀態重疊，如下所示：  
  
 ![連接及描述項狀態重疊](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 轉換資料表中的每個項目可以是下列值之一：  
  
-   **--** -狀態之後執行函式保持不變。  
  
-   **E**  

     **_n_**  ， **C_n_**， **S_n_**，或**D_n_** -環境、 連接、 陳述式或描述元的狀態會移至指定的狀態。  
 
-   **(KARTRIS)** -無效的控制代碼傳遞給函式。 如果控制代碼的 null 控制代碼是否有效的控制代碼類型錯誤-例如，連接控制代碼時所傳遞的陳述式控制代碼所需-函式會傳回 SQL_INVALID_HANDLE;否則行為未定義的而且可能嚴重。 它會呼叫此函式中指定的狀態的唯一可能的結果時，才會看到這個錯誤。 不會變更狀態以及括號所指示一律偵測到的驅動程式管理員 中，此錯誤。  
  
-   **NS** -下一個狀態。 陳述式轉換會與相同的陳述式有尚未通過的非同步狀態。 例如，假設 建立結果集的陳述式便會進入狀態 S11 從狀態 S1 因為**SQLExecDirect**傳回 SQL_STILL_EXECUTING。 處於 S11 NS 標記法表示的轉換陳述式是相同狀態 S1 中的陳述式來建立結果集。 如果**SQLExecDirect**傳回錯誤，陳述式會保留在狀態 S1; 陳述式如果成功，會移至狀態 S5; 如果它需要資料時，陳述式會移至狀態 S8; 而且如果它仍在執行中，它會保持處於 S11。  

-   **_XXXXX_** 或是 **(*XXXXX*)** -的 SQLSTATE 相關 [轉換] 資料表中。偵測到的驅動程式管理員中的 Sqlstate 是以括號括住。 函式會傳回 SQL_ERROR，而且指定的 SQLSTATE，但並不會變更狀態。 例如，如果**SQLExecute**之前，會呼叫**SQLPrepare**，它會傳回 SQLSTATE HY010 （函數順序錯誤）。  

> [!NOTE]  
>  資料表不會顯示不會變更狀態的轉換資料表不相關的錯誤。 例如，當**SQLAllocHandle**稱為 E1 處於環境，並傳回 SQLSTATE HY001 （記憶體配置錯誤），環境會維持狀態 E1; 這不會顯示在環境轉換資料表中的**SQLAllocHandle**。  
  
 如果環境、 連接、 陳述式或描述元可以移至多個狀態中，會顯示每個可能的狀態，並一或多個註腳說明所在每個轉換發生的條件。 下列的註腳可能會出現在任何資料表中。  
  
|註腳|意義|  
|--------------|-------------|  
|b|之前或之後。 指標置於結果集或結果集的結尾之後開始之前。|  
|c|目前的函式。 目前的函式以非同步方式執行。|  
|d|需要的資料。 此函式會傳回 SQL_NEED_DATA。|  
|e|錯誤。 此函式會傳回 SQL_ERROR。|  
|i|無效的資料列。 指標置於結果中的資料列集和資料列已刪除，或資料列上的作業中發生錯誤。 如果資料列狀態陣列存在，則資料列的資料列狀態陣列中的值會是 SQL_ROW_DELETED 或 SQL_ROW_ERROR。 （資料列狀態陣列是由指向 sql_attr_row_status_ptr 設定陳述式屬性。）|  
|nf|找不到。 此函式會傳回 sql_no_data 為止。 這不適用的時機**SQLExecDirect**， **SQLExecute**，或**SQLParamData**傳回 SQL_NO_DATA 之後執行搜尋的 update 或 delete 陳述式。|  
|np|尚未備妥。 尚未準備陳述式。|  
|nr|沒有結果。 陳述式不會或未建立結果集。|  
|o|其他函式。 另一個函式以非同步方式執行。|  
|p|備妥。 已備妥的陳述式。|  
|r|結果。 將陳述式，或未建立 （可能是空的） 的結果集。|  
|s|成功。 此函式會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|v|有效的資料列。 指標置於結果集中的資料列和插入資料列必須已成功，已成功更新，或另一個資料列上的作業已順利完成。 如果資料列狀態陣列存在，該資料列的資料列狀態陣列中的值為 SQL_ROW_ADDED、 SQL_ROW_SUCCESS 或 SQL_ROW_UPDATED。 （資料列狀態陣列是由指向 sql_attr_row_status_ptr 設定陳述式屬性。）|  
|x|執行中。 此函式會傳回 SQL_STILL_EXECUTING。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 在此範例中，環境狀態轉換中的資料列適用於資料表**SQLFreeHandle**當*HandleType*是 SQL_HANDLE_ENV，如下所示。  
  
|E0<br /><br /> 未配置|E1<br /><br /> 配置|E2<br /><br /> 連接|  
|------------------------|----------------------|-----------------------|  
|(KARTRIS)|E0|(HY010)|  
  
 如果**SQLFreeHandle**呼叫中使用的環境狀態 E0 *HandleType*設定為 SQL_HANDLE_ENV，驅動程式管理員會傳回 SQL_INVALID_HANDLE。 如果呼叫狀態 E1 *HandleType*設定為 SQL_HANDLE_ENV，移至狀態 E0，如果函式成功，並在函數失敗時，會保留在狀態 E1 的環境。 如果呼叫狀態 E2 *HandleType*設定為 SQL_HANDLE_ENV，驅動程式管理員一律會傳回 SQL_ERROR，而且 SQLSTATE HY010 （函數順序錯誤） 和環境仍處於 E2。  
  
 若要了解狀態轉換資料表，就必須了解它們參考到哪一個項目 （環境、 連接、 陳述式或描述元）。 假設函式會接受的項目型別 X 的控制代碼。該函式 X 狀態轉換表描述如何呼叫函式，以控制代碼的型別的項目 X，影響該項目。 例如， **SQLDisconnect**接受連接控制代碼。 連線狀態轉換表**SQLDisconnect**說明如何**SQLDisconnect**影響，它會呼叫連接的狀態。  
  
 假設函式會接受其中 Y 值不等於 X 的控制代碼的型別為 Y 的項目。X 狀態轉換表，該函式的說明會影響的方式呼叫的函式，與型別 X 的型別為 Y 的項目相關聯的控制代碼型別為 Y 的項目。例如，陳述式狀態轉換資料表中的**SQLDisconnect**說明如何**SQLDisconnect**會影響陳述式與其連接的控制代碼的呼叫時的狀態陳述式會產生關聯。  
  
 本附錄包含下列主題。  
  
-   [環境轉換](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [狀態轉換](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [描述項轉換](../../../odbc/reference/appendixes/descriptor-transitions.md)
