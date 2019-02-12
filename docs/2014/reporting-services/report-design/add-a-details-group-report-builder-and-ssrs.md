---
title: 新增詳細資料群組 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e6b467700d816e4b46dfa7ae38f67be32234c7d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041789"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>加入詳細資料群組 (報表產生器及 SSRS)
  系統會將報表資料集中的詳細資料指定為沒有群組運算式的群組。 當您想要顯示矩陣的詳細資料、加回您已經從資料表或清單中刪除的詳細資料，或加入額外的詳細資料群組時，請將詳細資料群組加入至現有的 Tablix 資料區域。 如需群組的詳細資訊，請參閱 [了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>將詳細資料群組加入到 Tablix 資料區域  
  
1.  在設計介面上，按一下 Tablix 資料區域中的任意位置來選取它。 [群組] 窗格會顯示選定資料區域的資料列和資料行群組。  
  
2.  在 [群組] 窗格中，以滑鼠右鍵按一下屬於最內部之子群組的群組。 按一下 **[加入群組]**，然後按一下 **[子群組]**。 **[Tablix 群組]** 對話方塊隨即開啟。  
  
3.  在 **[群組運算式]** 中，將運算式保留空白。 詳細資料群組沒有運算式。  
  
4.  選取 **[顯示詳細資料]**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     此時新的詳細資料群組會當做子群組加入到 [群組] 窗格中，而且您在步驟 1 中選取之群組的資料列控制代碼會顯示詳細資料群組圖示。 如需控制代碼的詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
