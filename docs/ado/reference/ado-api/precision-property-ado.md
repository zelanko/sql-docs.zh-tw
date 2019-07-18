---
title: Precision 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26da0367e494bd74253b904393a2dad62308a608
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931633"
---
# <a name="precision-property-ado"></a>Precision 屬性 (ADO)
表示數值有效位數的程度[參數](../../../ado/reference/ado-api/parameter-object.md)物件或數值[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**位元組**值，指出用來代表值的數字的最大數目。  
  
## <a name="remarks"></a>備註  
 使用**有效位數**屬性來判斷用來表示一個數字值的數字的最大數目**參數**或是**欄位**物件。  
  
 值會是讀取/寫入 on**參數**物件。  
  
 針對**欄位**物件，**精確度**是通常是唯讀。 不過，對於新**欄位**附加到的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**精確度**是只讀取/寫入之後[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>另請參閱  
 [NumericScale 和 Precision 屬性範例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 屬性範例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
