---
title: DrilledDown 屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8be1a63b9d4f1c979d7670c2ed3a79766070ca4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 屬性 (ADO MD)
指出是否子系緊接[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)軸上。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值而且是唯讀的。 **DrilledDown**傳回**True**如果軸上的目前成員沒有子成員。 **DrilledDown**傳回**False**如果目前成員的軸上的一個或多個子成員。  
  
## <a name="remarks"></a>備註  
 使用**DrilledDown**屬性來判斷是否有至少一個子系緊接這個成員在軸上的這個成員。 顯示成員時，此資訊會非常實用。  
  
 這個屬性才支援[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)屬於物件[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件。 從參考這個屬性時，就會發生錯誤**成員**屬於物件[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件。  
  
## <a name="applies-to"></a>適用於  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentSameAsPrev 屬性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
