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
ms.openlocfilehash: f3a72234a6d5e5cbb8e0dc9f5d625b93f15f437f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763329"
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
  
|||  
|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另請參閱  
 [NumericScale 和 Precision 屬性範例（VB）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 屬性範例（VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
