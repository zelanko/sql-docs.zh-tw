---
title: 報表動作表單編輯器 （動作索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b4320fde2f761e75f56e35032676a696a5e9669
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163489"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>報表動作表單編輯器 (動作索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 [Cube 設計師] 中 [動作] 索引標籤的 [報表動作表單編輯器] 窗格，即可修改 [動作組合管理] 中選取的報表動作。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入動作的名稱。  
  
 **動作目標**  
 展開以檢視 [目標類型] 和 [目標物件] 選項。  
  
 **目標類型**  
 選取要與動作相關聯之物件的類型。 伺服器只會將套用至指定類型之物件的動作傳回用戶端。 如果 [條件] 符合，而且選取了下表中指定的物件，用戶端就可以使用動作。  
  
|值|選取的物件|  
|-----------|---------------------|  
|屬性成員|依據 [目標物件] 中的屬性，從層級選取成員。<br /><br /> 注意：使用所選屬性的其他使用者階層，會繼承此報表動作。|  
|資料格|選取了 [目標物件] 中的命名集。 選取 [所有資料格] 即可選取 Cube 中所有的資料格。|  
|Cube|選取了 [目標物件] 中的 Cube。 選取 CURRENTCUBE 即可使用目前的 Cube。<br /><br /> 注意：在 Cube 可能會被重新命名或動作被複製到其他 Cube 的情況下，使用 CURRENTCUBE 可以提供更大彈性。 建議您使用 CURRENTCUBE 來代表目前的 Cube。|  
|維度成員|選取了 [目標物件] 中之維度的成員。|  
|階層|選取了 [目標物件] 中的階層。|  
|階層成員|選取了 [目標物件] 中之階層內的成員。|  
|層級|選取了 [目標物件] 中的層級。|  
|層級成員|選取了 [目標物件] 中之層級內的成員。|  
  
 **目標物件**  
 選取要與動作相關聯的物件。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體只會將套用至所選物件的動作傳回用戶端。 可用物件的清單受到 [目標類型] 之選擇的限制。  
  
 **條件 (選擇性)**  
 輸入描述選擇性條件的多維度運算式 (MDX) 運算式，這要配合 [目標物件] 使用，也因此將進一步限制動作可用的時機。 此運算式必須傳回布林值，如果此值為 True，則表示可使用該動作。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **報表伺服器**  
 展開即可檢視 [伺服器名稱]、[伺服器路徑] 以及 [報表格式] 選項。  
  
 **伺服器名稱**  
 輸入動作會在其上執行報表之 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 執行個體的名稱。  
  
 **伺服器路徑**  
 鍵入 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 執行個體上之報表的路徑。 例如，鍵入 **Sales/YearlySalesByCategory**。  
  
 **報表格式**  
 選取傳回報表時使用的格式。 下表描述可用的格式。  
  
|值|描述|  
|-----------|-----------------|  
|HTML5|報表會以 HTML 5.0 相容的格式傳回。|  
|HTML3|報表會以 HTML 3.2 相容的格式傳回。|  
|[匯出]|報表會以 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 活頁簿 (.xls) 檔案的形式傳回。|  
|PDF|報表會以 Adobe Portable Document Format (.pdf) 檔案傳回。|  
  
 **參數 (選擇性)**  
 展開即可檢視方格，您可以在其中提供 [報表] 所指定報表的報表參數。 方格包含下列資料行：  
  
|「資料行」|描述|  
|------------|-----------------|  
|**參數名稱**|鍵入要傳送給報表之報表參數的名稱。|  
|**參數值**|鍵入要傳送給報表之報表參數的值。<br /><br /> 按一下省略符號按鈕 (**...**) 即可顯示 [MDX 產生器] 對話方塊，並建立提供報表參數值的 MDX 運算式。 如需 [MDX 產生器] 對話方塊的詳細資訊，請參閱 [MDX 產生器對話方塊 &#40;Analysis Services - 多維度資料&#41;](mdx-builder-analysis-services-multidimensional-data.md)。<br /><br /> 如果將參數設定為 MDX 運算式，則在執行動作時會評估該運算式，否則會原封不動傳送給報表。|  
  
 **其他屬性**  
 展開以檢視 [引動過程]、[應用程式]、[描述]、[標題] 和 [標題是 MDX] 選項。  
  
 **引動過程**  
 選取設定，以指出何時該執行此動作。  
  
> [!NOTE]  
>  此選項只提供用戶端應用程式何時要執行動作的建議，並不會直接控制動作的叫用。  
  
 下表描述可用的設定。  
  
|值|描述|  
|-----------|-----------------|  
|批次|此動作應該當作批次作業或 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工作的一部分來執行。|  
|互動式|此動作會在使用者叫用動作時執行。|  
|開啟時|此動作會在第一次開啟 Cube 時執行。|  
  
 **應用程式**  
 鍵入可解譯 動作運算式 傳回之字串的應用程式名稱。  
  
 您也可以使用此選項來識別哪一個用戶端應用程式最常使用這個動作，以及在快顯功能表的該動作旁邊顯示適當的圖示。  
  
> [!NOTE]  
>  此選項只提供用戶端應用程式應該執行哪些動作的建議，並不會直接控制動作的存取。 用戶端應用程式應隱藏與其他用戶端應用程式相關聯的動作。  
  
 **說明**  
 鍵入動作的選擇性描述。  
  
 **Caption**  
 如果 [標題是 MDX] 設為 [False]，則請鍵入要顯示在用戶端應用程式中的動作標題。  
  
 如果 [標題是 MDX] 設為 [True]，請鍵入會傳回標題字串的 MDX 運算式。  
  
 **標題是 MDX**  
 選取 [False] 以指出 [標題] 包含一個常值字串，代表要顯示在用戶端應用程式中的動作標題。  
  
 選取 **[True]** 以指出 **[標題]** 包含一個會傳回字串的 MDX 運算式，字串代表要顯示在用戶端應用程式中的動作標題。 在動作傳回至用戶端應用程式之前，必須先解析 MDX 運算式。  
  
## <a name="see-also"></a>另請參閱  
 [動作&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [動作組合管理&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算工具&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [鑽研動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
