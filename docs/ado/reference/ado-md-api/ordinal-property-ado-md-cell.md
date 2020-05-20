---
title: Ordinal 屬性（ADO MD 資料格） |Microsoft Docs
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
ms.openlocfilehash: b0563912d49ba6baff085fd83be88693e8f8ba1f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765069"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 屬性 (ADO MD Cell)
在資料格集內依其位置唯一識別資料[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 資料格的序數值可唯一識別資料格集內的資料格。 在概念上，資料格集的編號會如同資料格集是一個*p*維陣列，其中*p*是[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)的數目。 資料格的編號是從零開始，以資料列主要順序。 以下是用來計算資料格序數的公式：  
  
 資料格的序數值可以搭配資料格[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件的[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性使用，以快速取出資料[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>套用至  
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 範例（VBScript）](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [格集物件（ADO MD）](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Item 屬性（ADO MD 格集）](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 屬性 (ADO MD Position)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
