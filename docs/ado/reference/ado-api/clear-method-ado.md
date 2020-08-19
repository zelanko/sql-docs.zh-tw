---
description: Clear 方法 (ADO)
title: " (ADO) 的 Clear 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: rothja
ms.author: jroth
ms.openlocfilehash: 502592df71938e31ff50462878659df52c95f127
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450990"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
從[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合中移除所有[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>備註  
 在[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合上使用**Clear**方法，從集合中移除所有現有的[錯誤](../../../ado/reference/ado-api/error-object.md)物件。 發生錯誤時，ADO 會自動清除 **錯誤** 集合，並根據新的錯誤填入 **錯誤** 物件。  
  
 有些屬性和方法會傳回在**錯誤**集合中顯示為**錯誤**物件的警告，但不會終止程式的執行。 在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法之前，請先：[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件上的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法;或者，在**記錄集**物件上設定[Filter](../../../ado/reference/ado-api/filter-property.md)屬性，在**Errors**集合上呼叫**Clear**方法。 如此一來，您就可以讀取**錯誤**集合的[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性來測試傳回的警告。  
  
## <a name="applies-to"></a>套用至  
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Execute、Requery 和 Clear 方法範例) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery 和 Clear 方法範例 (VBScript) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery 和 Clear 方法範例 (VC + +) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [ (ADO) 的 CancelBatch 方法 ](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [ (ADO Fields 集合) 的 Delete 方法 ](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Parameters 集合) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [ (ADO 記錄集的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [篩選屬性](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
