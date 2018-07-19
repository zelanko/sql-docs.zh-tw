---
title: Description 屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b073b4719de6554159947502a525d242f37e6707
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284067"
---
# <a name="description-property-ado-md"></a>Description 屬性 (ADO MD)
傳回目前物件的文字說明。  
  
## <a name="return-values"></a>傳回值  
 傳回**字串**和處於唯讀狀態。  
  
## <a name="remarks"></a>備註  
 如[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件**描述**僅適用於量值和公式的成員。 **描述**會傳回空字串 ("") 的所有其他類型的成員。 如需各種類型的成員的詳細資訊，請參閱[類型](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性。  
  
 這個屬性才支援**成員**屬於物件[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件。 從參考這個屬性時，就會發生錯誤**成員**屬於物件[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[CubeDef 物件 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Dimension 物件 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Hierarchy 物件 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Level 物件 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
