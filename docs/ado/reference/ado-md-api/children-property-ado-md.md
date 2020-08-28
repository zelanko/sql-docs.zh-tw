---
description: Children 屬性 (ADO MD)
title: 子系屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 7f6af5f18de07a3d9eb2f74ace77a9b4032303f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987119"
---
# <a name="children-property-ado-md"></a>Children 屬性 (ADO MD)
傳回 [成員](./members-collection-ado-md.md) 集合，其目前的 [成員](./member-object-ado-md.md) 是階層中的父代。  
  
## <a name="return-values"></a>傳回值  
 傳回 **成員** 集合，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 **子**系屬性包含**成員**集合，其目前的**成員**為階層式父代。 分葉層級 **成員** 物件沒有 **成員** 集合中的子成員。 只有屬於[層級](./level-object-ado-md.md)物件的**成員**物件才支援這個屬性。 從屬於[Position](./position-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ChildCount 屬性 (ADO MD)](./childcount-property-ado-md.md)