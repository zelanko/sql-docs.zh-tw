---
title: 篩選關聯規則模型中的規則 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- filtering rules [Analysis Services]
- Mining Model Viewer [Analysis Services], rules
- Rules Viewer
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 10f0dff6db48300b276ea586ec358e2f15089e14
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522444"
---
# <a name="filter-a-rule-in-an-association-rules-model"></a>篩選關聯規則模型中的規則
  您可以在關聯模型中使用篩選，將結果限制為您所感興趣的關聯。 例如，您可以篩選規則，只顯示包含特定產品的規則。  
  
 在資料採礦設計師中，您可以使用 **關聯規則檢視器 [規則]**[!INCLUDE[msCoName](../../includes/msconame-md.md)] 索引標籤上的控制項來篩選顯示的規則。  您還可以對模型建立查詢，只查看包含特定值的項目集。  
  
> [!NOTE]  
>  這個選項僅適用於使用 Microsoft 關聯分析演算法所建立的採礦模型。  
  
### <a name="filter-a-rule-in-an-association-model"></a>篩選關聯模型中的規則  
  
1.  使用 **[關聯規則檢視器]** 開啟此採礦模型。 若要在 SQL Server Management Studio 中進行這項處理，請以滑鼠右鍵按一下模型名稱，然後選取 **[瀏覽]**。 若要在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中進行這項處理，請按兩下包含此模型的採礦結構，然後按一下 [資料採礦設計師]**** 的 [採礦模型檢視器]**** 索引標籤。  
  
2.  按一下 **[關聯規則檢視器]** 的 **[規則]** 索引標籤。  
  
3.  在 **[篩選規則]** 方塊中輸入規則條件。 例如，規則條件可能是 "Bike Stand"，這也會傳回 "Bike Stands"。  
  
     **[篩選規則]** 文字方塊會支援 .NET 語言所定義的規則運算式。 因此，您可以使用類似以下的運算式： `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`。 此運算式會傳回包含 Helmets 和 Fenders 字 (順序不限) 之屬性的任何項目集。  
  
4.  在 **[最小機率]** 中，增加機率的值來查看更少的規則，或是降低此值來查看更多的規則。  
  
5.  在 **[最低重要性]** 中，增加重要性的值來查看更少的規則，或是降低此值來查看更多的規則。  
  
6.  在 **[顯示]** 中，選取下列其中一個選項： **[顯示屬性名稱和值]**、 **[只顯示屬性名稱]** 或 **[只顯示屬性值]**。  
  
7.  在 **[最大資料列數]** 中，增加這個值來提高符合指定之條件的總規則數，或是降低這個值來限制傳回的規則數。 規則會依據機率來排序，所以您可能會為了機率或重要性而移除符合指定之條件的其他規則。  
  
8.  選取或取消選取 **[顯示完整名稱]** 核取方塊，以切換規則名稱顯示的方式。  
  
     現在規則經過篩選後，只會顯示包含指示之項目的規則。 篩選條件會套用到屬性值，不論是在規則分隔符號 "->" 之前或之後。  
  
    > [!NOTE]  
    >  此檢視器會根據採礦模型的查詢來快取最初的規則清單，而且除非您設定最大資料列數、機率、重要性或完整名稱的顯示來變更此查詢的條件，否則此檢視器不會重新整理規則的清單。 因此，如果您輸入一個條件，而顯示畫面並未立即重新整理，您可以選取 **[顯示完整名稱]** 核取方塊然後再將它取消選取，以強制檢視器重新整理資料。  
  
### <a name="create-a-query-on-the-itemsets-in-an-association-model"></a>對關聯模型中的項目集建立查詢  
  
-   [關聯模型查詢範例](association-model-query-examples.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)   
 [使用 Microsoft 關聯規則檢視器流覽模型](browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [第 3 課：建立購物籃狀況 &#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
