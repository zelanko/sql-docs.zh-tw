---
title: 審查匯總使用方式（基於使用方式的基於優化 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.reviewaggregationusage.f1
ms.assetid: 49ce2094-c4dc-4e46-8cef-c17c5db084ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a58f7f8620924d4f707fe61c45ae87e19737471f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070164"
---
# <a name="review-aggregation-usage-usage-based-optimiation-wizard"></a>檢閱彙總使用方式 (基於使用方式的最佳化精靈)
  使用 **[檢閱彙總使用方式]** 頁面，即可設定彙總使用方式設定。  
  
## <a name="options"></a>選項。  
 **預設**  
 選取此選項，即可將屬性的彙總使用方式設定設為 Default。 透過使用這項設定，設計工具會根據屬性和維度的類型來套用預設規則。  
  
 **寫**  
 選取此選項，即可將屬性的彙總使用方式設定設為 Full。 透過使用這項設定，Cube 的每個彙總都必須包含這個屬性或在屬性鏈結中較低的相關屬性。 當某個屬性包含許多成員時，您就應該避免使用 Full 彙總使用方式設定。 如果針對多個屬性或具有許多成員的屬性指定，這項設定可能會讓彙總無法設計，因為大小過大。  
  
 **None**  
 選取此選項，即可將屬性的彙總使用方式設定設為 None。 透過使用這項設定，Cube 的任何彙總都無法包含這個屬性。  
  
 **L**  
 選取此選項，即可將屬性的彙總使用方式設定設為 Unrestricted。 透過使用這項設定，系統將不會對彙總設計師設定任何限制。 不過，此屬性仍然必須經過評估，以便判斷它是否為重要的彙總候選。  
  
 **全部設定為預設值**  
 選取此選項，即可將所有屬性的彙總使用方式設定都設為 Default。  
  
## <a name="see-also"></a>另請參閱  
 [匯總設計嚮導 F1 說明](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
