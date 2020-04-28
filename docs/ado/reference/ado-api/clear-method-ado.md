---
title: Clear 方法（ADO） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96bd13f130966b1830d07e49633842e4154b52b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920068"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
從[Errors](../../../ado/reference/ado-api/errors-collection-ado.md)集合中移除所有[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>備註  
 請使用[Errors](../../../ado/reference/ado-api/errors-collection-ado.md)集合上的**Clear**方法，從集合中移除所有現有的[錯誤](../../../ado/reference/ado-api/error-object.md)物件。 發生錯誤時，ADO 會自動清除**錯誤**集合，並根據新的錯誤將**錯誤物件填入其中。**  
  
 某些屬性和方法會傳回**錯誤**集合中顯示為**錯誤**物件的警告，但不會暫停程式的執行。 在您呼叫[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上的[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法之前，[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件上的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法;或者，在**記錄集**物件上設定[Filter](../../../ado/reference/ado-api/filter-property.md)屬性，針對**Errors**集合呼叫**Clear**方法。 如此一來，您就可以讀取**Errors**集合的[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性來測試傳回的警告。  
  
## <a name="applies-to"></a>套用至  
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute、Requery 和 Clear 方法範例（VB）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery 和 Clear 方法範例（VBScript）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery 和 Clear 方法範例（VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法（ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法（ADO Recordset）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Filter 屬性](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
