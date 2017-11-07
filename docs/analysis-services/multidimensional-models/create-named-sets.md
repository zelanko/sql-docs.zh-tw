---
title: "建立命名的集 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculations [Analysis Services], named sets
- named sets [Analysis Services]
- members [Analysis Services], named sets
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a98318cc28f79ab24af1ecce382b0b39a78dfab
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-named-sets"></a>建立命名集
  命名集是維度成員集或為了重複使用而建立的集運算式，例如使用於多維度運算式 (MDX) 查詢。 您可以結合 Cube 資料、算術運算子、數字和函數來建立命名集。 例如，您可以建立一個叫作 Top Ten Factories 的命名集，包含 Factories 維度中 Production 量值最高的 10 個成員。 然後使用者可以在查詢中使用 Top Ten Factories。 例如，使用者可將 Top Ten Factories 放在一個軸上，將 Measures 維度 (包括 Production 在內) 放在另一個軸上。 如需詳細資訊，請參閱 [Calculations in Multidimensional Models](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) (多維度模型中的計算) 和 [Building Named Sets in MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md) (在 MDX 中建立命名集 (MDX))。  
  
 若要建立命名集，請在 Cube 設計師的 **[計算]** 索引標籤上，使用 **[新增命名集]** 命令。 可在 **[計算]** 索引標籤工具列的 **[Cube]** 功能表上叫用此命令。 此命令顯示一個表單來指定命名集的下列選項：  
  
 **名稱**  
 選取命名集的名稱。 使用者瀏覽 Cube 時出現的名稱。  
  
 **運算式**  
 指定產生命名集的運算式。 可以用 MDX 撰寫此運算式。 運算式可以包含下列任一項：  
  
-   代表 Cube 元件 (例如維度、層級、量值等等) 的資料運算式。  
  
-   算術運算子。  
  
-   數字。  
  
-   函數。  
  
 您可以從 **[計算工具]** 窗格的 **[中繼資料]** 索引標籤中，將 Cube 元件複製或拖曳至 **[命名集表單編輯器]** 窗格的 **[運算式]** 方塊中。 您可以從 **[計算工具]** 窗格的 **[函數]** 索引標籤中，將函數複製或拖曳至 **[命名集表單編輯器]** 窗格的 **[運算式]** 方塊中。  
  
> [!IMPORTANT]  
>  如果您建立集運算式時，是明確地將集裡的成員命名，請利用一對大括號 ({}) 將成員清單括住。  
  
## <a name="see-also"></a>請參閱＜  
 [Calculations in Multidimensional Models](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  

