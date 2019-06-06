---
title: Count 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 10f531b601e44f346e27b52e40e6591457055ee8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698457"
---
# <a name="count-property-ado"></a>Count 屬性 (ADO)
指出集合中的物件數目。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值。  
  
## <a name="remarks"></a>備註  
 使用**計數**屬性來判斷指定的集合中有多少物件。  
  
 因為集合的成員，編號從 0 開始，您應該一律撰寫程式碼迴圈的零的成員開始和結束值是**計數**減 1 的屬性。 如果您使用 Microsoft Visual Basic，而且想要迴圈集合的成員，而不檢查**計數**屬性，請使用**每個...下一步**命令。  
  
 如果**計數**屬性為零，集合中沒有任何物件。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions 集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels 集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions 集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另請參閱  
 [Count 屬性範例 (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Count 屬性範例 （VC + +）](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
