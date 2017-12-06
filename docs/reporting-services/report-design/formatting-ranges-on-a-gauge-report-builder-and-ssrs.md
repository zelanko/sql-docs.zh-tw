---
title: "設定量測計上範圍的格式 (報表產生器及 SSRS)| Microsoft Docs"
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
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e0202e6304e13851a62896d3bf83807bac7e805d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>設定量測計上範圍的格式 (報表產生器及 SSRS)
 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，量測計範圍是量測計標尺上的一個區域，表示值在量測計上的重要子區段。 您可以使用量測計範圍，以視覺化的方式表示指標值靠近特定值範圍的時間。 範圍是由開始值和結束值所定義。  
  
 您也可以使用範圍來定義量測計的不同區段。 例如，在值範圍為 0 到 10 的量測計上，您可以定義一個值範圍為 0 到 3 的紅色範圍、一個值範圍為 4 到 7 的黃色範圍，以及一個值範圍為 8 到 10 的綠色範圍。 如果您所指定的開始值大於您所指定的結束值，這些值就會交換，讓開始值變成結束值，而結束值變成開始值。  
  
 您可以使用在標尺上放置指標的相同方式來放置範圍。 **[位置]** 和 **[距標尺距離]** 屬性會決定範圍的位置。 如需詳細資訊，請參閱 [量測計 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的標尺 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [格式化量測計上的指標 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [設定量測計的最小值或最大值 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [教學課程：將 KPI 新增至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
