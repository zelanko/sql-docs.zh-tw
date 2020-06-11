---
title: DMX 查詢編輯器（Analysis Services 資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
author: minewiskan
ms.author: owend
ms.openlocfilehash: cc14281cebe3a8e5e401acb7b84367f1688ad0ea
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528498"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>DMX 查詢編輯器 (Analysis Services - 資料採礦)
  使用 [DMX 查詢編輯器] 即可設計和執行以資料採礦延伸模組 (DMX) 語言撰寫的陳述式。  
  
## <a name="features"></a>功能  
  
-   在 [DMX 查詢編輯器] 的查詢編輯器窗格中鍵入指令碼。  
  
-   若要執行指令碼，請按 **F5**，或者在工具列或 **[查詢]** 功能表上按一下 **[執行]** 。 如果已選取部份程式碼，則僅執行該部份程式碼。 如果未選取程式碼，則會執行整個 DMX 查詢編輯器的內容。  
  
-   在中繼資料窗格中，可以檢視 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫所包含的 Cube 和其他物件的中繼資料  
  
-   如需 DMX 的語法說明，請在 [DMX 查詢編輯器] 中選取關鍵字，然後按一下 **F1**。  
  
-   如需 DMX 語法的動態說明，請在 **[說明]** 功能表上，按一下 **[動態說明]** ，以開啟動態說明元件。 使用動態說明時，在查詢編輯器中鍵入關鍵字，說明主題就會顯示在 **[動態說明]** 視窗內。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 編輯器工具列  
 當 [DMX 查詢編輯器] 開啟時，顯示的 **[SQL Server Analysis Services 編輯器]** 工具列中，會包含下表列出的按鈕。  
  
|詞彙|定義|  
|----------|----------------|  
|**[連接]**|開啟 **[連接到伺服器]** 對話方塊，以建立與 Analysis Services 執行個體的連接。|  
|**取消**|中斷 DMX 查詢編輯器與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**變更連接**|開啟 **[連接到伺服器]** 對話方塊，以建立另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**使用目前的連接新增查詢**|開啟新 DMX 查詢編輯器視窗，使用目前 DMX 查詢編輯器視窗的連接資訊。|  
|**可用的資料庫**|變更連接到同一執行個體的另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。|  
|**執行**|執行選取的程式碼，如果未選取程式碼，此選項會執行 DMX 查詢編輯器中的所有程式碼。|  
|**分析**|檢查所選取程式碼的語法。 如果未選取程式碼，此選項會檢查整個 DMX 查詢編輯器視窗的語法。|  
|**取消執行查詢**|將取消要求傳送到伺服器。 部份查詢無法立即取消，必須等候適當的取消條件。 取消之後，交易回復時可能會發生延遲。|  
  
## <a name="dmx-query-editor-window"></a>DMX 查詢編輯器視窗  
 下表列出的選項，是可以在 DMX 查詢編輯器中使用的選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**查詢編輯器視窗**|鍵入要由 DMX 查詢編輯器執行的 DMX 陳述式和指令碼。<br /><br /> 查詢編輯器的內容功能表提供下列選項：<br /><br /> **剪**下：將目前選取範圍複製到剪貼簿，並從 [查詢編輯器] 視窗中移除選取範圍。<br /><br /> **複製**：將目前選取範圍複製到剪貼簿。<br /><br /> **貼**上：將剪貼簿的內容貼入目前的選取範圍。<br /><br /> **連接**：開啟 [連接到伺服器]**** 對話方塊，以建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。<br /><br /> **中斷連接**：中斷目前查詢編輯器與實例的連線 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。<br /><br /> **中斷所有查詢的連接**：中斷連接所有開啟的查詢編輯器。<br /><br /> **變更連接**：開啟 [**連接到伺服器**] 對話方塊，以建立與其他實例的連接 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。<br /><br /> **在物件總管中開啟伺服器**：開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 目前查詢編輯器連接的目標實例**物件總管**。<br /><br /> **執行**：執行選取的程式碼，如果未選取任何程式碼，則執行目前查詢編輯器中的完整程式碼。<br /><br /> **屬性視窗**：在中，顯示目前查詢視窗的 [**屬性**] 視窗 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。<br /><br /> **查詢選項**：顯示 [**查詢選項**] 對話方塊。|  
|**中繼資料視窗**|顯示目前連接之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的中繼資料。|  
|**Cube**|選取目前連接之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫內的 Cube，即可在 **[中繼資料]** 索引標籤中顯示與 Cube 相關聯的中繼資料。|  
|**中繼資料**|顯示在 **[Cube]** 中選取之 Cube 的中繼資料，包括量值群組與量值、關鍵效能指標、維度、階層、層級、成員及成員屬性。 若要擷取物件的完整索引鍵，請：<br /><br /> 從 **[中繼資料]** 索引標籤，將物件拖曳至查詢窗格。<br /><br /> 或：<br /><br /> 以滑鼠右鍵按一下物件，然後選取 **[複製]**，再以滑鼠右鍵按一下查詢窗格，然後選取 **[貼上]**。|  
|**函式**|顯示從 DMSCHEMA_MINING_FUNCTIONS 結構描述資料列集所擷取，且 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫可以使用之 DMX 函數的中繼資料。<br /><br /> 若要擷取函數的語法，請：<br /><br /> 從 **[函數]** 索引標籤，將物件拖曳至查詢窗格。<br /><br /> 或：<br /><br /> 以滑鼠右鍵按一下函數，然後選取 **[複製]**，再以滑鼠右鍵按一下查詢窗格，然後選取 **[貼上]**。|  
|**結果視窗**|在方格中顯示 DMX 陳述式的結果。|  
|**訊息視窗**|顯示有關 DMX 陳述式如何執行的資訊。 例如，這個視窗會顯示執行期間發生的錯誤，或執行之後擷取的資料格數目。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)   
 [MDX 查詢編輯器 &#40;Analysis Services-多維度資料&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [XMLA 查詢編輯器 &#40;Analysis Services-多維度資料&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [查詢和文字編輯器 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [SQL Server Management Studio 鍵盤快速鍵](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [自訂功能表和快速鍵](../ssms/customize-menus-and-shortcut-keys.md)   
 [查詢編輯器中的色彩編碼](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
