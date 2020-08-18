---
description: Ordinal 屬性 (ADO MD Cell)
title: 序數屬性 (ADO MD 資料格) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: rothja
ms.author: jroth
ms.openlocfilehash: 55db23316b4d920154f00aa3b03fb101b2382483
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440810"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 屬性 (ADO MD Cell)
依資料格集內的位置來唯一識別資料 [格](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 資料格的序數值可唯一識別資料格集內的資料格。 在概念上，資料格會在資料格集中編號，如同資料格集是一種 *p*維陣列，其中 *p* 是 [軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)的數目。 資料格的編號是從零開始，以資料列為主的順序。 以下是計算資料格序數的公式：  
  
 資料格的序數值可以與資料格[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件的[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性一起使用，以快速取得資料[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>套用至  
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的座標軸範例 ](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [ (ADO MD) 的儲存格集物件 ](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [專案屬性 (ADO MD 格集) ](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 屬性 (ADO MD Position)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
