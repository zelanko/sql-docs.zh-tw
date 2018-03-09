---
title: "使用多維度資料 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c96d7fda2e02aeefa6225f1cea602f6ed6c7dc2e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="working-with-multidimensional-data"></a>使用多維度資料
A*資料格集*是多維度資料查詢的結果。 它包含的軸，通常是四個以上的座標軸和通常只有兩個或三個集合。 *軸*是用來尋找或篩選在 cube 中的特定值的一個或多個維度成員集合。  
  
 A*位置*沿著軸的點。 為座標軸單一維度所組成，這些位置會是維度成員的子集。 如果座標軸包含一個以上的維度，則每個位置是複合的實體，其具有 *n* 部分 where  *n* 是該軸方向的維度數目。 位置的每個部分是從一個的構成維度成員。  
  
 例如，如果 cube 包含銷售資料的地理位置和產品維度由沿著 x 軸的資料格集，沿著此軸的位置可能包含成員，「 美國 」 和 「 電腦 」。 在此範例中，判斷沿著 x 軸的位置，需要從每個維度的成員軸方向。  
  
 A*儲存格*是置於軸座標交集處的物件。 每個儲存格有多段其相關資訊，包括資料本身、 格式化的字串 （資料格資料的可顯示的形式），以及資料格序數的值。 （每個資料格是唯一的序數值，集中的資料格。 資料格集的第一個資料格中的序數值為零，最左邊的資料格，具有八個資料行的資料格集的第二個資料列中會有八個的序數值。）  
  
 例如，cube 會有下列六個維度 (請注意此 cube 的結構描述與稍微不同提供的範例[概觀的多維度結構描述和資料](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Salesperson  
  
-   地理位置 （也就是自然階層） — 大陸、 國家/地區、 州等等  
  
-   季 — 季、 月、 日  
  
-   Years  
  
-   量值，Sales，PercentChange，BudgetedSales  
  
-   產品  
  
 下列資料格集的所有產品的 1991年代表銷售：  
  
> [!NOTE]
>  在範例中的資料格值可視為座標軸位置序數，其中第一個數字代表 x 軸位置和 y 軸位置的第二位數的排序配對。  
  
 此資料格集的特性是，如下所示：  
  
-   座標軸維度： 季銷售人員，地理位置  
  
-   篩選的維度： 量值、 年的產品  
  
-   兩個座標軸: （x 或軸 0） 的資料行和資料列 （y 或軸 1）  
  
-   x 軸： 兩個巢狀維度銷售人員和地理位置  
  
-   y 軸： 季維度  
  
 X 軸有兩個巢狀的維度： 銷售人員和地理位置。 從地理位置，選取四個成員： 西雅圖、 波士頓美國南部和 （日文）。 從銷售人員選取兩個成員： 情人和 Nash。 這會產生總數 (8 = 4 * 2) 此座標軸上為 8 個位置。  
  
 每個座標以含有兩個成員的位置，從 「 銷售人員 」 維度，從 [Geography] 維度的另一個：  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸有只有一個維度，其中包含下 8 個位置：  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 資料格集、 資料格、 軸和位置全都是以 ADO MD 中對應的物件：[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)，[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
