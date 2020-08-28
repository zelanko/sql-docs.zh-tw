---
description: Item 屬性 (ADO MD Cellset)
title: 專案屬性 (ADO MD 格集) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: rothja
ms.author: jroth
ms.openlocfilehash: 997777e853a54ae56175b4b5795087e67079813b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986599"
---
# <a name="item-property-ado-md-cellset"></a>Item 屬性 (ADO MD Cellset)
使用它的座標，從資料格 [集](./cellset-object-ado-md.md) 抓取儲存格。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>參數  
 *Positions*  
 可唯一指定儲存格的值 **>variantarray** 。 *位置* 可以是下列其中一項：  
  
-   位置編號的陣列  
  
-   成員名稱的陣列  
  
-   序數位置  
  
## <a name="remarks"></a>備註  
 使用**Item**屬性可傳回資料格[集](./cellset-object-ado-md.md)物件內的[Cell](./cell-object-ado-md.md)物件。 如果 **專案** 屬性找不到對應至 *位置* 引數的資料格，就會發生錯誤。  
  
 **Item**屬性是 [**儲存格**] 物件的預設屬性。 下列語法形式可以互換：  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
 *位置*引數會指定要傳回的資料格。 您可以依序數位置或沿著每個軸的位置來指定資料格。 依每個軸的位置指定資料格時，您可以針對每個位置指定位置的數值或成員的名稱。  
  
 序數位置是可唯一識別資料格 **集**內一個資料格的數位。 在概念上，資料格會在 **資料格集中編號，如同資料** 格 **集** 是一種 *p*維陣列，其中 *p* 是軸的數目。 資料格的處理順序是以資料列為主。 以下是計算資料格序數的公式：  
  
 如果成員名稱是以字串的形式傳遞至 **專案**，則成員必須以數值軸識別碼的遞增順序列出。 在座標軸內，成員必須以維度嵌套的遞增順序列出，也就是最外層的維度成員最先出現，後面接著內部維度的成員。 每個維度都應該以個別的字串表示，而成員字串清單應以逗號分隔。  
  
> [!NOTE]
>  您的資料提供者可能不支援依成員名稱抓取資料格。 如需詳細資訊，請參閱提供者的檔。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料格物件 (ADO MD) ](./cell-object-ado-md.md)   
 [Cellset 物件 (ADO MD)](./cellset-object-ado-md.md)