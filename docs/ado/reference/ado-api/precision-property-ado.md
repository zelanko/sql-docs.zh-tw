---
description: Precision 屬性 (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4be9c3ae7e9f4cc8ac7f90b78b80ee96b64eaf5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442700"
---
# <a name="precision-property-ado"></a>Precision 屬性 (ADO)
指出 [參數](../../../ado/reference/ado-api/parameter-object.md) 物件或數值 [欄位](../../../ado/reference/ado-api/field-object.md) 物件中數值的精確度程度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **位元組** 值，表示用來表示值的最大位數。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **精確度** ] 屬性來決定用於表示數值 **參數** 或 **欄位** 物件值的最大位數。  
  
 此值為 **Parameter** 物件的讀取/寫入值。  
  
 對於 **Field**物件而言，有效 **位數** 通常是唯讀的。 不過，對於附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，而且資料提供者已透過呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功加入新**欄位**之後，才會讀取/寫入**精確度**。  
  
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
 [NumericScale 和 Precision 屬性範例 (VB) ](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 屬性範例 (VC + +) ](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 屬性 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
