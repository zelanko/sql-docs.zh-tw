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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923136"
---
# <a name="working-with-multidimensional-data"></a>使用多維度資料
資料*格集*是針對多維度資料進行查詢的結果。 它是由一組軸組成，通常不能超過四個軸，通常只有兩個或三個。 「*軸*」是一或多個維度中的成員集合，可用來尋找或篩選 cube 中的特定值。  
  
 *位置*是沿著軸的點。 如果是由單一維度組成的軸，這些位置就是維度成員的子集。 如果軸包含一個以上的維度，則每個位置都是一個複合實體，其中 n 是以該軸為導向的維度數目 *，其中有* *n*個部分。 位置的每個部分都是來自一個組成維度的成員。  
  
 例如，如果包含銷售資料之 cube 中的 Geography 和 Product 維度是沿著資料格集的 X 軸來導向，沿著此軸的位置可能會包含成員 "USA" 和 "電腦"。 在此範例中，決定沿著 X 軸的位置時，每個維度中的成員都必須沿著軸來導向。  
  
 「資料*格*」是位於軸座標交集處的物件。 每個資料格都有與它相關聯的多個資訊片段，包括資料本身、格式化的字串（資料格資料的可顯示形式）和資料格序數值。 （每個資料格都是資料格集內的唯一序數值。 資料格集內第一個資料格的序數值為零，而包含八個數據行之資料格集的第二個數據列中最左邊的資料格，其序數值為8。）  
  
 例如，一個 cube 具有下列六個維度（請注意，這個 cube 架構與在多維度[架構和資料的總覽](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)中所提供的範例稍有不同）：  
  
-   銷售人員  
  
-   地理位置（自然階層）-大陸、國家/地區、州等等  
  
-   季、季、月、天  
  
-   Years  
  
-   量值-Sales、PercentChange、BudgetedSales  
  
-   Products  
  
 下列的儲存格代表所有產品的1991銷售額：  
  
> [!NOTE]
>  範例中的資料格值可視為軸位置序數的已排序配對，其中第一個數位代表 X 軸位置，而第二個數字則是 y 軸位置。  
  
 此格集的特性如下所示：  
  
-   軸維度：季，銷售人員，地理位置  
  
-   篩選維度：量值、年、產品  
  
-   兩個軸：資料行（x 或軸0）和資料列（y 或軸1）  
  
-   X 軸：兩個嵌套維度、銷售人員和地理位置  
  
-   y 軸：季維度  
  
 X 軸有兩個嵌套維度：銷售人員和地理位置。 從地理位置選取四個成員：西雅圖、波士頓、美國南部和日本。 從銷售人員選取兩個成員：情人節和 Nash。 這會產生此軸上總共八個位置（8 = 4 * 2）。  
  
 每一個座標都會表示為具有兩個成員的位置-一個是來自「銷售人員」維度，另一個是「Geography」維度：  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸只有一個維度，其中包含下列八個位置：  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 資料格集、資料格、軸和位置都會以對應的物件 ADO MD 表示：資料格[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)、資料[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度）（ADO MD）](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多維度架構和資料的總覽](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [搭配 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
