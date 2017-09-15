---
title: "Count 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 173b2fc9073676e77ad3068e9e9dc3ca76089702
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="count-property-ado"></a>Count 屬性 (ADO)
指出集合中的物件數目。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值。  
  
## <a name="remarks"></a>備註  
 使用**計數**屬性來判斷在指定集合中有多少物件。  
  
 因為集合的成員，編號從 0 開始，您應一律撰寫迴圈零的成員開始和結束值是**計數**減 1 的屬性。 如果您使用 Microsoft Visual Basic，而且想要循環集合的成員，而不檢查**計數**屬性，請使用**每個...下一步**命令。  
  
 如果**計數**屬性為零，集合中沒有任何物件。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[維度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[索引鍵集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[層級集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[成員集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[位置集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[程序集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[資料表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[使用者集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[檢視集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另請參閱  
 [計數屬性範例 (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [計數屬性範例 （VC + +）](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [重新整理方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)

