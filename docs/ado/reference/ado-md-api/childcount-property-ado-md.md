---
title: ChildCount 屬性（ADO MD） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 858bed2c2fe04a1fbf0486b0e0bfc9a26447e4ef
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764399"
---
# <a name="childcount-property-ado-md"></a>ChildCount 屬性 (ADO MD)
指出目前[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件為階層中父系的成員數目。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用**ChildCount**屬性來傳回**成員**所擁有的子系的估計數目。 [子](../../../ado/reference/ado-md-api/children-property-ado-md.md)系屬性可以傳回**成員**的實際子系。  
  
 對於來自[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的**成員**物件，傳回的最大數目是65536。 如果實際的子係數目超過65536，則傳回的值仍會是65536。 因此，應用程式應該將65536的**ChildCount**解讀為等於或大於65536個子系。  
  
 對於來自[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件，請使用**子**集合的 [ADO 集合[計數](../../../ado/reference/ado-api/count-property-ado.md)] 屬性來判斷子系的確切數目。 如果集合中的子係數目很大，判斷子系的確切數目可能會變慢。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [子系屬性（ADO MD）](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 屬性（ADO）](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
