---
title: Delete 方法（ADO Parameters 集合） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 19fb69e51e04a2e15c60767981bc32e4dfe77141
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757374"
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 (ADO Parameters 集合)
從[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合中刪除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
 **字串**值，其中包含您想要刪除之物件的名稱，或物件在集合中的序數位置（索引）。  
  
## <a name="remarks"></a>備註  
 在集合上使用**Delete**方法，可讓您移除集合中的其中一個物件。 這個方法僅適用于[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的**Parameters**集合。 呼叫**Delete**方法時，您必須使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[Name](../../../ado/reference/ado-api/name-property-ado.md)屬性或其集合索引-物件變數不是有效的引數。  
  
## <a name="applies-to"></a>套用至  
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法（ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO Recordset）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
