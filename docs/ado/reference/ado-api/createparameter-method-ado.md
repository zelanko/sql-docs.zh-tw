---
title: CreateParameter 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af796c36bd2960730536ec07ac49614876311e84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933292"
---
# <a name="createparameter-method-ado"></a>CreateParameter 方法 (ADO)
使用指定的屬性，建立新的[參數](../../../ado/reference/ado-api/parameter-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**參數**物件。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 選擇性。 包含**參數**物件名稱的**字串**值。  
  
 *型別*  
 選擇性。 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，指定**參數**物件的資料類型。  
  
 *方向*  
 選擇性。 指定**參數**物件類型的[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
 *大小*  
 選擇性。 **Long**值，指定參數值的最大長度（以字元或位元組為單位）。  
  
 *ReplTest1*  
 選擇性。 **Variant** ，指定**參數**物件的值。  
  
## <a name="remarks"></a>備註  
 使用**CreateParameter**方法，以指定的名稱、類型、方向、大小和值，建立新的**參數**物件。 您在引數中傳遞的任何值都會寫入對應的**參數**屬性。  
  
 這個方法不會自動將**參數**物件附加至[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的**Parameters**集合。 這可讓您設定當您將**參數**物件附加至集合時，ADO 將驗證其值的其他屬性。  
  
 如果您在*類型*引數中指定可變長度的資料類型，則必須傳遞*大小*引數或設定**參數**物件的[size](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性，才能將它附加至**參數**集合;否則，就會發生錯誤。  
  
 如果您在*類型*引數中指定數值資料類型（**adNumeric**或**adDecimal**），則也必須設定[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)和[Precision](../../../ado/reference/ado-api/precision-property-ado.md)屬性。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Append 和 CreateParameter 方法範例（VB）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 和 CreateParameter 方法範例（VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append 方法（ADO）](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)   
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
