---
title: "值屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17e3c9f28e42dbd70118bb29a330514a9c29e013
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="value-property-ado"></a>Value 屬性 (ADO)
指派給的值會指出[欄位](../../../ado/reference/ado-api/field-object.md)，[參數](../../../ado/reference/ado-api/parameter-object.md)，或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant**值，指出物件的值。 預設值取決於[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性。  
  
## <a name="remarks"></a>備註  
 使用**值**屬性來設定或傳回資料來源**欄位**物件，若要設定或傳回參數值與**參數**物件，或用來設定或傳回與屬性設定**屬性**物件。 是否**值**屬性是可讀寫或唯讀狀態需視許多因素： 請參閱個別物件主題，如需詳細資訊。  
  
 設定和傳回的長整數二進位資料，可讓 ADO**值**屬性。  
  
> [!NOTE]
>  如**參數**物件、 ADO 讀取**值**一次只能從提供者的屬性。 如果命令包含**參數**其**值**屬性是空的而且您建立[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)命令，請先關閉**資料錄集**之前擷取**值**屬性。 否則，對於某些提供者，**值**屬性可能為空白，且不會包含正確的值。  
>   
>  對於新**欄位**已附加至的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件**值**屬性必須設定在任何其他**欄位**可以指定屬性。 首先，為特定值**值**指派屬性必須與[更新](../../../ado/reference/ado-api/update-method.md)上**欄位**稱為集合。 然後，其他屬性，例如[類型](../../../ado/reference/ado-api/type-property-ado.md)或[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)可以存取。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[參數物件](../../../ado/reference/ado-api/parameter-object.md)|[屬性物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [值屬性範例 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)   
 [值屬性範例 （VC + +）](../../../ado/reference/ado-api/value-property-example-vc.md)   

