---
title: 子系屬性（ADO MD） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e52923ae428ab7b0e633049594781bd4456f9df
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764389"
---
# <a name="children-property-ado-md"></a>Children 屬性 (ADO MD)
傳回[成員](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合，其中目前[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)是階層中的父系。  
  
## <a name="return-values"></a>傳回值  
 傳回**成員**集合，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 [**子**系] 屬性包含**成員**集合，其目前**成員**為階層式父系。 分葉層級**成員**物件在**members**集合中沒有子成員。 只有屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件才支援這個屬性。 當這個屬性是從屬於[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的**成員**物件參考時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ChildCount 屬性 (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
