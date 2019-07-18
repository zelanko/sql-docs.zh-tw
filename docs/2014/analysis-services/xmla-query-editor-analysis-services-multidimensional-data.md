---
title: XMLA 查詢編輯器 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.editor.xmla.f1
helpviewer_keywords:
- XMLA Query Editor
- Query Editor [XMLA]
ms.assetid: 14623019-7839-4038-9d12-2f8953d2ec04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1939ea9e1de7b0b7858ad09ad26bc3b4fbf008c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065304"
---
# <a name="xmla-query-editor-analysis-services---multidimensional-data"></a>XMLA 查詢編輯器 (Analysis Services - 多維度資料)
  使用 XMLA 查詢編輯器，即可設計和執行以多維度運算式 (XMLA) 語言撰寫的陳述式和指令碼。  
  
## <a name="features"></a>功能  
  
-   在 XMLA 查詢編輯器的查詢編輯器窗格中鍵入指令碼。  
  
-   若要執行指令碼，請按 **F5**，或在工具列上按一下 [執行]  ，亦或在 [查詢]  功能表上按一下 [執行]  。 如果已選取部份程式碼，則僅執行該部份程式碼。 如果未選取程式碼，則會執行整個 XMLA 查詢編輯器的內容。  
  
-   在中繼資料窗格中，可以檢視 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫所包含的 Cube 和其他物件的中繼資料。  
  
-   如需 XMLA 語法的說明，請在 XMLA 查詢編輯器中選取關鍵字，然後按一下 **F1**。  
  
-   如需 XMLA 語法的動態說明，請在 [說明]  功能表上按一下 [動態說明]  ，以開啟動態說明元件。 使用動態說明時，在查詢編輯器中鍵入關鍵字，說明主題就會顯示在 **[動態說明]** 視窗內。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 編輯器工具列  
 當 XMLA 查詢編輯器開啟時，就會出現 [SQL Server Analysis Services 編輯器]  工具列，其中會顯示下列按鈕。  
  
|詞彙|定義|  
|----------|----------------|  
|**[連接]**|開啟 [連接到伺服器]  對話方塊，以建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**中斷連接**|中斷 XMLA 查詢編輯器與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**變更連接**|開啟 **[連接到伺服器]** 對話方塊，以建立另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**使用目前的連接新增查詢**|使用目前 XML 查詢編輯器視窗的連接資訊，開啟新的 XMLA 查詢編輯器視窗。|  
|**可用的資料庫**|變更連接到同一執行個體的另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。|  
|**執行**|執行選取的程式碼，如果未選取任何程式碼，則會執行 XMLA 查詢編輯器中的所有程式碼。|  
|**剖析**|檢查所選取程式碼的語法。 如果未選取程式碼，此選項會檢查整個 XMLA 查詢編輯器視窗的語法。|  
|**取消執行查詢**|將取消要求傳送到伺服器。 部份查詢無法立即取消，必須等候適當的取消條件。 取消查詢之後，交易回復時可能產生延遲。|  
  
## <a name="xmla-query-editor-window"></a>XMLA 查詢編輯器視窗  
 XMLA 查詢編輯器有下列選項可用：  
  
|詞彙|定義|  
|----------|----------------|  
|**查詢編輯器視窗**|鍵入要由 XMLA 查詢編輯器執行的 XMLA 陳述式和指令碼。<br /><br /> 查詢編輯器的內容功能表提供下列選項：<br /><br /> **剪下**：將目前選取範圍複製到剪貼簿，並從查詢編輯器視窗中移除選取範圍。<br />**複製**：將目前選取範圍複製到剪貼簿。<br />**貼上**：將剪貼簿內容貼到目前選取範圍。<br />**連接**：開啟 [連接到伺服器]  對話方塊，以建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。<br />**中斷連接**：中斷目前查詢編輯器與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。<br />**中斷連接所有查詢**：中斷連接所有開啟的查詢編輯器。<br />**變更連接**：開啟 **[連接到伺服器]** 對話方塊，以建立另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。<br />**在物件總管中開啟伺服器**：在物件總管  中，開啟目前查詢編輯器所連接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。<br />**執行**：執行選取的程式碼，如果未選取程式碼，則執行目前查詢編輯器中的所有程式碼。<br />**屬性視窗**：在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，顯示目前查詢視窗的 [屬性]  視窗。<br />**查詢選項**：顯示 [查詢選項]  對話方塊。|  
|**結果視窗**|以文字顯示 XMLA 陳述式或指令碼的結果。|  
|**[訊息] 視窗**|顯示 XMLA 陳述式或指令碼如何執行的相關資訊。 例如，這個視窗會顯示執行期間發生的錯誤，或執行之後擷取的資料格數目。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 查詢編輯器 &#40;Analysis Services-多維度資料&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [DMX 查詢編輯器 &#40;Analysis Services-資料採礦&#41;](dmx-query-editor-analysis-services-data-mining.md)   
 [查詢與文字編輯器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [SQL Server Management Studio 鍵盤快速鍵](../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
