---
title: 選擇增強功能 （商業智慧精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8834e8412cedbd2d97f9b5717f2e7979999a0a06
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681195"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>選擇增強功能 (商業智慧精靈)
  使用 **[選擇增強功能]** 頁面，來選擇要加入至 Cube 或維度的商業智慧增強功能。  
  
## <a name="options"></a>選項。  
 **可用的增強功能**  
 選取要加入的商業智慧增強功能。 下表列出可用的增強功能。  
  
|增強功能|描述|  
|-----------------|-----------------|  
|**定義時間智慧**|加入所選階層的其他時間檢視。 這些檢視包括某週期至今檢視、滾動平均檢視及某週期至另一週期檢視。<br /><br /> 注意:此選項是只有 cube 能夠使用。|  
|**定義帳戶智慧**|將標準的會計科目分類 (例如收入與費用) 指派給帳戶屬性的成員。<br /><br /> 如果量值的彙總函式設定為 *ByAccount*， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體就使用會計科目分類，根據時段來彙總帳戶屬性的跨成員量值。|  
|**定義維度智慧**|使用維度智慧來指定維度的標準商務類型，以及指定維度屬性的有效類型。 用戶端應用程式在分析資料時可以使用這些類型規格。|  
|**指定一元運算子**|指定一元運算子來取代預設彙總，其中與在 Cube 中所包含的父子式階層的成員相關聯。<br /><br /> 注意:此選項是只有 cube 能夠使用。|  
|**建立自訂成員公式**|建立自訂成員公式來取代預設彙總，其中與具有不同運算子的維度成員相關聯。|  
|**指定屬性排列方式**|指定所選屬性的成員如何排列。 可以依所選屬性的名稱或索引鍵，或依所選屬性之相關屬性的名稱或索引鍵來排列成員。 依預設，會依所選屬性的名稱來排列成員。|  
|**啟用維度回寫**|啟用維度結構的手動修改。 可寫入維度的更新會直接記錄在維度資料表中。|  
|**定義局部加總行為**|手動定義個別量值的彙總方法或帳戶類型屬性的成員。 如果 Cube 包含帳戶維度，您可以使用 [定義帳戶智慧] 選項來依據帳戶類型自動設定局部加總行為。<br /><br /> 注意:此選項是只有 cube 能夠使用。|  
|**定義貨幣轉換**|定義規則來轉換和分析 Cube 中的多語系資料。 使用商業智慧精靈所產生的多維度運算式 (MDX) 指令碼在 Cube 中套用轉換規則。<br /><br /> 注意:此選項是只有 cube 能夠使用。|  
  
 **說明**  
 提供所選商業智慧增強功能的簡短描述。  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧精靈 F1 說明](business-intelligence-wizard-f1-help.md)   
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [維度設計師&#40;Analysis Services-多維度資料&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
