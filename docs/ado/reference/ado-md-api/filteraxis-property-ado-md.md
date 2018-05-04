---
title: FilterAxis 屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 671a56b9117ea77b479d1a0fff78729ca9c3f5ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis 屬性 (ADO MD)
指出目前的篩選器資訊[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="return-values"></a>傳回值  
 傳回[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)物件，並為唯讀。  
  
## <a name="remarks"></a>備註  
 使用**FilterAxis**屬性來傳回用來配量這些資料之維度相關資訊。 [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)屬性**軸**傳回交叉分析篩選器的維度數目。 這個座標軸通常會有一個資料列。  
  
 **軸**傳回**FilterAxis**並未包含在[座標軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [軸物件 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [維度物件 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount 屬性 (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
