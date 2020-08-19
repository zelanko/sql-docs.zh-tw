---
description: Delete 方法 (ADO Fields 集合)
title: Delete 方法 (ADO Fields 集合) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: rothja
ms.author: jroth
ms.openlocfilehash: fb60cea6ef2e741103e94f38955bb2afc688e228
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444170"
---
# <a name="delete-method-ado-fields-collection"></a>Delete 方法 (ADO Fields 集合)
從 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 集合中刪除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>參數  
 *欄位*  
 **Variant** ，指定要刪除的[欄位](../../../ado/reference/ado-api/field-object.md)物件。 這個參數可以是 **欄位** 物件的名稱或 **欄位** 物件本身的序數位置。  
  
## <a name="remarks"></a>備註  
 呼叫 **Fields。** 在開啟的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 上的 Delete 方法會造成執行階段錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法 (ADO Parameters 集合) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [ (ADO 記錄集的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
