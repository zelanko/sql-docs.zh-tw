---
title: Children 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 219aeba8cfc7e913a2febdd031c844aed922832e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709669"
---
# <a name="children-property-ado-md"></a>Children 屬性 (ADO MD)
傳回[成員](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合目前[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)階層中的父系。  
  
## <a name="return-values"></a>傳回值  
 傳回**成員**集合並處於唯讀狀態。  
  
## <a name="remarks"></a>備註  
 **子系**屬性包含**成員**集合目前**成員**是階層式父代。 分葉層級**成員**中的物件具有沒有子成員**成員**集合。 這個屬性才支援**成員**屬於物件[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件。 從參考這個屬性時，就會發生錯誤**成員**屬於物件[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件。  
  
## <a name="applies-to"></a>適用於  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ChildCount 屬性 (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
