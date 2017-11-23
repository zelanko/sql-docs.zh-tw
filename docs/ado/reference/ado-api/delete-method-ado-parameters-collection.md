---
title: "Delete 方法 （ADO 參數集合） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords: Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b58c32020f5a73f293fe0bd679e253e3bcad0ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="delete-method-ado-parameters-collection"></a>Delete 方法 （ADO 參數集合）
刪除的物件從[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 A**字串**值，在集合中包含您想要刪除的物件或物件的序數位置 （索引） 的名稱。  
  
## <a name="remarks"></a>備註  
 使用**刪除**集合上的方法可讓您在集合中移除其中一個物件。 這個方法是僅適用於**參數**集合[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 您必須使用[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性或其集合的索引時呼叫**刪除**方法-物件變數不是有效的引數。  
  
## <a name="applies-to"></a>適用於  
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>請參閱＜  
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
