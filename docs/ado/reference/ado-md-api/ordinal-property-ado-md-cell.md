---
title: Ordinal 屬性 (ADO MD Cell) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c4a40c59ad222c943cefe089ffaddd53f2cec25a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708821"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 屬性 (ADO MD Cell)
可唯一識別[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)資料格集內的位置。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數和處於唯讀狀態。  
  
## <a name="remarks"></a>備註  
 儲存格的序數的值可唯一識別資料格集內的儲存格。 就概念而言，資料格會編號資料格集中，好像 cellset *p*-維陣列，其中*p*數目[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)。 資料格會從零以列為主要順序開始進行編號。 以下是計算資料格序數的公式：  
  
 儲存格的序數的值可以搭配[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件，以便快速擷取[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)。  
  
## <a name="applies-to"></a>適用於  
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 範例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [項目屬性 (ADO MD Cellset)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 屬性 (ADO MD Position)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
