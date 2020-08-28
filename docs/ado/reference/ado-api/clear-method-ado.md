---
description: Clear 方法 (ADO)
title: " (ADO) 的 Clear 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d78980c1baee5aed1280f69c0d5224622a217ea0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975469"
---
# <a name="clear-method-ado"></a>Clear 方法 (ADO)
從[錯誤](./errors-collection-ado.md)集合中移除所有[錯誤](./error-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>備註  
 在[錯誤](./errors-collection-ado.md)集合上使用**Clear**方法，從集合中移除所有現有的[錯誤](./error-object.md)物件。 發生錯誤時，ADO 會自動清除 **錯誤** 集合，並根據新的錯誤填入 **錯誤** 物件。  
  
 有些屬性和方法會傳回在**錯誤**集合中顯示為**錯誤**物件的警告，但不會終止程式的執行。 在[記錄集](./recordset-object-ado.md)物件上呼叫[Resync](./resync-method.md)、 [UpdateBatch](./updatebatch-method.md)或[CancelBatch](./cancelbatch-method-ado.md)方法之前，請先：[Connection](./connection-object-ado.md)物件上的[Open](./open-method-ado-connection.md)方法;或者，在**記錄集**物件上設定[Filter](./filter-property.md)屬性，在**Errors**集合上呼叫**Clear**方法。 如此一來，您就可以讀取**錯誤**集合的[Count](./count-property-ado.md)屬性來測試傳回的警告。  
  
## <a name="applies-to"></a>套用至  
 [Errors 集合 (ADO)](./errors-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Execute、Requery 和 Clear 方法範例) ](./execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery 和 Clear 方法範例 (VBScript) ](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery 和 Clear 方法範例 (VC + +) ](./execute-requery-and-clear-methods-example-vc.md)   
 [ (ADO) 的 CancelBatch 方法 ](./cancelbatch-method-ado.md)   
 [ (ADO Fields 集合) 的 Delete 方法 ](./delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Parameters 集合) ](./delete-method-ado-parameters-collection.md)   
 [ (ADO 記錄集的 Delete 方法) ](./delete-method-ado-recordset.md)   
 [篩選屬性](./filter-property.md)   
 [Resync 方法](./resync-method.md)   
 [UpdateBatch 方法](./updatebatch-method.md)