---
title: 選取轉換類型 （商業智慧精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97ab8896d13bfb19790148fb6f01bb8e054ab270
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748080"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>選取轉換類型 (商業智慧精靈)
  使用 **[選取轉換類型]** 頁面，即可針對以多種貨幣儲存的交易，定義本地貨幣和報表貨幣之間的關聯性。 本地貨幣為 **[選取量值]** 頁面中，選取之量值用於儲存交易的貨幣。 報表貨幣是用於轉換 **[選取量值]** 頁面中所選取交易的貨幣。  
  
> [!NOTE]  
>  如果 [商業智慧精靈] 是從維度設計師啟動，或是在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中之方案總管的某維度上按一下滑鼠右鍵來啟動，則不會出現此頁面。  
  
## <a name="options"></a>選項。  
 **多對多**  
 使用本地貨幣儲存交易。 貨幣轉換功能會先將這類交易轉換為 **[設定貨幣轉換選項]** 頁面中指定的樞紐貨幣，再轉換為一或多種其他的報表貨幣。  
  
 例如，樞紐貨幣可以設定為美元 (USD)，而事實資料表則以歐元 (EUR)、澳幣 (AUD) 和墨西哥披索 (MXN) 儲存交易。 選取此選項會將這些交易從指定的本地貨幣轉換為樞紐貨幣，然後再次將已轉換的交易從樞紐貨幣轉換為指定的報表貨幣。 如此一來，交易就可以儲存為指定的本地貨幣，並以指定的樞紐貨幣來檢視，或以 **[指定報表貨幣]** 頁面中指定的任何報表貨幣來檢視。  
  
 **多對一**  
 使用本地貨幣儲存交易。 貨幣轉換功能會將這類交易轉換為 **[設定貨幣轉換選項]** 頁面中指定的樞紐貨幣。 樞紐貨幣是唯一指定的報表貨幣。  
  
> [!NOTE]  
>  如果選取此選項，[指定報表貨幣] 頁面就不會出現。  
  
 例如，樞紐貨幣可以設定為美元 (USD)，而事實資料表則以歐元 (EUR)、澳幣 (AUD) 和墨西哥披索 (MXN) 儲存交易。 選取此選項會將這些交易從指定的本地貨幣轉換為樞紐貨幣。 如此一來，交易就可以儲存為指定的本地貨幣，並以指定的樞紐貨幣來檢視。  
  
 **一對多**  
 使用 [設定貨幣轉換選項] 頁面中指定的樞紐貨幣來儲存交易，然後轉換成一或多種其他的報表貨幣。  
  
> [!NOTE]  
>  如果選取此選項，[定義本地貨幣參考] 頁面就不會出現。  
  
 例如，樞紐貨幣可以設定為美元 (USD)，而事實資料表將以 USD 儲存交易。 選取此選項會將這些交易從樞紐貨幣轉換為指定的報表貨幣。 如此一來，交易就可以儲存為指定的樞紐貨幣，並以指定的樞紐貨幣來檢視，或以 **[指定報表貨幣]** 頁面中指定的任何報表貨幣來檢視。  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧精靈 F1 說明](business-intelligence-wizard-f1-help.md)   
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [維度設計師&#40;Analysis Services-多維度資料&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
