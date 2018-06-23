---
title: 資料來源，從現有的物件 （資料來源精靈） (Analysis Services) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.datasourcewizard.specifyobject.f1
ms.assetid: e6ef6dea-9db8-45c4-8959-f9febd7caf7b
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 60f07885aff1d323cb2627e933330af3f35b8d45
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032005"
---
# <a name="data-sources-from-existing-objects-data-source-wizard-analysis-services"></a>從現有物件建立資料來源 (資料來源精靈) (Analysis Services)
  使用 **[從現有物件中建立資料來源]** 頁面，即可指定新資料來源將依據的現有資料來源或專案。  
  
## <a name="options"></a>選項。  
 **建立您的方案中現有的資料來源為基礎的資料來源**  
 選取即可將方案中的現有資料來源，作為新資料來源的依據。 建立、重新整理，或部署了使用新資料來源的專案之後，新的資料來源就會從您選取此選項時所指定的資料來源取得設定。  
  
 **資料來源**  
 從資料來源的清單 (清單是依專案來分組) 中，選取新資料來源將依據的資料來源。  
  
 **建立資料來源依據 Analysis Services 專案**  
 選取此選項，即可建立參考目前方案中之其他 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的新資料來源。 新資料來源會從所選取專案的 `TargetServer` 和 `TargetDatabase` 屬性中取得設定。 建立、重新整理，或部署了使用新資料來源的專案之後，新的資料來源就會從您選取此選項時所指定的資料來源取得設定。  
  
 **專案**  
 在新的資料來源中選取您要參考的專案。  
  
## <a name="see-also"></a>另請參閱  
 [資料來源精靈 F1 說明&#40;Analysis Services&#41;](data-source-wizard-f1-help-analysis-services.md)   
 [多維度模型中的資料來源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支援的資料來源&#40;SSAS 多維度&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  