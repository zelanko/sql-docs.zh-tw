---
title: "將總計新增到群組或 Tablix 資料區 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: cf1b96c3-7f0f-4c94-ad08-5239c77ccfe4
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: 63b61913ff8df9f2f822e83e5722f0a8895395bd
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs"></a>將總計加入到群組或 Tablix 資料區 (報表產生器及 SSRS)
 您可以在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表的 Tablix 資料區中，加入群組的總計或整個資料區域的總計。 根據預設，總計是套用篩選之後，群組或資料區域中的數值、非 Null 資料的總和。 若要加入群組的總計，在 [群組] 窗格中，按一下群組之快速鍵功能表上的 **[加入總計]** 。 若要加入 Tablix 主體區域中個別資料格的總計，按一下資料格之快速鍵功能表上的 **[加入總計]** 。 [新增總計] 命令與內容相關，而且僅能針對數值欄位啟用。 根據所選取的 Tablix 資料格，您可以在 Tablix 主體區域中選取資料格來加入單一資料格的總計，或者在 Tablix 資料列群組區域或 Tablix 資料行群組區域中選取資料格來加入整個群組的總計。 如需 Tablix 資料區的詳細資訊，請參閱 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)。  
  
 加入總計之後，您可以從內建報表函數的清單，將預設函數 Sum 變更為不同的彙總函數。 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。[!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-total-for-an-individual-value-in-the-tablix-body-area"></a>在 Tablix 主體區域中加入個別值的總計  
  
-   在 Tablix 資料區域主體區域中，以滑鼠右鍵按一下您要加入總計的資料格。 資料格必須包含數值欄位。 指向 **[加入總計]**，然後按一下 **[資料列]** 或 **[資料行]**。  
  
     目前群組外的新資料列或資料行會加入到資料區域中，其中包含您按下之資料格中欄位的預設總計。  
  
     如果 Tablix 資料區域是資料表，將會自動加入資料列。  
  
## <a name="to-add-totals-for-a-row-group"></a>加入資料列群組的總計  
  
-   在 Tablix 資料區域資料列群組區域中，以滑鼠右鍵按一下您要加總之資料列群組區域中的資料格，指向 [新增總計]，然後按一下 [之前] 或 [之後]。  
  
     目前群組外的新資料列會加入到資料區域中，然後會在資料列中加入每個數值欄位的預設總計。  
  
## <a name="to-add-totals-for-a-column-group"></a>加入資料行群組的總計  
  
-   在 Tablix 資料區域資料列群組區域中，以滑鼠右鍵按一下您要加總之資料行群組區域中的資料格，指向 [新增總計]，然後按一下 [之前] 或 [之後]。  
  
     目前群組外的新資料行會加入到資料區域中，然後會在資料行中加入每個數值欄位的預設總計。  
  
## <a name="see-also"></a>另請參閱  
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
