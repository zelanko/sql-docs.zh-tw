---
title: Value 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: 6648fcabe8890ef653558636738735a4f5e4012f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759444"
---
# <a name="value-property-ado"></a>Value 屬性 (ADO)

指出指派給[欄位](../../../ado/reference/ado-api/field-object.md)、[參數](../../../ado/reference/ado-api/parameter-object.md)或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件的值。
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回表示物件值的**變數**值。 預設值取決於[Type](../../../ado/reference/ado-api/type-property-ado.md)屬性。
  
## <a name="remarks"></a>備註

您可以使用**Value**屬性來設定或傳回**欄位**物件的資料、設定或傳回具有**參數**物件的參數值，或是設定或傳回具有**屬性**物件的屬性設定。 **Value**屬性是否為讀取/寫入或唯讀，取決於許多因素。 如需詳細資訊，請參閱個別的物件主題。

ADO 允許使用**Value**屬性來設定和傳回長二進位資料。
  
> [!NOTE]
> 針對**參數**物件，ADO 只會從提供者讀取**Value**屬性一次。 如果命令包含的**參數**的**Value**屬性是空的，而且您從命令建立[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，請確定您先關閉**記錄集**，再抓取**Value**屬性。 否則，對於某些提供者而言， **Value**屬性可能是空的，而且不會包含正確的值。
> 
> 對於已附加至[Record](../../../ado/reference/ado-api/record-object-ado.md)物件之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，必須先設定**Value**屬性，才能指定任何其他**欄位**屬性。 首先，必須已指派**value**屬性的特定值，並在呼叫的**Fields**集合上進行[更新](../../../ado/reference/ado-api/update-method.md)。 然後，可以存取其他屬性，例如[類型](../../../ado/reference/ado-api/type-property-ado.md)或[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)。
  
## <a name="applies-to"></a>套用至
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>另請參閱

[Value 屬性範例（VB）](../../../ado/reference/ado-api/value-property-example-vb.md) 
[Value 屬性範例（VC + +）](../../../ado/reference/ado-api/value-property-example-vc.md) 
