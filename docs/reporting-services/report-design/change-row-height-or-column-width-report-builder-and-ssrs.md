---
title: 變更資料列高度或資料行寬度 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: adf756e3ef9cbed7689a5cceb80e6ef4d93e2fb9
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581722"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>變更資料列高度或資料行寬度 (報表產生器及 SSRS)
  當您設定資料列高度時，就是針對轉譯報表中的資料列指定最大高度。 不過，根據預設，資料列中的文字方塊會設定為垂直成長，以便在執行階段容納其資料，而且這可能會導致資料列擴展超過您所指定的高度。 若要設定固定的資料列高度，您必須變更文字方塊屬性，讓它們不會自動擴展。  
  
 當您設定資料行寬度時，就是針對轉譯報表中的資料行指定最大寬度。 資料行不會自動水平調整來容納文字。  
  
 如果資料列或資料行中的資料格包含矩形或資料區，則資料格的最小高度和寬度就是由包含項目的高度和寬度所決定。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>移動資料列控制代碼以變更資料列高度  
  
1.  在 [設計] 檢視中，按一下 Tablix 資料區中的任何位置，即可選取它。 灰色的資料列控制代碼會顯示在 Tablix 資料區的外框線上。  
  
2.  將滑鼠指標停留在您想要擴展的資料列控制代碼邊緣。 此時就會出現雙向箭頭。  
  
3.  按一下以抓取資料列的邊緣，然後向上或向下移動，以便調整資料列高度。  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>設定儲存格屬性以變更資料列高度  
  
1.  在 [設計] 檢視中，按一下資料表資料列中的儲存格。  
  
     ![資料表中選取的資料格](../../reporting-services/report-design/media/table-selectcell.png "資料表中選取的資料格")  
  
2.  在顯示的 **[屬性]** 窗格中，修改 **[高度]** 屬性，然後按一下 **[屬性]** 窗格外的任何位置。  
  
     ![適用於所選取資料表資料格的 [屬性] 窗格](../../reporting-services/report-design/media/cell-propertiespane.png "適用於所選取資料表資料格的 [屬性] 窗格")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>防止資料列自動垂直擴展  
  
1.  在 [設計] 檢視中，按一下 Tablix 資料區中的任何位置，即可選取它。 灰色的資料列控制代碼會顯示在 Tablix 資料區的外框線上。  
  
2.  按一下資料列控制代碼，即可選取此資料列。  
  
3.  在 [屬性] 窗格中，將 CanGrow 設為 [False]。  
  
    > [!NOTE]  
    >  如果您看不到 [屬性] 窗格，請按一下 **[檢視]** 功能表上的 **[屬性]**。  
  
### <a name="to-change-column-width"></a>若要變更資料行寬度  
  
1.  在 [設計] 檢視中，按一下 Tablix 資料區中的任何位置，即可選取它。 灰色的資料行控制代碼會顯示在 Tablix 資料區的外框線上。  
  
2.  將滑鼠指標停留在您想要擴展的資料行控制代碼邊緣上方， 此時就會出現雙向箭頭。  
  
3.  按一下以抓取資料行的邊緣，然後向左或向右移動，以便調整資料行寬度。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 (報表產生器及 SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 [Tablix 資料區資料格、資料列及資料行 (報表產生器及 SSRS)](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [資料表 (報表產生器及 SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 (報表產生器及 SSRS)](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 (報表產生器及 SSRS)](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 (報表產生器及 SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
