---
title: 屬性關聯性圖表（屬性關聯性設計工具索引標籤，維度設計師）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.ardesigner.ardiagram.f1
ms.assetid: 320989ad-bd95-43f4-a2e7-b262d66dbda7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0f0e03c8d06d018390a3537ec15c4ab06c927bf4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527894"
---
# <a name="attribute-relationship-diagram-attribute-relationship-designer-tab-dimension-designer-analysis-services---multidimensional-data"></a>屬性關聯性圖表 (屬性關聯性設計師索引標籤，維度設計師) (Analysis Services - 多維度資料)
  在 **[屬性關聯性]** 索引標籤上，使用緊鄰在工具列底下的窗格，即可檢視屬性關聯性圖表，以及建立、修改或刪除屬性關聯性。  
  
 **檢視包含屬性關聯圖表的窗格**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的方案總管中，按兩下維度即可開啟 [維度設計師]，然後按一下 [屬性關聯性]**** 索引標籤。  
  
## <a name="using-the-attribute-relationship-diagram"></a>使用屬性關聯性圖表  
 使用屬性關聯性圖表，即可建立、編輯或刪除屬性關聯性。 此外，屬性關聯性圖表也會反白顯示有問題的屬性關聯性並於工具提示中顯示問題的描述。  
  
 此圖表會提供三個個別的快速鍵功能表：圖表快速鍵功能表、屬性快速鍵功能表和關聯性快速鍵功能表。  
  
### <a name="diagram-shortcut-menu"></a>圖表快速鍵功能表  
 若要開啟屬性關聯性圖表的快速鍵功能表，請以滑鼠右鍵按一下圖表的背景。 圖表快速鍵功能表有下列命令：  
  
 **新增屬性關聯性**  
 開啟 [建立屬性關聯性]**** 對話方塊，而且您可以在其中定義新的屬性關聯性。  
  
 如需詳細資訊，請參閱[建立屬性關聯性和編輯屬性關聯性對話方塊 &#40;屬性關聯性設計師索引標籤，維度設計師&#41; &#40;Analysis Services - 多維度資料&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) 和[定義屬性關聯性](multidimensional-models/attribute-relationships-define.md)。  
  
 **排列形狀**  
 根據 [維度設計師] 所使用的配置演算法，排列形狀。  
  
 **自動排列形狀**  
 根據 [維度設計師] 所使用的配置演算法，自動排列圖表中的形狀。 根據預設， **[自動排列形狀]** 是啟用狀態。  
  
 **顯示清單檢視**  
 顯示或隱藏 [屬性]**** 和 [屬性關聯性]**** 清單。 這些清單顯示於自己的窗格中，而這些窗格緊鄰在包含屬性關聯性圖表的窗格底下。  
  
 **展開所有形狀**  
 顯示與最上層屬性相關聯的群組屬性。 只有在您展開屬性關聯性圖表中的形狀時，才會顯示群組屬性。  
  
> [!NOTE]  
>  如果您按一下這個選項，[維度設計師] 就會讓屬性關聯性圖表中的形狀返回設計師所使用的預設配置。  
  
 **摺疊所有形狀**  
 隱藏與最上層屬性相關聯的群組屬性。  
  
> [!NOTE]  
>  如果您按一下這個選項，[維度設計師] 就會讓屬性關聯性圖表中的形狀返回設計師所使用的預設配置。  
  
 **縮放**  
 顯示可用顯示比例選項的清單。  
  
### <a name="attribute-shortcut-menu"></a>屬性快速鍵功能表  
 若要開啟屬性快速鍵功能表，請以滑鼠右鍵按一下屬性關聯性圖表中的屬性。 屬性快速鍵功能表有下列命令：  
  
 **新增屬性關聯性**  
 開啟 [建立屬性關聯性]**** 對話方塊，而且您可以在其中定義新的屬性關聯性。  
  
 如需詳細資訊，請參閱[建立屬性關聯性和編輯屬性關聯性對話方塊 &#40;屬性關聯性設計師索引標籤，維度設計師&#41; &#40;Analysis Services - 多維度資料&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) 和[定義屬性關聯性](multidimensional-models/attribute-relationships-define.md)。  
  
 **屬性**  
 在 [屬性]**** 視窗中顯示屬性 (Attribute) 的屬性 (Property)。  
  
### <a name="relationship-shortcut-menu"></a>關聯性快速鍵功能表  
 若要開啟關聯性快速鍵功能表，請以滑鼠右鍵按一下在兩種屬性之間識別關聯性的箭號。 關聯性快速鍵功能表有下列命令：  
  
 **編輯屬性關聯性**  
 開啟 [編輯屬性關聯性]**** 對話方塊，而且您可以在其中修改屬性關聯性。  
  
 如需詳細資訊，請參閱[建立屬性關聯性和編輯屬性關聯性對話方塊 &#40;屬性關聯性設計師索引標籤，維度設計師&#41; &#40;Analysis Services - 多維度資料&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) 和[定義屬性關聯性](multidimensional-models/attribute-relationships-define.md)。  
  
 **關聯性類型**  
 將關聯性類型設定為 [彈性]**** 或 [固定]****。 在彈性關聯性中，成員之間的關聯性會隨時間變更。 在固定關聯性中，成員之間的關聯性不會隨時間變更。  
  
 **刪除**  
 刪除屬性關聯性。  
  
 **屬性**  
 在 [屬性]**** 視窗中顯示關聯性的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [屬性關聯性 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](attribute-relationships-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具列 &#40;屬性關聯性設計師索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-attribute-relationship-dimension-designer-analysis-services-multidimensional-data.md)   
 [屬性 &#40;屬性關聯性設計師索引標籤，維度設計師&#41; &#40;Analysis Services 多維度資料&#41;](attributes-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [屬性關聯性 &#40;屬性關聯性設計工具索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](attribute-relationships-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
