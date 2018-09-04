---
title: 插入或刪除資料列 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f28d49d8636c1a4715eeb73eecfd95a1dffb076b
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279137"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>插入或刪除資料列 (報表產生器及 SSRS)
您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表中的 Tablix 資料區加入或刪除資料列。 Tablix 資料區可以是資料表、矩陣或清單。 下列程序不適用於圖表和量測計資料區域。  
  
 在 Tablix 資料區中，您可以加入與群組相關聯的資料列 (位於群組內部) 或與群組沒有關聯的資料列 (位於群組外部)。 位於群組內部的資料列會針對每個唯一的群組值重複一次。 例如，位於群組內部而且以包含色彩名稱之資料行值為基礎的資料列會針對每個不同的色彩名稱重複一次。 若為巢狀群組，資料列可能會位於子群組外部，但位於父群組內部。 在此情況下，資料列會針對父群組中的每個唯一值重複一次。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>選取資料區，以便顯示資料列和資料行控制代碼  
  
-   在 [設計] 檢視中，按一下 Tablix 資料區的左上角，如此資料行和資料列控制代碼就會顯示在上方和旁邊。  
  
     如需資料區區域的詳細資訊，請參閱 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>在選取的資料區中插入資料列  
  
-   以滑鼠右鍵按一下您想要插入資料列的資料列控制代碼，按一下 [插入資料列]，然後按一下 [上方] 或 [下方]。  
  
     \- 或 -  
  
-   在您想要插入資料列的資料區中，以滑鼠右鍵按一下資料格，按一下 [插入資料列]，然後按一下 [上方] 或 [下方]。  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>從選取的資料區中刪除資料列  
  
-   選取要刪除的一個或多個資料列，以滑鼠右鍵按一下所選資料列之任一資料列的控制代碼，然後按一下 [刪除資料列]。  
  
     \- 或 -  
  
-   在您想要刪除資料列的資料區中，以滑鼠右鍵按一下資料格，然後按一下 [刪除資料列]。  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>在選取之資料區的群組中插入資料列  
  
-   在您想要插入資料列之 Tablix 資料區的資料列群組區域中，以滑鼠右鍵按一下資料列群組資料格，按一下 [插入資料列]，然後按一下 [上方 - 群組外]、[上方 - 群組內]、[下方 - 群組內] 或 [下方 - 群組外]。  
  
     如此就會在您按一下之資料列群組資料格所表示的群組內部或外部加入資料列。  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>從選取之資料區的群組中刪除資料列  
  
-   在您想要刪除資料列之 Tablix 資料區的資料列群組區域中，以滑鼠右鍵按一下資料列群組資料格，然後按一下 [刪除資料列]。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [了解群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
