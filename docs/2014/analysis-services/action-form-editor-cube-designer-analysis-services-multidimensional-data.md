---
title: 動作表單編輯器 （動作索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f51a23b7dddddc0365809fd6bc92c922fdd402fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239958"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>動作表單編輯器 (動作索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 [Cube 設計師] 中之 [動作] 索引標籤上的 [Action Form Editor (動作表單編輯器)] 窗格，即可建立和修改標準動作。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入動作的名稱。  
  
 **動作目標**  
 展開以檢視 [目標類型] 和 [目標物件] 選項。  
  
 **目標類型**  
 選取要與動作相關聯之物件的類型。 伺服器只會將套用至指定類型之物件的動作傳回用戶端。 如果 [條件] 符合，而且選取了下表中指定的物件，用戶端就可以使用動作。  
  
|值|選取的物件|  
|-----------|---------------------|  
|屬性成員|依據 [目標物件] 中的屬性，從層級選取成員。|  
|資料格|選取了 [目標物件] 中的命名集。 選取 [所有資料格] 即可選取 Cube 中所有的資料格。|  
|Cube|選取了 [目標物件] 中的 Cube。 選取 CURRENTCUBE 即可使用目前的 Cube。<br /><br /> 注意：在 Cube 可能會被重新命名或動作被複製到其他 Cube 的情況下，使用 CURRENTCUBE 可以提供更大彈性。 建議您使用 CURRENTCUBE 來代表目前的 Cube。|  
|維度成員|選取了 [目標物件] 中之維度的成員。|  
|階層|選取了 [目標物件] 中的階層。|  
|階層成員|選取了 [目標物件] 中之階層內的成員。|  
|層級|選取了 [目標物件] 中的層級。|  
|層級成員|選取了 [目標物件] 中之層級內的成員。|  
  
 **目標物件**  
 選取要與動作相關聯的物件。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體只會將套用至所選物件的動作傳回用戶端。 可用物件的清單受到 [目標類型] 之選擇的限制。  
  
 **條件 (選擇性)**  
 輸入描述選擇性條件的多維度運算式 (MDX) 運算式，這要配合 [目標物件] 使用，也因此將進一步限制動作可用的時機。 此運算式必須傳回布林值，如果此值為 True，則表示可使用該動作。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 **動作內容**  
 展開以檢視 [類型] 和 [動作運算式] 選項。  
  
 **型別**  
 選取執行動作時要採取的動作類型。 下列是可以使用的動作類型：  
  
|值|描述|  
|-----------|-----------------|  
|資料集|傳回用戶端應用程式要執行和顯示的多維度運算式 (MDX) 陳述式 (代表多維度資料集)。|  
|專屬|傳回與此動作的 [應用程式] 設定相關聯之用戶端應用程式可以解譯的專屬字串。|  
|資料列集|傳回用戶端應用程式要執行和顯示的多維度運算式 (MDX) 陳述式 (代表表格式資料列集)。|  
|引數|傳回用戶端應用程式要執行的命令字串。|  
|URL|傳回用戶端應用程式要開啟的統一資源定位器 (URL) 字串，通常使用網際網路瀏覽器。|  
  
 如需動作類型的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 **動作運算式**  
 鍵入傳回用戶端應用程式執行的動作所傳回之字串的多維度運算式 (MDX) 陳述式。  
  
 **其他屬性**  
 展開以檢視 [引動過程]、[應用程式]、[描述]、[標題] 和 [標題是 MDX] 選項。  
  
 **引動過程**  
 選取設定，以指出何時該執行此動作。  
  
> [!NOTE]  
>  此選項只提供用戶端應用程式何時要執行動作的建議，並不會直接控制動作的叫用。  
  
 下表描述可用的設定。  
  
|值|描述|  
|-----------|-----------------|  
|批次|此動作應該當作批次作業的一部份或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工作來執行。|  
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
  
 如果 [標題是 MDX] 設定為 [True]，則請鍵入會傳回標題字串的多維度運算式 (MDX) 運算式。  
  
 **標題是 MDX**  
 選取 [False] 以指出 [標題] 包含一個常值字串，代表要顯示在用戶端應用程式中的動作標題。  
  
 選取 **[True]** 以指出 **[標題]** 包含一個會傳回字串的 MDX 運算式，字串代表要顯示在用戶端應用程式中的動作標題。 在動作傳回至用戶端應用程式之前，必須先解析 MDX 運算式。  
  
## <a name="see-also"></a>另請參閱  
 [動作&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [動作組合管理&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算工具&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [鑽研動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [報表動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
