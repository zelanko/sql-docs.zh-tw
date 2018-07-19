---
title: FilterAxis 屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: f59eeff4dc01e2f881712ca2309a83e80d785b27
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283927"
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
