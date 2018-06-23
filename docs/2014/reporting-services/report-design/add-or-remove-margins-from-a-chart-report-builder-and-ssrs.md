---
title: 新增或移除圖表中的邊界 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 809c8f142fa7b796286d41c4a7389b760c76334f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135746"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>加入或移除圖表中的邊界 (報表產生器及 SSRS)
  在直條圖和散佈圖類型中，圖表會自動在 X 軸的端點加入側邊界。 在橫條圖類型中，圖表會自動在 Y 軸的端點加入側邊界。 在所有其他圖表類型中，圖表中都不會加入側邊界。 您不可以變更邊界的大小。  
  
 此主題不適用於圓形圖、環圈圖、漏斗圖或金字塔圖等圖表類型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-or-disable-side-margins"></a>啟用或停用側邊界  
  
1.  以滑鼠右鍵按一下座標軸，然後選取 [軸屬性]。 [垂直軸屬性] 或 [水平軸屬性] 對話方塊隨即出現。  
  
2.  在 [軸選項] 頁面上，設定 [側邊界] 屬性：  
  
    -   **自動** ：圖表將會判斷是否要根據圖表類型加入側邊界。  
  
    -   **停用** ：橫條圖、直條圖和散佈圖不會有側邊界。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [軸屬性對話方塊、軸選項 &#40;報表產生器及 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [指定軸間隔 &#40;報表產生器及 SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [圖表&#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  