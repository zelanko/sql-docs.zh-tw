---
title: 限制資料列（資料分割 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4207f617b4f6fafde5392fdea013196c54501314
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547430"
---
# <a name="restrict-rows-partition-wizard"></a>限制資料列 (資料分割精靈)
  使用 [限制資料列]**** 頁面，即可限制從指定之資料表中擷取且將彙總並納入資料分割中的資料列。  
  
> [!NOTE]  
>  唯有在 [指定來源資訊]**** 頁面中選取了單一資料表之後，才會顯示此頁面。  
  
> [!CAUTION]  
>  如果在其他分割區所使用的 [指定來源資訊]**** 頁面上，指定了 [可用的資料表]**** 中的某資料表，您就必須在 [限制資料列]**** 頁面中提供查詢，或者接受在 Cube 中可能會有重複資料的風險。  
  
## <a name="options"></a>選項  
 **指定查詢來限制資料列**  
 選取即可在 [查詢]**** 方塊中，輸入限制資料列的查詢。  
  
 如果在選取此選項時，[提供 WHERE 子句]**** 是空的，該選項就會使用 SQL 陳述式，從先前選取之資料表中擷取所有的資料行與資料列來進行擴展。  
  
 **查詢**  
 鍵入或修改處理資料分割時，從資料表中擷取資料列所使用的 SQL 陳述式。  
  
> [!IMPORTANT]  
>  指定 WHERE 子句，就可以在這個資料分割使用記錄的子集。 當有多個分割區以單一事實資料表為基礎時，這是防止資料重複所必要的。  
  
 **勾選**  
 驗證 [查詢]**** 中的陳述式是否為有效的 SQL 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
