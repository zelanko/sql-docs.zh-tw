---
description: ChildCount 屬性 (ADO MD)
title: ChildCount 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a5c3668a115de8137cd96f489f3e11483cb50045
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987129"
---
# <a name="childcount-property-ado-md"></a>ChildCount 屬性 (ADO MD)
指出目前 [成員](./member-object-ado-md.md) 物件為階層中之父系的成員數目。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用 **ChildCount** 屬性來傳回 **成員** 具有多少子系的估計值。 [子](./children-property-ado-md.md)系屬性可以傳回**成員**的實際子系。  
  
 針對[位置](./position-object-ado-md.md)物件中的**成員**物件，傳回的最大數目是65536。 如果子系的實際數目超過65536，則傳回的值仍會是65536。 因此，應用程式應該將65536的 **ChildCount** 解讀為等於或大於65536個子系。  
  
 針對[層級](./level-object-ado-md.md)物件的**成員**物件，請使用**子**系集合上的 ADO collection [Count](../ado-api/count-property-ado.md)屬性來判斷確切的子係數目。 如果集合中的子係數目很大，判斷確切的子係數目可能會很慢。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [子系屬性 (ADO MD) ](./children-property-ado-md.md)   
 [Count 屬性 (ADO) ](../ado-api/count-property-ado.md)   
 [Members 集合 (ADO MD)](./members-collection-ado-md.md)