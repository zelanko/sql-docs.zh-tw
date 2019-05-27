---
title: 新增刻度斷層至圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d91c65e49d7afda378fb66d5ce65604b7f9b752e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106525"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>將刻度斷層加入至圖表 (報表產生器及 SSRS)
  刻度斷層是在圖表繪圖區上繪製的一道區域線，代表在值軸高低值之間的延續性有斷層 (通常是垂直軸或 Y 軸)。 使用刻度斷層可在相同的圖表區域中顯示兩個相異的範圍。  
  
 ![具有刻度斷層的圖表](../media/rs-multipledatarangeschart-scalebreak.gif "具有刻度斷層的圖表")  
  
> [!NOTE]  
>  您無法指定刻度斷層在圖表上的放置位置。 圖表會根據資料集中的值，自行計算資料範圍之間是否有足夠的分隔，以在執行階段於值軸 (Y 軸) 上繪製刻度斷層。  
  
 具有刻度斷層的圖表範例可從範例報表取得。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](https://go.microsoft.com/fwlink/?LinkId=198283)：  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>若要在圖表上啟用刻度斷層  
  
1.  以滑鼠右鍵按一下垂直軸，然後按一下 [軸屬性]。 [垂直軸屬性] 對話方塊隨即開啟。  
  
2.  選取 [啟用刻度斷層] 核取方塊。  
  
### <a name="to-change-the-style-of-the-scale-break"></a>變更刻度斷層的樣式  
  
1.  開啟 [屬性] 窗格。  
  
2.  以滑鼠右鍵在設計介面上按一下圖表的 Y 軸。 Y 軸物件的屬性 (依預設名為「圖表軸」) 會顯示在 [屬性] 窗格中。  
  
3.  在 [刻度] 區段中，展開 ScaleBreakStyle 屬性。  
  
4.  變更 ScaleBreakStyle 屬性的值，例如 BreakLineType 和 Spacing。 如需刻度中斷線屬性的詳細資訊，請參閱[將包含多個資料範圍的數列顯示在圖表上 &#40;報表產生器及 SSRS&#41;](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [軸屬性對話方塊，軸選項 &#40;報表產生器及 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
