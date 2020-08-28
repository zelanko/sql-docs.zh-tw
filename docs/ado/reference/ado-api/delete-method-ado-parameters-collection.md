---
description: Delete 方法 (ADO Parameters 集合)
title: Delete 方法 (ADO Parameters 集合) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 3860a824690d9dca469a22135d35e040cc000dca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974119"
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 (ADO Parameters 集合)
從 [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 集合中刪除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 **字串**值，包含您要刪除之物件的名稱，或物件在集合中 (索引) 的序數位置。  
  
## <a name="remarks"></a>備註  
 在集合上使用 **Delete** 方法，可讓您移除集合中的其中一個物件。 這個方法僅適用于[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的**Parameters**集合。 呼叫**Delete**方法時，您必須使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[Name](../../../ado/reference/ado-api/name-property-ado.md)屬性或其集合索引-物件變數不是有效的引數。  
  
## <a name="applies-to"></a>套用至  
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Fields 集合) 的 Delete 方法 ](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [ (ADO 記錄集的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
