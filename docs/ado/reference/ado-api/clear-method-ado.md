---
title: "Clear 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 831ec9b295ca4e3d81707cfc2c1cc14169d1527c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
移除所有[錯誤](../../../ado/reference/ado-api/error-object.md)物件從[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>備註  
 使用**清除**方法[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)要移除所有現有集合[錯誤](../../../ado/reference/ado-api/error-object.md)從集合的物件。 ADO 錯誤發生時，會自動清除**錯誤**集合，並填滿它與**錯誤**物件會根據新的錯誤。  
  
 某些屬性和方法傳回的警告會顯示為**錯誤**中的物件**錯誤**集合但不是會停止執行程式。 之前先呼叫[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件;[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件; 或設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，呼叫**清除**方法**錯誤**集合。 這樣一來，您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
## <a name="applies-to"></a>適用於  
 [錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行，請重新查詢，並清除方法範例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [執行，請重新查詢，並清除方法範例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [執行，請重新查詢，並清除方法範例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 參數集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [篩選屬性](../../../ado/reference/ado-api/filter-property.md)   
 [重新同步處理方法](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)

