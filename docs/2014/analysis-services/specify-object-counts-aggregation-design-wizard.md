---
title: 指定物件計數（匯總設計嚮導） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
author: minewiskan
ms.author: owend
ms.openlocfilehash: c66b972395f86746b2d08df234db8aa0c71d03fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940319"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>指定物件計數 (彙總設計精靈)
  使用 **[指定物件計數]** 頁面，即可自動計算 Cube 中的物件計數，或者手動輸入估計的計數。 「彙總設計精靈」會使用物件計數來估計儲存需求。  
  
## <a name="options"></a>選項。  
 **Cube 物件**  
 顯示 Cube 中的維度及屬性。 在 `AggregationUsage` `None` wizard 的 [**審核匯總使用**方式] 頁面中，只有未將其屬性設定為的屬性會顯示出來，因為這些屬性是唯一需要指定計數的屬性。  
  
 **估計計數**  
 顯示量值群組中估計的資料列數目以及資料庫維度中估計的屬性成員計數。 您可以輸入要當做估計計數使用的值，也可以計算估計計數的值。 若要計算計數值，請 `0` 在欄位中輸入，然後按一下 [**計數**]。 已經顯示計數的欄位不會更新。  
  
 **分割區計數**  
 (選擇性) 輸入量值群組中估計的資料列數目並輸入資料分割中估計的屬性成員計數。  
  
 **Count**  
 針對所有空白欄位，計算並重新填入 [估計計數]**** 資料行的值。 已經顯示計數的欄位不會更新。  
  
## <a name="see-also"></a>另請參閱  
 [匯總設計嚮導 F1 說明](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
