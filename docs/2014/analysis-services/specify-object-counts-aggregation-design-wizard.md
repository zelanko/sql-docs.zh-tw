---
title: 指定物件計數 （彙總設計精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a2040623e235b79a16c767062655deac81d6271
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319318"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>指定物件計數 (彙總設計精靈)
  使用 **[指定物件計數]** 頁面，即可自動計算 Cube 中的物件計數，或者手動輸入估計的計數。 「彙總設計精靈」會使用物件計數來估計儲存需求。  
  
## <a name="options"></a>選項。  
 **Cube 物件**  
 顯示 Cube 中的維度及屬性。 不需要的屬性及其`AggregationUsage`屬性設定為`None`中**檢閱彙總使用方式**精靈頁面會顯示，因為這些是唯一需要指定計數的屬性。  
  
 **估計的計數**  
 顯示量值群組中估計的資料列數目以及資料庫維度中估計的屬性成員計數。 您可以輸入要當做估計計數使用的值，也可以計算估計計數的值。 若要計算計數值，請輸入`0`個欄位，然後再按一下**計數**。 已經顯示計數的欄位不會更新。  
  
 **資料分割計數**  
 (選擇性) 輸入量值群組中估計的資料列數目並輸入資料分割中估計的屬性成員計數。  
  
 **Count**  
 針對所有空白欄位，計算並重新填入 [估計計數] 資料行的值。 已經顯示計數的欄位不會更新。  
  
## <a name="see-also"></a>另請參閱  
 [彙總設計精靈 F1 說明](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 精靈&#40;多維度資料&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
