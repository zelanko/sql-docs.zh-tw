---
description: FilterAxis 屬性 (ADO MD)
title: FilterAxis 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
author: rothja
ms.author: jroth
ms.openlocfilehash: 07bc04f345659bbaeb97f754bb00b124977276c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441030"
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis 屬性 (ADO MD)
指出目前資料 [格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)的篩選資訊。  
  
## <a name="return-values"></a>傳回值  
 傳回 [座標軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md) 物件，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用 **FilterAxis** 屬性來傳回用來分割資料之維度的相關資訊。 軸的 [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) 屬性會傳回 **交叉** 分析篩選器維度的數目。 這個軸通常只會有一個資料列。  
  
 **FilterAxis**傳回的**軸**不包含在[儲存格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件的[座標軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合中。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [軸物件 (ADO MD) ](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [維度物件 (ADO MD) ](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount 屬性 (ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
