---
title: "Delete 方法 （ADO 參數集合） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 770271da0c0b2b378adf2be5611428e05f7f5148
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 （ADO 參數集合）
刪除的物件從[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
 A**字串**值，在集合中包含您想要刪除的物件或物件的序數位置 （索引） 的名稱。  
  
## <a name="remarks"></a>備註  
 使用**刪除**集合上的方法可讓您在集合中移除其中一個物件。 這個方法是僅適用於**參數**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 您必須使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性或其集合的索引時呼叫**刪除**方法-物件變數不是有效的引數。  
  
## <a name="applies-to"></a>適用於  
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
