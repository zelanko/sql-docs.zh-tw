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
ms.openlocfilehash: 7560f7f2c487f42d26d83236d824bf997b4f49d1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778147"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 屬性 (ADO MD)
指出子系是否緊接在軸上的 [成員](./member-object-ado-md.md) 後面。  
  
## <a name="return-values"></a>傳回值  
 傳回 **布林** 值，而且是唯讀的。 如果軸上沒有目前成員的子成員， **DrilledDown**會傳回**True** 。 如果目前的成員在軸上有一個或多個子成員， **DrilledDown**會傳回**False** 。  
  
## <a name="remarks"></a>備註  
 您可以使用 **DrilledDown** 屬性來判斷緊接在這個成員後面的座標軸上是否至少有一個這個成員的子系。 這項資訊在顯示成員時會很有用。  
  
 只有屬於[Position](./position-object-ado-md.md)物件的[成員](./member-object-ado-md.md)物件才支援這個屬性。 從屬於[層級](./level-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentSameAsPrev 屬性 (ADO MD)](./parentsameasprev-property-ado-md.md)