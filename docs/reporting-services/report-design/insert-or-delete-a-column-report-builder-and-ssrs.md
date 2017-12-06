---
title: "插入或刪除資料行 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9c2dd96d3e5ba42ca292f501fe7726f6549ae860
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>插入或刪除資料行 (報表產生器及 SSRS)
  您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 Tablix 資料區加入或刪除資料行。 Tablix 資料區可以是資料表、矩陣或清單。 下列程序不適用於圖表和量測計資料區域。  
  
 在 Tablix 資料區中，您可以加入與群組相關聯的資料行 (位於群組內部) 或與群組沒有關聯的資料行 (位於群組外部)。 位於群組內部的資料行會針對每個唯一的群組值重複一次。 例如，位於群組內部而且以包含色彩名稱之資料行值為基礎的資料行會針對每個不同的色彩名稱重複一次。 若為巢狀群組，資料行可能會位於子群組外部，但位於父群組內部。 在此情況下，資料列會針對父群組中的每個唯一值重複一次。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>若要選取資料區，以便顯示資料列和資料行控制代碼  
  
-   在 [設計] 檢視中，按一下 Tablix 資料區的左上角，如此資料行和資料列控制代碼就會顯示在它的上方和旁邊。  
  
     如需資料區區域的詳細資訊，請參閱 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
## <a name="to-insert-a-column-in-a-selected-data-region"></a>在選取的資料區中插入資料行  
  
-   以滑鼠右鍵按一下您想要插入資料行的資料行控制代碼、按一下 [插入資料行]，然後按一下 [左方] 或 [右方]。  
  
     -或-  
  
-   在您想要插入資料列的資料區中，以滑鼠右鍵按一下資料格、按一下 [插入資料行]，然後按一下 [左方] 或 [右方]。  
  
## <a name="to-delete-a-column-from-a-selected-data-region"></a>從選取的資料區中刪除資料行  
  
-   選取您想要刪除的一或多個資料行、以滑鼠右鍵按一下其中一個選取之資料行的控制代碼，然後按一下 [刪除資料行]。  
  
     -或-  
  
-   在您想要刪除資料行的資料區中，以滑鼠右鍵按一下資料格，然後按一下 [刪除資料行]。  
  
## <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>在選取之資料區的群組中插入資料行  
  
-   在您想要插入資料行之 Tablix 資料區的資料行群組區域中，以滑鼠右鍵按一下資料行群組資料格、按一下 [插入資料行]，然後按一下 [左方 - 群組外]、[左方 - 群組內]、[右方 - 群組內] 或 [右方 - 群組外]。  
  
     如此就會在您按一下之資料行群組資料格所表示的群組內部或外部加入資料行。  
  
## <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>從選取之資料區的群組中刪除資料行  
  
-   在您想要刪除資料行之 Tablix 資料區的資料行群組區域中，以滑鼠右鍵按一下資料行群組資料格，然後按一下 [刪除資料行]。  
  
## <a name="see-also"></a>另請參閱  
 [了解群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
