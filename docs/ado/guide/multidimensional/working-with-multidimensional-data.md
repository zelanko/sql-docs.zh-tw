---
title: 使用多維度資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61f3e34af2a9331118b41657cf958021b972b04a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923136"
---
# <a name="working-with-multidimensional-data"></a>使用多維度資料
A*資料格集*是多維度資料的查詢的結果。 它包含的軸、 通常不超過四個座標軸通常只有兩個或三個集合。 *軸*是用來找出或篩選 cube 中的特定值的一或多個維度的成員集合。  
  
 A*位置*是沿著座標軸的點。 座標軸的單一維度所組成，這些位置會是維度成員的子集。 如果座標軸包含一個以上的維度，則每個位置是複合實體，其具有*n*組件的位置*n*會導向該軸的維度數目。 位置的每個部分是一個的構成維度的成員。  
  
 例如，如果 cube 包含銷售資料的地理位置和產品維度由沿著 x 軸的資料格集，沿著此軸的位置可能包含的成員，「 美國 」 和 「 電腦 」。 在此範例中，判斷沿著 x 軸的位置，需要在每個維度的成員為導向的軸。  
  
 A*儲存格*是位於軸座標為單位的交集處的物件。 每個資料格具有多個與其相關聯，包括資料本身、 格式化的字串 （資料格資料的可顯示的形式），以及資料格序數的值的資訊片段。 （每個資料格會是唯一的序數值，在資料格集。 資料格集的第一個資料格中的序數值為零，而最左儲存格，具有八個資料行的資料格集的第二個資料列中會有八個章節的序數值。）  
  
 例如，cube 會有下列六個維度 (請注意此 cube 的結構描述稍有不同所提供的範例[概觀的多維度結構描述和資料](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   銷售人員  
  
-   地理位置 （自然階層）-大陸、 國家/地區、 州等等  
  
-   季-季數個月，天  
  
-   Years  
  
-   量值-銷售、 PercentChange BudgetedSales  
  
-   產品  
  
 下列資料格集表示 1991 適用於所有的產品銷售：  
  
> [!NOTE]
>  在範例中資料格的值可視為排序的配對，其中第一個數字代表 x 軸的位置和 y 軸位置的第二位數的座標軸位置序數。  
  
 此資料格集的特性如下所示：  
  
-   座標軸維度：季銷售人員，地理位置  
  
-   篩選的維度：量值、 年，產品  
  
-   兩個座標軸：（x 或 0 軸） 的資料行和資料列 （y 或軸 1）  
  
-   x 軸： 兩個巢狀維度，銷售人員和地理位置  
  
-   y 軸：季中的維度  
  
 X 軸有兩個巢狀的維度：銷售人員和地理位置。 從地理位置，會選取四個成員：西雅圖、 波士頓舉行，美國南部和日本。 從銷售人員，會選取兩個成員：情人和 Nash。 這會產生此軸 (8 = 4 * 2) 上為 8 個位置的總計。  
  
 每個座標被以含有兩個成員-一個銷售人員維度中，從 [Geography] 維度的另一個位置：  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸只能有一個維度，其中包含下列八個位置：  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 資料格集、 資料格、 軸和位置全都被以 ADO MD 中對應的物件：[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)，[資料格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度的結構描述和資料的概觀](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
