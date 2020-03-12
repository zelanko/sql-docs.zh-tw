---
title: 使用者定義的函式 | Microsoft 文件
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
- UDF
- TVF
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09fb423dc4d3685b22c67b2a86a74443633ba74a
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2020
ms.locfileid: "78370541"
---
# <a name="user-defined-functions"></a>使用者定義的函式
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者定義函數與程式語言函數類似，是可接受參數、執行動作 (如複雜計算) 以及傳回該動作所得值的常式。 傳回值可以是單一純量值或結果集。  
   
##  <a name="Benefits"></a> 使用者定義的函式  
為何要使用使用者定義函式 (UDF)？ 
  
-   可進行模組化的程式撰寫。  
  
     只需建立函數一次，將它儲存在資料庫中，就可以在程式中無限次地隨意呼叫。 使用者自訂函數不需透過原始程式碼即可修改 。  
  
-   可加快執行速度。  
  
     如同預存程序，[!INCLUDE[tsql](../../includes/tsql-md.md)]  使用者自訂函數可藉由針對重複執行來快取以及重複使用計畫，來降低 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼的編譯成本。 這表示，每次使用時，使用者自訂函數不需要重新剖析和最佳化，所以執行時間可以更快。  
  
     與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數相比，CLR 函數在計算工作、字串處理與商務邏輯等方面提供更顯著的效能優勢。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數更適用於經常需要存取資料的作業。  
  
-   可降低網路傳輸量。  
  
     對於無法以單一純量運算式表示的作業 (例如，根據某些複雜條件約束來篩選資料)，可以利用函數來表示。 接著，您可以在 WHERE 子句中叫用函式，以減少傳送到用戶端的資料列數。  
  
> [!IMPORTANT]
> 查詢中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] UDF 只能在單一執行緒上執行 (序列執行計劃)。 因此使用 UDF 會禁止平行查詢處理。 如需平行查詢處理的詳細資訊，請參閱[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)。
  
##  <a name="FunctionTypes"></a> 函式類型  
**純量函式**  
 使用者定義純量函數會傳回在 RETURNS 子句中所定義之類型的單一資料值。 針對內嵌純量函式，傳回的純量值是單一陳述式的結果。 針對多重陳述式純量函式，函式主體可包含一系列傳回單一值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 傳回類型可以是 **text**、 **ntext**、 **image**、 **cursor**和 **timestamp**以外的任何資料類型。 
 **[範例。](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)**
  
**資料表值函式**  
 使用者定義的資料表值函數會傳回 **table** 資料類型。 若是內嵌資料表值函式，則不會有函式主體；資料表會是單一 SELECT 陳述式的結果集。 **[範例。](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)**
  
**系統函式**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供許多可用以執行各種作業的系統函數。 這些函數不能修改。 如需詳細資訊，請參閱[內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)、[系統預存函式 &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md)，和[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
##  <a name="Guidelines"></a> 指導方針  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 造成陳述式取消並且以模組中下一個陳述式繼續 (例如觸發程序或預存程序) 的錯誤會在函式內部以不同方式處理。 在函數中，這樣的錯誤會造成函數停止執行。 進而導致叫用該函數的陳述式取消。  
  
 `BEGIN...END` 區塊中的陳述式不能有任何副作用。 函數副作用是在函數的範圍外對資源狀態所做的任何永久變更，例如修改資料庫資料表。 在函數中陳述式只能變更函數的區域性物件，例如本機資料指標或變數。 在函數中不得執行的動作包括修改資料庫資料表、對函數的非本機資料指標進行運算、傳送電子郵件、試圖修改目錄，以及產生傳回給使用者的結果集。  
  
> [!NOTE]
> 若 `CREATE FUNCTION` 陳述式會對資源產生在發出 `CREATE FUNCTION` 陳述式時不存在的副作用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行該陳述式。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會執行叫用的函數。  
  
 查詢中指定的函數真正執行的次數，會因最佳化工具建立的執行計畫而有不同。 `WHERE` 子句中的子查詢所叫用的函式就是一個例子。 子查詢及其函數的執行次數，會因最佳化工具選擇的存取路徑而有不同。  
 
> [!IMPORTANT]   
> 如需使用者定義函式的詳細資訊和效能考量事項，請參閱[建立使用者定義函式 &#40;資料庫引擎&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)。 
  
##  <a name="ValidStatements"></a> 函式中有效的陳述式  
函數中有效的陳述式類型包括：  
  
-   `DECLARE` 陳述式，可用來定義對函式而言為區域的資料變數與資料指標。  
  
-   指派值給對函式而言為區域的物件，例如使用 `SET` 將值指派給純量及資料表區域變數。  
  
-   參考在函數中宣告、開啟、關閉及取消配置的本機資料指標之資料指標運算。 不允許將資料傳回用戶端的 `FETCH` 陳述式。 只允許使用 `INTO` 子句將值指派給區域變數的 FETCH 陳述式。  
  
-   除 `TRY...CATCH` 陳述式之外的流程控制陳述式。  
  
-   `SELECT` 陳述式，包含選取清單，其中含有將值指派給區域變數的運算式。  
  
-   `UPDATE`、`INSERT` 和 `DELETE` 陳述式，修改對函式而言為區域變數的資料表變數。  
  
-   呼叫擴充預存程序的 `EXECUTE` 陳述式。  
  
### <a name="built-in-system-functions"></a>內建系統函數  
 下列非決定性內建函數可用於 Transact-SQL 使用者定義函數中。  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 下列非決定性內建函式**不得**用於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者定義函式中。  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 如需決定性與非決定性內建系統函數的清單，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
##  <a name="SchemaBound"></a> 結構描述繫結的函式  
 `CREATE FUNCTION` 支援 `SCHEMABINDING` 子句，它可將函式與其參考的任何物件結構描述繫結在一起，例如資料表、檢視及其他使用者定義函式。 嘗試更改或卸除任何被結構描述繫結函數所參考的物件將會失敗。  
  
 必須滿足以下條件，您才可以在 [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) 中指定 `SCHEMABINDING`：  
  
-   函數所參考的所有檢視及使用者自訂函數，都必須是結構描述繫結的。  
  
-   函數所參考的所有物件，都必須與函數位於相同的資料庫。 這些物件必須利用單一部份或兩部份名稱來加以參考。  
  
-   您對於函式中參考的所有物件 (資料表、檢視及使用者定義函式) 必須擁有 `REFERENCES` 權限。  
  
 您可以使用 `ALTER FUNCTION` 來移除結構描述繫結。 `ALTER FUNCTION` 陳述式應在不指定 `WITH SCHEMABINDING` 的情況下重新定義函式。  
  
##  <a name="Parameters"></a> 指定參數  
 使用者自訂函數會使用零或多個輸入參數，並會傳回純量值或資料表。 每一函數最多可以有 1024 個輸入參數。 若函數的參數有預設值，在呼叫函數以取得預設值時必須指定 DEFAULT 關鍵字。 此一行為不同於使用者自訂預存程序中有預設值的參數，在這些預存程序中省略參數亦意謂著省略預設值。 使用者自訂函數不支援輸出參數。  
  
##  <a name="Tasks"></a> 更多範例！  
  
|||  
|-|-|  
|**工作描述**|**主題**|  
|描述如何建立 Transact-SQL 使用者定義函數。|[建立使用者定義函式 &#40;資料庫引擎&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|描述如何建立 CLR 函數。|[建立 CLR 函數](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|描述如何建立使用者定義的彙總函式。|[建立使用者定義彙總](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|描述如何修改 Transact-SQL 使用者定義函數。|[修改使用者定義函數](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|描述如何刪除使用者定義函數。|[刪除使用者定義函數](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|描述如何執行使用者定義函數。|[執行使用者定義函數](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|描述如何重新命名使用者定義函數。|[重新命名使用者定義函數](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|描述如何檢視使用者定義函數的定義。|[檢視使用者定義函數](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
