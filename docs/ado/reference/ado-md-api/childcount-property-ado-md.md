---
title: ChildCount 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01be10781c0925683ed2da9fdff24190d175fca6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611406"
---
# <a name="childcount-property-ado-md"></a>ChildCount 屬性 (ADO MD)
指出為其成員數目前[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件是階層中的父系。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數和處於唯讀狀態。  
  
## <a name="remarks"></a>備註  
 使用**ChildCount**屬性，以傳回多少的子系的估計**成員**有。 實際的子系**成員**可以由[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性。  
  
 針對**成員**物件從[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件，則傳回的最大數目為 65536。 如果子系的實際數目超過 65536，傳回的值仍會是 65536。 因此，應用程式應該解讀**ChildCount**的 65536 為等於或大於 65536 的子系。  
  
 針對**成員**物件從[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件，請使用 ADO 集合[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**子系**集合來判斷子系的確實數目。 判斷子系的確實數目可能較慢，如果在集合中的子系數目很大。  
  
## <a name="applies-to"></a>適用於  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Children 屬性 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
