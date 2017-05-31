---
title: "Database Engine 查詢編輯器 (SQL Server Management Studio) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40ac7dd736d0366fe5cb564719a375e2e6a6a43d
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>Database Engine 查詢編輯器 (SQL Server Management Studio)
  使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器，建立及執行包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的指令碼。 此編輯器也支援執行包含 **sqlcmd** 命令的指令碼。  
  
## <a name="transact-sql-f1-help"></a>Transact-SQL F1 說明  
 當您選取 F1 時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器支援將您連結至特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的參考主題。 若要執行這項操作，請反白顯示 Transact-SQL 陳述式的名稱，然後選取 F1。 接著，說明搜尋引擎會搜尋具有符合您反白顯示的字串之 F1 說明屬性的主題。  
  
 如果說明搜尋引擎找不到具有完全符合您反白顯示的字串之 F1 說明關鍵字的主題，則會顯示此主題。 在這種情況下，有兩種方法可以找到您正在尋找的說明：  
  
-   複製您反白顯示的編輯器字串，並將它貼入《SQL Server 線上叢書》的 [搜尋] 索引標籤，然後進行搜尋。  
  
-   僅反白顯示 Transact-SQL 陳述式可能符合套用至主題之 F1 說明關鍵字的部分，然後再次選取 F1。 搜尋引擎要求您反白顯示的字串與指派給主題的 F1 說明關鍵字完全相符。 如果您反白顯示的字串包含環境獨有的元素 (例如資料行或參數名稱)，搜尋引擎不會產生符合的結果。 反白顯示的字串範例包括：  
  
    -   Transact-SQL 陳述式的名稱，例如 SELECT、CREATE DATABASE 或 BEGIN TRANSACTION。  
  
    -   內建函數的名稱，例如 SERVERPROPERTY 或 @@VERSION。  
  
    -   系統預存程序資料表的名稱，或是檢視表，例如 sys.data_spaces 或 sp_tableoption。  
  
## <a name="working-with-the-database-engine-query-editor"></a>使用 Database Engine 查詢編輯器  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中實作的四個編輯器之一。 如需在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中實作之功能及您可以使用編輯器執行之主要工作的描述，請參閱[查詢與文字編輯器 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)。  
  
## <a name="sql-editor-toolbar"></a>SQL 編輯器工具列  
 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器開啟時，SQL 編輯器工具列會顯示下列按鈕。  
  
 **Connect**  
 隨即開啟 [連接到伺服器] 對話方塊。 使用此對話方塊可建立與伺服器的連接。  
  
 **中斷連接**  
 中斷目前查詢編輯器的伺服器連接。  
  
 **變更連接**  
 隨即開啟 [連接到伺服器] 對話方塊。 使用此對話方塊可建立與不同伺服器的連接。  
  
 **使用目前的連接新增查詢**  
 開新的 [查詢編輯器] 視窗，並使用目前 [查詢編輯器] 視窗中的連接資訊。  
  
 **可用的資料庫**  
 變更連接到同一伺服器的其他資料庫。  
  
 **Execute**  
 執行選取的程式碼，或是在未選取任何程式碼時，執行查詢編輯器中的所有程式碼。  
  
 **偵錯**  
 啟用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具。 此偵錯工具支援偵錯動作，例如設定中斷點、監看變數及逐步執行程式碼。  
  
 **取消執行查詢**  
 將取消要求傳送到伺服器。 部份查詢無法立即取消，必須等候適當的取消條件。 當取消交易之後，交易回復時可能產生延遲。  
  
 **剖析**  
 檢查選取之程式碼的語法。 如果未選取任何程式碼，則會檢查 [查詢編輯器] 視窗中所有程式碼的語法。  
  
 **顯示估計執行計畫**  
 在未實際執行查詢的情況下，向查詢處理器要求查詢執行計畫，並且將計畫顯示在 [執行計畫] 視窗中。 此計畫會使用索引統計資料，當做執行查詢時，每個部分預期將傳回的預估資料列數。 使用的實際查詢計劃可以與預估的執行計畫不同。 如果傳回的資料列數與預估的資料列數差異極大，而且查詢處理器為了要提高效率而變更計畫時，就可能發生這個情況。  
  
 **查詢選項**  
 隨即開啟 [查詢選項] 對話方塊。 使用此對話方塊可設定查詢執行與查詢結果的預設選項。  
  
 **啟用 IntelliSense**  
 指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中是否有提供 IntelliSense 功能。  
  
 **包括實際執行計畫**  
 執行查詢、傳回查詢結果以及查詢使用的執行計畫。 這些會當做圖形化查詢計劃出現在 **[執行計畫]** 視窗中。  
  
 **包括用戶端統計資料**  
 包括 [用戶端統計資料] 視窗，其中包含關於查詢、網路封包的統計資料，以及查詢經過的時間。  
  
 **以文字顯示結果**  
 在 [結果] 視窗中以文字傳回查詢結果。  
  
 **以方格顯示結果**  
 在 [結果] 視窗中以一或多個方格傳回查詢結果。  
  
 **將結果存檔**  
 執行查詢時，會開啟 [儲存結果] 對話方塊。 在 **[儲存於]**中，選取您想要用來儲存檔案的資料夾。 在 **[檔案名稱]**中輸入檔案的名稱，然後按一下 **[儲存]** ，將查詢結果另存為使用 .rpt 副檔名的 **[報表]** 檔案。 若要使用進階選項，請按一下 [儲存] 按鈕上的向下箭頭，然後按一下 [使用編碼方式儲存]。  
  
 **註解選取範圍**  
 在行頭加入註解運算子 (--)，將目前的行標示為註解。  
  
 **取消註解選取範圍**  
 在行頭移除任何註解運算子 (--)，將目前的行標示為使用中的來源陳述式。  
  
 **減少行縮排**  
 移除行頭的空白，將此行的文字移到左邊。  
  
 **增加行縮排**  
 在行頭加入空白，將此行的文字移到右邊。  
  
 **指定範本參數的值**  
 開啟一個對話方塊，讓您指定預存程序和函數中之參數的值。  
  
 您也可以加入 SQL 編輯器工具列，其方式是選取 **[檢視]** 功能表、選取 **[工具列]**，然後選取 **[SQL 編輯器]**。 如果您在沒有任何 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗開啟時加入 SQL 編輯器工具列，則所有的按鈕都將無法使用。  
  
## <a name="sql-editor-toolbar"></a>SQL 編輯器工具列  
 當開啟 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗時，您可以加入 [偵錯] 工具列，其方式是選取 **[檢視]** 功能表、選取 **[工具列]**，然後選取 **[偵錯]**。 如果您在沒有任何 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗開啟時加入 [偵錯] 工具列，則所有的按鈕都將無法使用。  
  
 **Continue**  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗中執行程式碼，直到遇到中斷點為止。  
  
 **全部中斷**  
 設定偵錯工具在遇到中斷時，中斷附加偵錯工具的所有處理序。  
  
 **停止偵錯**  
 讓選取的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗移出偵錯模式，並還原標準執行模式。  
  
 **顯示下一個陳述式**  
 將游標移到下一個要執行的陳述式。  
  
 **逐步執行**  
 系統會執行下一個陳述式。 如果此陳述式會叫用 Transact-SQL 預存程序、函數或觸發程序，偵錯工具就會顯示包含模組程式碼的新 [查詢編輯器] 視窗。 此視窗會處於偵錯模式中，而且執行作業會在模組的第一個陳述式上暫停。 接著，您就可以透過如設定中斷點或逐步執行程式碼，在模組之間移動。  
  
 **不進入函數**  
 系統會執行下一個陳述式。 如果此陳述式會叫用 Transact-SQL 預存程序、函數或觸發程序，此模組就會執行直到完成為止，而且結果會傳回給呼叫的程式碼。 如果您確定模組中沒有任何錯誤，就可以不進入此模組。 在呼叫模組之後的陳述式上會暫停執行。  
  
 **跳離函數**  
 跳回下一個最高的呼叫層級 (函數、預存程序或觸發程序)。 執行作業會在呼叫預存程序、函數或觸發程序之後的陳述式上暫停。  
  
 **視窗**  
 開啟 [中斷點] 視窗或 [即時運算] 視窗。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Management Studio 鍵盤快速鍵](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
