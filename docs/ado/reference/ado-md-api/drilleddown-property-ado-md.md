---
title: DrilledDown 屬性（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: f1175d2a70c376e3da1e079e4a3eb93a39235758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938463"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 屬性 (ADO MD)
指出子系是否緊接在軸的[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)後面。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值，而且是唯讀的。 如果軸上沒有目前成員的子成員，則**DrilledDown**會傳回**True** 。 如果目前成員在軸上有一個或多個子成員，則**DrilledDown**會傳回**False** 。  
  
## <a name="remarks"></a>備註  
 您可以使用**DrilledDown**屬性，判斷這個成員緊接在此成員的軸上，是否至少有一個子系。 此資訊在顯示成員時很有用。  
  
 只有屬於[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件才支援這個屬性。 當這個屬性是從屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件參考時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentSameAsPrev 屬性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
