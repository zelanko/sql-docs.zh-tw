---
title: Precision 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: rothja
ms.author: jroth
ms.openlocfilehash: a7a9b9a0a8416cb47adf8d959990ba1e39c60595
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242592"
---
# <a name="precision-property-ado"></a>Precision 屬性 (ADO)
表示[參數](../../../ado/reference/ado-api/parameter-object.md)物件或數值[欄位](../../../ado/reference/ado-api/field-object.md)物件中數值的有效位數程度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**位元組**值，指出用來表示值的最大位數。  
  
## <a name="remarks"></a>備註  
 使用**Precision**屬性來判斷用來表示數值**參數**或**欄位**物件值的最大位數。  
  
 **參數**物件上的值為讀取/寫入。  
  
 對於**欄位**物件，**精確度**通常是唯讀的。 不過，對於已附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，且資料提供者已藉由呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功加入新**欄位**之後，有效**位數**才會是讀取/寫入。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Field 物件](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [NumericScale 和 Precision 屬性範例（VB）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 屬性範例（VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
