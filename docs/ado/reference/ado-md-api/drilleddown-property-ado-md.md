---
title: DrilledDown 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9021ce8b3ad4f7442650731cb60b70cd4376d78a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828206"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 屬性 (ADO MD)
指出是否子系緊接[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)軸上。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值，並處於唯讀狀態。 **DrilledDown**會傳回 **，則為 True**如果軸上的目前成員沒有子成員。 **DrilledDown**會傳回**False**如果目前成員的軸上的一個或多個子成員。  
  
## <a name="remarks"></a>備註  
 使用**DrilledDown**屬性來判斷是否有至少一個子系緊接這個成員在軸上的這個成員。 顯示成員時，這項資訊是很有用。  
  
 這個屬性才支援[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)屬於物件[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件。 從參考這個屬性時，就會發生錯誤**成員**屬於物件[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件。  
  
## <a name="applies-to"></a>適用於  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentSameAsPrev 屬性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
