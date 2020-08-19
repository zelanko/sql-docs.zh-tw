---
description: 使用多維度資料
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c37f18f8bcaa3d0c1f78b3ddb8d0c6413fe7277
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452390"
---
# <a name="working-with-multidimensional-data"></a>使用多維度資料
資料 *格集* 是查詢多維度資料的結果。 它是由一組軸所組成，通常不能超過四個軸，而且通常只有兩個或三個。 *軸*是一或多個維度的成員集合，可用來尋找或篩選 cube 中的特定值。  
  
 *位置*是沿著軸的點。 針對由單一維度組成的座標軸，這些位置是維度成員的子集。 如果軸包含一個以上的維度，則每個位置都是複合實體，其具有 *n* 個部分，其中 *n* 是沿著該軸導向的維度數目。 位置的每個部分都是來自一個組成維度的成員。  
  
 例如，如果 cube 中包含銷售資料的地理位置和產品維度是沿著資料格集的 X 軸方向，則沿著此軸的位置可能會包含 "USA" 和 "電腦" 的成員。 在此範例中，沿著 X 軸決定位置需要每個維度的成員沿著軸進行導向。  
  
 資料 *格* 是位於軸座標交集處的物件。 每個資料格都有相關聯的多個資訊片段，包括資料本身、格式化的字串 (資料格資料) 的可顯示格式，以及資料格序數值。  (每個資料格都是資料格集內唯一的序數值。 資料格集的第一個資料格的序數值為零，而資料格集的第二個數據列中最左邊的資料格有八個數據行的序數值為8。 )   
  
 例如，cube 具有下列六個維度 (請注意，這個 cube 架構與在多維度 [架構和資料](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)) 的總覽中提供的範例稍有不同：  
  
-   Salesperson  
  
-   地理 (自然階層) -大陸、國家/地區、州等等  
  
-   季-季、月、日  
  
-   Years  
  
-   量值-Sales、PercentChange、BudgetedSales  
  
-   產品  
  
 下列的儲存格代表所有產品的1991銷售額：  
  
> [!NOTE]
>  範例中的資料格值可視為軸位置序數的排序配對，其中第一個數位代表 X 軸位置，而第二個數字則是 y 軸位置。  
  
 此儲存格的特性如下所示：  
  
-   軸維度：季、銷售人員、地理位置  
  
-   篩選維度：量值、年份、產品  
  
-   兩個軸：資料行 (x，或軸 0) 和資料列 (y，或軸 1)   
  
-   X 軸：兩個嵌套維度：銷售人員和地理位置  
  
-   y 軸：季維度  
  
 X 軸有兩個嵌套維度：銷售人員和地理位置。 從地理位置選取四個成員：西雅圖、波士頓、美國南部和日本。 從銷售人員選取了兩個成員：情人和 Nash。 這會在此軸上產生總共八個位置 (8 = 4 * 2) 。  
  
 每個座標都會以兩個成員的位置表示：一個來自「銷售人員」維度，另一個則是「地理位置」維度：  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸只有一個維度，其中包含下列八個位置：  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 資料格集、資料格、軸和位置全都以對應物件的 ADO MD[表示：資料格、資料](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多維度)  (ADO MD) ](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度架構和資料的總覽](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
