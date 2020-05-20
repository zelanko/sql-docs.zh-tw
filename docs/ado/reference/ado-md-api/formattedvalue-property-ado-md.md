---
title: FormattedValue 屬性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1acc577b1822beb69826120034ffa4872e60c60b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764239"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue 屬性 (ADO MD)
表示[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)值的格式化顯示。  
  
## <a name="return-values"></a>傳回值  
 傳回**字串**，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 使用**FormattedValue**屬性，即可取得資料[格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)物件之[value](../../../ado/reference/ado-md-api/value-property-ado-md.md)屬性的格式化顯示值。 例如，如果儲存格的值為1056.87，而此值表示貨幣金額，則**FormattedValue**會是 $1056.87。  
  
## <a name="applies-to"></a>套用至  
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [格集範例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Value 屬性 (ADO MD)](../../../ado/reference/ado-md-api/value-property-ado-md.md)
