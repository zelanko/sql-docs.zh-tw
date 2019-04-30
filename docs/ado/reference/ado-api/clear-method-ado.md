---
title: Clear 方法 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0e69e7d2d2a66ccb9df0e03f6f77849c502f3bf2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239751"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
移除所有[錯誤](../../../ado/reference/ado-api/error-object.md)物件從[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>備註  
 使用**清楚**方法[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)若要移除所有現有的集合[錯誤](../../../ado/reference/ado-api/error-object.md)從集合的物件。 ADO 錯誤發生時，會自動清除**錯誤**集合，並填滿它**錯誤**物件根據新的錯誤。  
  
 某些屬性和方法會傳回警告，如下所示**錯誤**中的物件**錯誤**集合，但不是會中斷程式執行。 在呼叫之前[Resync](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件;[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，或是設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，請呼叫**清除**上的方法**錯誤**集合。 如此一來，您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
## <a name="applies-to"></a>適用於  
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute、 Requery 和 Clear 方法範例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、 Requery 和 Clear 方法範例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、 Requery 和 Clear 方法範例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法 (ADO Fields 集合)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [篩選屬性](../../../ado/reference/ado-api/filter-property.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
