---
title: CreateParameter 方法 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b67abec7ab37d16ed6a444d5355412dd4dff5e03
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="createparameter-method-ado"></a>CreateParameter 方法 (ADO)
建立新[參數](../../../ado/reference/ado-api/parameter-object.md)具有指定之屬性的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**參數**物件。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 選擇性。 A**字串**值，包含名稱**參數**物件。  
  
 *型別*  
 選擇性。 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，指定的資料型別**參數**物件。  
  
 *方向*  
 選擇性。 A [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值，指定的型別**參數**物件。  
  
 *大小*  
 選擇性。 A**長**字元或位元組中指定的參數值的最大長度的值。  
  
 *值*  
 選擇性。 A **Variant**所指定的值**參數**物件。  
  
## <a name="remarks"></a>備註  
 使用**CreateParameter**方法來建立新**參數**具有指定的名稱、 類型、 方向、 大小和值物件。 您傳遞引數中的任何值會寫入至對應**參數**屬性。  
  
 這個方法不會自動附加**參數**物件**參數**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 這可讓您設定其他屬性，當您附加時，將會驗證其值 ADO**參數**物件加入至集合。  
  
 如果您指定的可變長度資料型別*類型*引數，您必須傳遞*大小*引數或組[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性**參數**之前附加到物件**參數**集合; 否則就會發生錯誤。  
  
 如果您指定的數值資料類型 (**adNumeric**或**adDecimal**) 中*類型*引數，則您也必須設定[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)和[精確度](../../../ado/reference/ado-api/precision-property-ado.md)屬性。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [附加和 CreateParameter 方法範例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [附加和 CreateParameter 方法範例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [參數物件](../../../ado/reference/ado-api/parameter-object.md)   
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
