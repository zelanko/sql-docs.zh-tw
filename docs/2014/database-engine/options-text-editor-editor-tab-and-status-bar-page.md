---
title: 選項 (文字編輯器：編輯器索引標籤和狀態列頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 241a74861a7f634389324276daf9b03a8590e64d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844268"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>選項 (文字編輯器：編輯器索引標籤和狀態列頁面）
  [編輯器索引標籤和狀態列] 頁面可讓您自訂 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 查詢編輯器所顯示的資訊。 您可以指定 [查詢編輯器] 視窗的索引標籤和狀態列中顯示的資訊層級，以及狀態列出現在編輯器視窗頂端或底部。  
  
## <a name="option-settings-by-editor"></a>依編輯器的選項設定  
 所有 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 編輯器中都可以使用編輯器索引標籤和狀態列，但有不同的功能等級。  
  
 Database Engine 查詢編輯器可以連接至伺服器群組，在此情況下，它會開啟伺服器群組中所有執行個體的連接，而且可以同時在每個連接上執行相同查詢。 您可以使用這個對話方塊，指定當連接至多個執行個體，而不是一個執行個體時，狀態列會有不同的色彩。若要變更多伺服器的結果選項時，請使用[選項 (查詢結果/SQL Server/多伺服器)](../../2014/database-engine/options-query-results-sql-server-multi-server.md) 頁面。  
  
## <a name="status-bar-content"></a>狀態列內容  
 指定出現在查詢編輯器狀態列中的資訊。  
  
 **顯示執行時間**  
 包括指令碼執行時間。 設定如下：  
  
 **無**  
 狀態列不會顯示任何時間資訊。  
  
 **End**  
 狀態列會在指令碼執行時顯示目前當日時間。 當指令碼完成時，則會顯示指令碼完成的當日時間。  
  
 **經過**  
 狀態列會顯示指令碼已執行的時間長度。 當指令碼完成時，則會顯示執行指令碼所花費的時間。  
  
 **包含資料庫名稱**  
 包含連接的目前資料庫名稱。 當第一次開啟查詢編輯器時，這是登入的預設資料庫。 稍後可透過 Transact-SQL USE 陳述式變更資料庫內容。  
  
 **包含登入名稱**  
 包含登入名稱。  
  
 **包含資料列計數**  
 包含目前執行之指令碼已處理的資料列計數。  
  
 **包含伺服器名稱**  
 包含伺服器名稱。 如果是本機連接，這是執行個體名稱。 如果是遠端連接，這是遠端電腦名稱與執行個體名稱。  
  
## <a name="status-bar-layout-and-colors"></a>狀態列配置和色彩  
 指定查詢編輯器狀態列中項目的色彩。  
  
 **群組連線**  
 當查詢編輯器有一個以上的連接時，設定狀態列的色彩。  
  
 **單一伺服器連接**  
 當查詢編輯器有單一連接時，設定狀態列的色彩。  
  
 **狀態列位置**  
 指定狀態列的位置。 設定如下：  
  
 **頂端**  
 狀態列會出現在 [查詢編輯器] 視窗頂端。  
  
 **底部**  
 狀態列會出現在 [查詢編輯器] 視窗的底部。  
  
## <a name="tab-text"></a>索引標籤文字  
 指定出現在 [查詢編輯器] 視窗頂端之索引標籤的文字。 如果因文字太長而無法顯示時，您可以將滑鼠停留在索引標籤顯示工具提示，檢視其中的完整字串。  
  
 **包含資料庫名稱**  
 包含連接的目前資料庫名稱。 當第一次開啟查詢編輯器時，這是登入的預設資料庫。 稍後可透過 Transact-SQL USE 陳述式變更資料庫內容。  
  
 **包含檔案名稱**  
 包含儲存指令碼的檔案名稱。  
  
 **包含資料夾名稱**  
 包含儲存指令碼檔的資料夾路徑。  
  
 **包含登入名稱**  
 包含登入名稱。  
  
 **包含伺服器名稱**  
 包含伺服器名稱。 如果是本機連接，這是執行個體名稱。 如果是遠端連接，這是遠端電腦名稱與執行個體名稱。  
  
## <a name="see-also"></a>另請參閱  
 [選項&#40;環境：字型和色彩頁面&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [查詢編輯器中的色彩編碼](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
