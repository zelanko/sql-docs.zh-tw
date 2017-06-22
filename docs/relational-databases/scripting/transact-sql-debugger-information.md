---
title: "Transact-SQL 偵錯工具資訊 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transact-SQL debugger, Locals Window
- Transact-SQL debugger, Watch Window
- Transact-SQL debugger, Threads Window
- Transact-SQL debugger, Call Stack Window
- Transact-SQL debugger, QuickWatch
- Transact-SQL debugger, viewing information
ms.assetid: b99819cc-f388-41a1-b304-36e78ce24147
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 706952bff0744cb88d12a624ba4c68363cb85652
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="transact-sql-debugger---information"></a>Transact-SQL 偵錯工具 - 資訊
  每當偵錯工具在特定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上暫停執行作業時，您就可以使用各種偵錯工具視窗來檢視目前的執行狀態。  
  
## <a name="debugger-windows"></a>偵錯工具視窗  
 在偵錯工具模式中，偵錯工具會在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 主視窗的底部開啟兩個視窗。 偵錯工具會在這兩個視窗中顯示其所有資訊。 每個偵錯工具視窗都具有一些可讓您選取的索引標籤，以便控制哪一組資訊要顯示在視窗中。 左側的偵錯工具視窗包含 [區域變數]、[監看式 1]、[監看式 2]、[監看式 3] 和 [監看式 4] 索引標籤。 右側的偵錯工具視窗包含 [呼叫堆疊]、[執行緒]、[中斷點]、[命令視窗] 和 [輸出] 索引標籤。  
  
> [!NOTE]  
>  先前的描述適用於偵錯工具視窗的預設位置。 您可以拖曳索引標籤，以便在視窗之間移動它，也可以取消停駐索引標籤來建立新的視窗，以便將它放在想要的位置。  
  
 根據預設，並非所有索引標籤或視窗都處於使用中狀態。 您可以使用下列其中一種方式來開啟特定視窗：  
  
-   在 [偵錯] 功能表上，按一下 [視窗]，然後選取您想要的視窗。  
  
-   在 [偵錯] 工具列上，按一下 [中斷點]，然後選取您想要的視窗。  
  
## <a name="transact-sql-expressions"></a>Transact-SQL 運算式  
 運算式是評估成單一純量值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子句，例如變數或參數。 左側的偵錯工具視窗最多可以在五個索引標籤或視窗中顯示目前指派給運算式的資料值：[區域變數]、[監看式 1]、[監看式 2]、[監看式 3] 和 [監看式 4]。  
  
 [區域變數] 視窗會顯示有關 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具目前範圍中之區域變數的資訊。 [區域變數] 視窗中所列的這組運算式會隨著偵錯工具逐步執行不同的程式碼部分而變更。  
  
 [快速監看式] 中的運算式和四個 [監看] 視窗都不限於僅列出變數的識別碼。 您可以指定評估為單一值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式，例如將數字加入變數中，或是評估為單一值的 SELECT 陳述式。 範例如下：  
  
-   變數的名稱，例如 @IntegerCounter。  
  
-   變數上的算術運算，例如 @IntegerCounter + 1。  
  
-   兩個字元變數的字串作業，例如 @FirstName + @LastName。  
  
-   傳回單一值的 SELECT 陳述式，例如 SELECT CharCol FROM MyTable WHERE PrimaryKey = 1。  
  
 您可以使用 [快速監看式] 視窗來檢視 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式的值，然後將該運算式儲存至 [監看式] 視窗。 若要在 [快速監看式] 中選取運算式，請在 [運算式] 方塊中選取或輸入運算式的名稱。  
  
 四個 [監看式] 視窗會顯示有關您已選取之變數和運算式的資訊。 在您於清單中加入或刪除運算式之前，[監看式] 視窗中所列的這組運算式都不會變更。  
  
 若要將運算式加入至 [監看式] 視窗，您可以在 [快速監看式] 對話方塊中選取 [加入監看式]，也可以在 [監看式] 視窗中空白資料列的 [名稱] 資料行中輸入運算式的名稱。  
  
 您可以在 [區域變數]、[監看式] 或 [快速監看式] 視窗中，以滑鼠右鍵按一下資料列，然後選取 [編輯值]，藉以設定變數的資料值。 [區域變數] 視窗、[監看式] 視窗和 [快速監看式] 對話方塊中的 [值] 資料行支援都文字、XML 和 HTML 資料視覺化檢視。 這些視覺化檢視是以 [值] 資料行最右邊的放大鏡資料提示表示。 您可以使用這些視覺化檢視，在符合資料類型的顯示中檢視文字、XML 或 HTML 資料值，例如在瀏覽器視窗中檢視 XML 檔。  
  
 在偵錯模式中，當您將滑鼠指標移到識別碼上方時，[快速諮詢] 快顯就會顯示運算式的名稱及其目前值。 如需詳細資訊，請參閱[快速諮詢 &#40;IntelliSense&#41;](../../relational-databases/scripting/quick-info-intellisense.md)。  
  
## <a name="breakpoints"></a>中斷點  
 您可以使用 [中斷點] 視窗來檢視和管理目前已設定的中斷點。 如需詳細資訊，請參閱[逐步執行 TRANSACT-SQL 程式碼](../../relational-databases/scripting/step-through-transact-sql-code.md)。  
  
## <a name="call-stacks"></a>呼叫堆疊  
 [呼叫堆疊] 視窗會顯示目前的執行位置，以及有關執行作業如何從原始編輯器視窗通過任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模組 (函數、預存程序或觸發程序) 而到達目前執行位置的資訊。 [呼叫堆疊] 視窗中的每個資料列都稱為堆疊框架，而且代表下列任何一個項目：  
  
-   目前的執行位置。  
  
-   從某個模組到另一個模組的呼叫。  
  
-   從編輯器視窗到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模組的呼叫。  
  
 堆疊的順序與呼叫模組的順序相反。 目前的執行位置位於堆疊的頂端，而原始的呼叫則位於底部。 堆疊框架左邊界的黃色箭頭可識別偵錯工具暫停執行作業的所在框架。  
  
 [名稱] 資料行會記錄下列資訊：  
  
-   包含向下呼叫至下一層之程式碼行的來源模組。  
  
-   在堆疊上呼叫下一個模組的程式碼行。  
  
-   如果呼叫移至使用參數的預存程序或函數，就會一併列出所有參數的名稱、資料類型和值。  
  
 [區域變數]、[監看式] 和 [快速監看式] 視窗中的運算式都會針對目前的堆疊框架進行評估。 根據預設，目前的堆疊框架是堆疊中的最上層框架，也就是偵錯工具暫停執行所在的框架。 當您將其他堆疊框架指定成目前的框架時，[區域變數]、[監看式] 和 [快速監看式] 視窗中的運算式就會針對新的堆疊框架重新評估。 您可以按兩下框架，或按一下框架，然後選取 [切換至框架]，藉以變更目前的堆疊框架。 此時，[區域變數]、[監看式] 和 [快速監看式] 視窗中的運算式就會針對新的框架重新評估。 每當目前的堆疊框架不是堆疊中的最上層框架時，堆疊框架左邊界的綠色箭頭可識別目前的堆疊框架。  
  
 當您以滑鼠右鍵按一下堆疊框架，然後選取 [移至原始程式碼] 時，該框架的程式碼就會顯示在 [查詢編輯器] 視窗中。 不過，該框架不會成為目前的框架，而且 [區域變數]、[監看式] 和 [快速監看式] 視窗的內容不會變更。  
  
## <a name="system-information-and-transact-sql-results"></a>系統資訊和 Transact-SQL 結果  
 偵錯工具會在 [輸出] 視窗中列出其狀態和事件訊息。 這包括一些資訊，例如偵錯工具附加至其他處理序的時間，或是偵錯工具執行緒結束的時間。  
  
 在偵錯模式中，[結果] 和 [訊息] 索引標籤仍然會在 [查詢編輯器] 中處於使用中狀態。 [結果] 索引標籤會繼續顯示在偵錯工作階段期間執行之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的結果集。 [訊息] 索引標籤會繼續顯示系統訊息，例如 *xx* 個資料列受影響，以及 PRINT 和 RAISERROR 陳述式的輸出。  
  
## <a name="see-also"></a>另請參閱  
 [本機視窗](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [監看式視窗](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [快速監看式對話方塊](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [中斷點視窗](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md)   
 [呼叫堆疊視窗](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [執行緒視窗](../../relational-databases/scripting/transact-sql-debugger-threads-window.md)   
 [輸出視窗](../../relational-databases/scripting/transact-sql-debugger-output-window.md)   
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
