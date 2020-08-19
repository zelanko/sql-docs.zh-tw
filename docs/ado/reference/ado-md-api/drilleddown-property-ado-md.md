---
description: DrilledDown 屬性 (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 132b1a7210a9fd37866f1a150430f0d1a6d29606
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441040"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 屬性 (ADO MD)
指出子系是否緊接在軸上的 [成員](../../../ado/reference/ado-md-api/member-object-ado-md.md) 後面。  
  
## <a name="return-values"></a>傳回值  
 傳回 **布林** 值，而且是唯讀的。 如果軸上沒有目前成員的子成員， **DrilledDown**會傳回**True** 。 如果目前的成員在軸上有一個或多個子成員， **DrilledDown**會傳回**False** 。  
  
## <a name="remarks"></a>備註  
 您可以使用 **DrilledDown** 屬性來判斷緊接在這個成員後面的座標軸上是否至少有一個這個成員的子系。 這項資訊在顯示成員時會很有用。  
  
 只有屬於[Position](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件才支援這個屬性。 從屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentSameAsPrev 屬性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
