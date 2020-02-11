---
title: 選取成員（商業智慧 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cc66896eb1735d09991644dd49c03b5a94c208d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069424"
---
# <a name="select-members-business-intelligence-wizard"></a>選取成員 (商業智慧精靈)
  使用 **[選取成員]** 頁面，即可決定商業智慧精靈應該對哪些成員套用 **[設定貨幣轉換選項]** 頁面所指定的貨幣轉換功能。  
  
> [!NOTE]  
>  如果 [商業智慧精靈] 是從 [維度設計師] 啟動，或是在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中方案總管的某維度上按一下滑鼠右鍵來啟動，則不會出現此頁面。  
  
## <a name="options"></a>選項。  
 **量值維度**  
 選取即可套用貨幣轉換功能至 Cube 中的一個或多個量值。  
  
 若選取，方格會顯示下表列出的選項。  
  
|選項|描述|  
|------------|-----------------|  
|**內建量值類型**|選取即可包含指定量值的貨幣轉換功能。|  
|**量值**|從比率量值群組中選取量值，此群組包含 [內建量值類型]**** 中所選取量值在轉換時使用的匯率。|  
  
 **帳戶階層**  
 選取即可套用貨幣轉換功能至 Cube 所包含帳戶維度之帳戶階層中的一個或多個成員。 帳戶階層是帳戶維度內其`Type`屬性設定為*account*的階層。  
  
 若選取，方格會顯示下表列出的選項。  
  
|選項|描述|  
|------------|-----------------|  
|**帳戶成員**|選取即可包含帳戶階層所指定成員的貨幣轉換功能。|  
|**量值**|從比率量值群組中選取量值，此群組包含 **[帳戶成員]** 中所選取成員之量值在轉換時使用的匯率。|  
  
 **依據類型的帳戶階層**  
 選取即可套用貨幣轉換功能至帳戶階層中、`Type` 屬性設定為指定之帳戶類型的所有屬性成員。  
  
 若選取，方格會顯示下表列出的選項。  
  
|選項|描述|  
|------------|-----------------|  
|**帳戶類型**|選取即可包含所指定帳戶類型的貨幣轉換功能。|  
|**量值**|從比率量值群組中選取量值，此群組包含使用 **[帳戶類型]** 中所選取帳戶類型之屬性成員的量值在轉換時使用的匯率。|  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧 Wizard F1 說明](business-intelligence-wizard-f1-help.md)   
 [Cube 設計工具 &#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [維度設計師 &#40;Analysis Services 多維資料&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
