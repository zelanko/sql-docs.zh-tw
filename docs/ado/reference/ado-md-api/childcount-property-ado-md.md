---
description: ChildCount 屬性 (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 713958259b274e779802828d1940cabf25c5c222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441200"
---
# <a name="childcount-property-ado-md"></a>ChildCount 屬性 (ADO MD)
指出目前 [成員](../../../ado/reference/ado-md-api/member-object-ado-md.md) 物件為階層中之父系的成員數目。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用 **ChildCount** 屬性來傳回 **成員** 具有多少子系的估計值。 [子](../../../ado/reference/ado-md-api/children-property-ado-md.md)系屬性可以傳回**成員**的實際子系。  
  
 針對[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件中的**成員**物件，傳回的最大數目是65536。 如果子系的實際數目超過65536，則傳回的值仍會是65536。 因此，應用程式應該將65536的 **ChildCount** 解讀為等於或大於65536個子系。  
  
 針對[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件，請使用**子**系集合上的 ADO collection [Count](../../../ado/reference/ado-api/count-property-ado.md)屬性來判斷確切的子係數目。 如果集合中的子係數目很大，判斷確切的子係數目可能會很慢。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [子系屬性 (ADO MD) ](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 屬性 (ADO) ](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
