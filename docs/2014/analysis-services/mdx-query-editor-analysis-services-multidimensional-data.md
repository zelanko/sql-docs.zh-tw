---
title: MDX 查詢編輯器（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 579af162998ffaa7c9483a6e6d29a87f98e96fac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077883"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>MDX 查詢編輯器 (Analysis Services - 多維度資料)
  使用 MDX 查詢編輯器即可設計和執行以多維度運算式 (MDX) 語言撰寫的陳述式和指令碼。  
  
## <a name="features"></a>特性  
  
-   在 [MDX 查詢編輯器] 的查詢編輯器窗格中鍵入指令碼。  
  
-   若要執行指令碼，請按 **F5**，或在工具列上按一下 [執行]****，抑或在 [查詢]**** 功能表上按一下 [執行]****。 如果已選取部份程式碼，則僅執行該部份程式碼。 如果未選取程式碼，則執行整個 MDX 查詢編輯器的內容。  
  
-   在中繼資料窗格中，可以檢視 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫所包含的 Cube 和其他物件的中繼資料。  
  
-   如需 MDX 語法的說明，請在 [MDX 查詢編輯器] 中選取關鍵字，然後按一下 **F1**。  
  
-   如需 MDX 語法的動態說明，請在 [說明]**** 功能表上，按一下 [動態說明]****，以便開啟動態說明元件。 使用動態說明時，在查詢編輯器中鍵入關鍵字，說明主題就會顯示在 **[動態說明]** 視窗內。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 編輯器工具列  
 當 [MDX 查詢編輯器] 開啟時，顯示的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 編輯器工具列中，就會包含下表列出的按鈕。  
  
|詞彙|定義|  
|----------|----------------|  
|**連線**|開啟 [連接到伺服器]**** 對話方塊，以建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**取消**|中斷 MDX 查詢編輯器與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**變更連接**|開啟 **[連接到伺服器]** 對話方塊，以建立另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。|  
|**使用目前連接的新查詢**|使用目前 MDX 查詢編輯器視窗的連接資訊，開啟新的 MDX 查詢編輯器視窗。|  
|**可用的資料庫**|連接到同一執行個體的另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。|  
|**執行**|執行選取的程式碼，如果未選取程式碼，則執行 MDX 查詢編輯器的所有程式碼。|  
|**分析**|檢查所選取程式碼的語法。 如果未選取程式碼，則會檢查整個 MDX 查詢編輯器視窗的語法。|  
|**取消執行查詢**|將取消要求傳送到伺服器。 部份查詢無法立即取消，必須等候適當的取消條件。 取消查詢之後，交易回復時可能產生延遲。|  
  
## <a name="mdx-query-editor-window"></a>MDX 查詢編輯器視窗  
 下表列出在 MDX 查詢編輯器中可用的選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**查詢編輯器視窗**|鍵入要由 MDX 查詢編輯器執行的 MDX 陳述式和指令碼。<br /><br /> 查詢編輯器的內容功能表提供下列選項：<br /><br /> **剪**下：將目前選取範圍複製到剪貼簿，並從 [查詢編輯器] 視窗中移除選取範圍。<br /><br /> **複製**：將目前選取範圍複製到剪貼簿。<br /><br /> **貼**上：將剪貼簿的內容貼入目前的選取範圍。<br /><br /> **連接**：開啟 [**連接到伺服器**] 對話方塊，以建立與[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例的連接。<br /><br /> **中斷連接**：中斷目前查詢編輯器與[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例的連線。<br /><br /> **中斷所有查詢的連接**：中斷連接所有目前開啟的查詢編輯器。<br /><br /> **變更連接**：開啟 [**連接到伺服器**] 對話方塊，以建立與其他[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例的連接。<br /><br /> **在物件總管中開啟伺服器**：開啟[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]目前查詢編輯器連接的目標實例**物件總管**。<br /><br /> **執行**：執行選取的程式碼，如果未選取任何程式碼，則執行目前查詢編輯器中的完整程式碼。<br /><br /> **屬性視窗**：在中**** [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，顯示目前查詢視窗的 [屬性] 視窗。<br /><br /> **查詢選項**：顯示 [**查詢選項**] 對話方塊。|  
|**中繼資料視窗**|顯示目前連接之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的中繼資料。|  
|**Cube**|選取目前連接之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫內的 Cube，即可在 **[中繼資料]** 索引標籤中顯示與 Cube 相關聯的中繼資料。|  
|**中繼資料**|顯示在 **[Cube]** 中選取之 Cube 的中繼資料，包括量值群組與量值、關鍵效能指標、維度、階層、層級、成員及成員屬性。 若要擷取物件的完整索引鍵，請：<br /><br /> 從 **[中繼資料]** 索引標籤，將物件拖曳至查詢窗格。<br /><br /> 以滑鼠右鍵按一下物件，然後選取 [複製]****，再以滑鼠右鍵按一下查詢窗格，然後選取 [貼上]****。|  
|**函數**|顯示從 MDSCHEMA_FUNCTIONS 結構描述資料列集所擷取，且 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫可以使用的 MDX 函數之中繼資料。 若要擷取函數的語法，請：<br /><br /> 從 **[函數]** 索引標籤，將物件拖曳至查詢窗格。<br /><br /> 以滑鼠右鍵按一下函數，然後選取 **[複製]**，再以滑鼠右鍵按一下查詢窗格，然後選取 **[貼上]**。|  
|**結果視窗**|在方格中顯示 MDX 陳述式或指令碼的結果。|  
|**訊息視窗**|顯示執行 MDX 陳述式或指令碼的相關資訊。 例如，這個視窗會顯示執行期間發生的錯誤，或執行之後擷取的資料格數目。|  
  
  
