---
title: "有效位數屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords: Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 866d9db49e2aeb487d38ebde085ca4ae9da197dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="precision-property-ado"></a>有效位數屬性 (ADO)
表示數值有效位數的程度[參數](../../../ado/reference/ado-api/parameter-object.md)物件或數值[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**位元組**值，指出用來代表值的數字的最大數目。  
  
## <a name="remarks"></a>備註  
 使用**精確度**屬性來判斷用來代表值的數字的數字的最大數目**參數**或**欄位**物件。  
  
 值是讀取/寫入上**參數**物件。  
  
 如**欄位**物件**精確度**是通常是唯讀。 不過，對於新**欄位**已附加至的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**精確度**是只讀取/寫入之後[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [NumericScale 和有效位數屬性範例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和有效位數屬性範例 （VC + +）](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
