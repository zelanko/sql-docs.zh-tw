---
title: 查詢與文字編輯器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.TextEditor
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df942352f756c1911693ce339498489f88e31a7f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132968"
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>查詢與文字編輯器 (SQL Server Management Studio)
  您可以使用其中一個 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 編輯器，以互動方式編輯及測試 [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX 或 XML/A 指令碼，或者編輯 XML 或純文字檔。 每個編輯器都會得到一項特定語言專用服務的支援，會將關鍵字著上顏色，且會進行語法和用法錯誤的檢查。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器含有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具，可讓您用來協助修正 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼的問題。  
  
## <a name="sql-server-management-studio-editors"></a>SQL Server Management Studio 編輯器  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的四個編輯器共用一個常見架構。 文字編輯器實作基本的功能層級，並可以當做文字檔的基本編輯器使用。 其他三個編輯器 (查詢編輯器) 將此基本功能擴充到包含可定義 SQL Server 支援的其中一種語言之語法的語言服務。 查詢編輯器也會針對 IntelliSense 和偵錯等編輯器功能，實作不同的支援層級。 這些查詢編輯器包括用來建立包含 Transact-SQL 和 XQuery 陳述式之指令碼的 Database Engine 查詢編輯器、MDX 語言適用的 MDX 編輯器、DMX 語言適用的 DMX 編輯器，以及 XML for Analysis 語言適用的 XML/A 編輯器。  
  
## <a name="common-components"></a>一般元件  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的所有編輯器會共用這些元件：  
  
 **程式碼窗格**  
 您輸入查詢或文字的區域。 在查詢編輯器中，這包含您的語言所能使用的陳述式產生器功能。 支援尋找和取代、大量註解及自訂字型和色彩的文字編輯環境。  
  
 您可以設定在關聯於縮排文字、按 Tab 鍵移動文字和拖放文字等動作時，會影響程式碼窗格中之文字行為的選項。 查詢視窗可以設定為以文件視窗中的索引標籤，或個別文件來運作。  
  
 **選取範圍邊界**  
 空白資料行，在邊界指標列和您可以在其中按一下以選取文字行的程式碼文字之間。 您可以隱藏或顯示選取範圍邊界。  
  
 **水平和垂直捲軸**  
 可讓您水平和垂直捲動程式碼窗格，以便檢視超出程式碼窗格可檢視邊緣的程式碼。  
  
 **顯示行號**  
 在「編輯器」中的文字或程式碼左側顯示行號。 您可以瀏覽至特定行號。  
  
 **自動換行**  
 將很長的文字行或程式碼行分成數行來顯示，您便可以看到該文字行或程式碼行中的所有文字。 自動換行不會影響文字執行或列印時所呈現的方式。 請在 **[工具]** 的 **[選項]** 對話方塊之 [文字編輯器]、[所有語言]、[一般] 頁面上，或在特定編輯器頁面上，開啟 [自動換行]。  
  
## <a name="code-editor-components"></a>程式碼編輯器元件  
 程式碼編輯器除了包含與文字和 XML 編輯器共用的功能之外，還包含下列功能：  
  
 **結果**  
 這個視窗用來檢視查詢結果。 這個視窗能夠以方格或文字來顯示結果，或者將結果導向至檔案。 結果方格可以顯示為個別的索引標籤視窗。  
  
 **IntelliSense**  
 在編輯器的 [編輯] 功能表上，指向 [IntelliSense] 來檢視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 選項。  
  
 **色彩編碼**  
 顯示每種語法元素類型的不同色彩，改進了複雜陳述式的可讀性。  
  
 **程式碼大綱**  
 顯示程式碼群組時，在程式碼左側顯示大綱。 您可以收合和展開程式碼群組，讓您更容易檢視您的程式碼。  
  
 **範本**  
 這些範本是包含必要陳述式之基本結構的檔案，以協助您在資料庫中建立物件。 這些範本可用來加快指令碼編寫速度。  
  
 **訊息**  
 執行指令碼時，顯示伺服器所傳回的錯誤、警告以及參考用訊息。 再次執行指令碼前，訊息清單不會變更。  
  
 **狀態列**  
 顯示與 [查詢編輯器] 視窗相關聯的系統資訊，例如查詢編輯器所連接的執行個體。  
  
## <a name="database-engine-query-editor-components"></a>Database Engine 查詢編輯器元件  
 只有 Database Engine 查詢編輯器才能使用這些元件：  
  
 **偵錯工具**  
 可讓您在特定陳述式上暫停程式碼執行作業。 然後，您就可以檢視資料和系統資訊，以便協助您在程式碼中尋找錯誤。  
  
 **錯誤清單**  
 顯示 IntelliSense 找到的語法和語意錯誤。 當您編輯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼時，這份錯誤清單會動態變更。  
  
 **圖形化執行程序表**  
 顯示針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之執行計畫建立的邏輯步驟。  
  
 **用戶端統計資料**  
 顯示分組成類別目錄之查詢執行的相關資訊。 從 **[查詢]** 功能表中選取 **[包括用戶端統計資料]** 時，會在執行查詢時顯示 **[用戶端統計資料]** 視窗。 來自後續查詢執行的統計資料會與平均值一起列出。 從 **[查詢]** 功能表中選取 **[重設用戶端統計資料]** ，即可重設平均值。  
  
 **程式碼片段**  
 當您在 Database Engine 查詢編輯器中加入陳述式時，可以當做起點使用的範本。 您可以插入 SQL Server 所提供的預先定義程式碼片段，或是加入您自己的程式碼片段。  
  
 **SQLCMD 模式**  
 執行包含一組 sqlcmd 公用程式所支援之命令的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 如需詳細資訊，請參閱 [sqlcmd 使用說明主題](../../database-engine/sqlcmd-how-to-topics.md)。  
  
## <a name="editor-tasks"></a>編輯器工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何檢視及使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器的基本功能。|[Database Engine 查詢編輯器 &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)|  
|描述如何檢視及使用 MDX 查詢編輯器的基本功能。|[MDX 查詢編輯器 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/mdx-query-editor-analysis-services-multidimensional-data.md)|  
|描述如何檢視及使用 DMX 查詢編輯器的基本功能。|[DMX 查詢編輯器 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/dmx-query-editor-analysis-services-data-mining.md)|  
|描述如何檢視及使用 XML/A 查詢編輯器的基本功能。|[XML 編輯器 &#40;SQL Server Management Studio&#41;](xml-editor-sql-server-management-studio.md)|  
|描述如何設定各種編輯器的選項，例如行號和 IntelliSense 選項。|[設定編輯器 &#40;SQL Server Management Studio&#41;](configure-editors-sql-server-management-studio.md)|  
|描述您可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中開啟編輯器的各種方式。|[開啟編輯器 &#40;SQL Server Management Studio&#41;](open-an-editor-sql-server-management-studio.md)|  
|描述如何管理檢視模式，例如自動換行、分割視窗或索引標籤。|[管理編輯器和檢視模式](manage-the-editor-and-view-mode.md)|  
|描述如何設定格式選項，例如隱藏的文字或縮排。|[管理程式碼格式設定](manage-code-formatting.md)|  
|描述如何使用累加搜尋或移至等功能，在編輯器視窗中瀏覽文字。|[導覽程式碼與文字](navigate-code-and-text.md)|  
|描述如何設定各種語法類別的色彩編碼選項，以更容易讀取複雜的陳述式。|[查詢編輯器中的色彩編碼](color-coding-in-query-editors.md)|  
|描述如何使用程式碼大綱，以隱藏您目前未使用的部分複雜指令碼。|[程式碼大綱](code-outlining.md)|  
|描述如何將文字從指令碼的一個位置拖放至新位置。|[拖放文字](drag-and-drop-text.md)|  
|描述如何執行全域搜尋和取代，例如變更資料行名稱時。|[搜尋和取代](search-and-replace.md)|  
|描述如何設定書籤，以便更容易尋找重要的程式碼片段。|[管理書籤](../native-client-ole-db-rowsets/bookmarks.md)|  
|描述如何列印視窗或方格中的指令碼或結果。|[列印程式碼與結果](print-code-and-results.md)|  
|描述如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器的 sqlcmd 功能。|[使用查詢編輯器編輯 SQLCMD 指令碼](edit-sqlcmd-scripts-with-query-editor.md)|  
|描述如何使用 IntelliSense 功能，例如在輸入時自動完成物件名稱，或確保中斷點位於有效的位置。|[IntelliSense &#40;SQL Server Management Studio&#41;](intellisense-sql-server-management-studio.md)|  
|描述如何在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中使用程式碼片段。 程式碼片段是常用陳述式或區塊的範本，可自訂或擴充成包含網站專屬的程式碼片段。|[Transact-SQL 程式碼片段](transact-sql-code-snippets.md)|  
|描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具來逐步執行程式碼，以及檢視偵錯資訊 (例如變數和參數中的值)。|[Transact-SQL 偵錯工具](transact-sql-debugger.md)|  
|描述如何為不同的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體設定自訂色彩，並將這些色彩設為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗中狀態列的背景。|[狀態列 &#40;Database Engine 查詢編輯器&#41;](status-bar-database-engine-query-editor.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Management Studio 鍵盤快速鍵](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
