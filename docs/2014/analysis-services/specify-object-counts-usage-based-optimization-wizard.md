---
title: 指定物件計數（基於使用方式的優化 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0503192c3c948110f8301c8eb375e1c8203e42f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068240"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>指定物件計數 (基於使用方式的最佳化精靈)
  使用 **[指定物件計數]** 頁面，即可自動計算 Cube 中的物件計數，或者手動輸入估計的計數。 「基於使用方式的最佳化精靈」會使用物件計數來估計儲存需求。  
  
## <a name="options"></a>選項。  
 **Cube 物件**  
 顯示 Cube 中的維度及屬性。 在 wizard 的 [**審核匯總使用**方式`AggregationUsage` ] 頁面中，只有未將其屬性設為 [無] 的屬性會顯示出來，因為這是唯一需要指定計數的屬性。  
  
 **估計計數**  
 顯示量值群組中估計的資料列數目以及資料庫維度中估計的屬性成員計數。 您可以輸入要當做估計計數使用的值，也可以計算估計計數的值。 若要計算計數值，請在欄位中輸入 0 ，然後按一下 [計數] ****。 已經顯示計數的欄位不會更新。  
  
 **分割區計數**  
 (選擇性) 輸入量值群組中估計的資料列數目以及資料分割中估計的屬性成員計數。  
  
 **計數**  
 針對所有空白欄位，計算並重新填入 [估計計數]**** 資料行的值。 已經顯示計數的欄位不會更新。  
  
## <a name="see-also"></a>另請參閱  
 [匯總設計嚮導 F1 說明](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
