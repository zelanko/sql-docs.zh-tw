---
title: Delete 方法 （ADO Parameters 集合） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 644e691dcc0f6fcf024a8d56e8adf516c2c5a096
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698302"
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 (ADO Parameters 集合)
刪除的物件[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 A**字串**包含您想要刪除的物件或物件的序數位置 （索引） 的名稱在集合中的值。  
  
## <a name="remarks"></a>備註  
 使用**刪除**集合上的方法可讓您在集合中移除其中一個物件。 這個方法是僅適用於**參數**的集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 您必須使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性或其集合的索引時呼叫**刪除**方法的物件變數不是有效的引數。  
  
## <a name="applies-to"></a>適用於  
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法 (ADO Fields 集合)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
