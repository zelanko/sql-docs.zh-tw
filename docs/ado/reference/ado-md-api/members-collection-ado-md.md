---
title: Members 集合 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 541e1098dfd18210e7c07a0718ecd3add758c8a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659561"
---
# <a name="members-collection-ado-md"></a>Members 集合 (ADO MD)
包含[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件從一個層級或沿著座標軸的位置。  
  
## <a name="remarks"></a>備註  
 A**成員**集合用來包含下列類型的成員：  
  
-   構成 cube 中的層級的成員。 這些包含在**成員**的集合[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件。 例如，使用 從範例[概觀的多維度結構描述和資料](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)，國家 （地區） 層級的四個成員是加拿大、 美國、 英國和德國。  
  
-   成員的階層內的特定成員子系。 這些成員會傳回[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性之父代**成員**物件。 比方說，一次使用相同的範例，兩個的子系 Canada 成員是加拿大東部及加拿大-西部。  
  
-   定義座標軸上的特定位置的成員[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。 使用從 cellset[使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)做為範例，在 x 軸上的第一個位置的兩個成員是情人節和西雅圖。 這些成員包含所**成員**的集合[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件。  
  
 **成員**是標準的 ADO 集合。 使用屬性和集合的方法，您可以執行下列作業：  
  
-   取得集合中具有的物件數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   傳回集合中具有預設值的物件[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   更新的提供者從集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Members 範例 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
