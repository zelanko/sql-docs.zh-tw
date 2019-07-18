---
title: 選取日曆 （維度精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.serverSpecialCalendars.f1
ms.assetid: 6e28a020-2586-4b13-9333-b499fb1b33af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde8172abbebe08fc4aae4cc0282955c2a582d02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069685"
---
# <a name="select-calendars-dimension-wizard"></a>選取日曆 (維度精靈)
  使用 [選取日曆]  頁面來建立其他階層，其中代表時間維度的會計日曆、報表日曆、製造日曆或國際標準組織 (ISO) 8601 日曆。  
  
> [!NOTE]  
>  唯有在 [選取維度類型]  頁面上選取了 [伺服器時間維度]  ，或者在 [維度定義]  頁面上選取了 [不使用資料來源而建立維度]  ，且在 [選取維度類型]  頁面上選取了 [時間維度]  ，才會顯示此頁面。  
  
## <a name="options"></a>選項。  
 **會計日曆**  
 選取即可根據會計日曆建立時間階層。  
  
 **開始日期和月份**  
 選取會計日曆的開始日期和月份。  
  
> [!NOTE]  
>  唯有選取 [會計日曆]  時，才能使用此選項。  
  
 **會計日曆命名慣例**  
 選取會計日曆所使用的命名慣例。 選取 [日曆年度名稱]  或 [日曆年度名稱 +1]  。  
  
> [!NOTE]  
>  唯有選取 [會計日曆]  時，才能使用此選項。  
  
 **報表 （或行銷） 日曆**  
 選取即可根據報表日曆建立時間階層。  
  
 **開始的週和月份**  
 選取報表日曆開始的週和月份。  
  
> [!NOTE]  
>  選取 [報表 (或行銷) 日曆]  時，才能使用此選項。  
  
 **月份週別模式**  
 選取報表日曆所使用的月份週別模式。  
  
> [!NOTE]  
>  選取 [報表 (或行銷) 日曆]  時，才能使用此選項。  
  
 下表列出月份週別模式可用的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**週 445**|該季的第一個月有 4 週，該季的第二個月有 4 週，而該季的第三個月有 5 週。|  
|**週 454**|該季的第一個月有 4 週，該季的第二個月有 5 週，而該季的第三個月有 4 週。|  
|**週 544**|該季的第一個月有 5 週，該季的第二個月有 4 週，而該季的第三個月有 4 週。|  
  
 **製造日曆**  
 選取即可根據製造日曆建立時間階層。  
  
 **開始的週和月份**  
 選取製造日曆開始的週和月份。  
  
> [!NOTE]  
>  選取 [製造日曆]  時，才能使用此選項。  
  
 **延長期間的季度**  
 選取或鍵入會包含延長期間的季度。  
  
> [!NOTE]  
>  選取 [製造日曆]  時，才能使用此選項。  
  
 **ISO 8601 日曆**  
 選取即可根據 ISO 8601 日曆建立階層。  
  
## <a name="see-also"></a>另請參閱  
 [維度精靈 F1 說明](dimension-wizard-f1-help.md)   
 [維度&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
