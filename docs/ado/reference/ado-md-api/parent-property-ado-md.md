---
title: Parent 屬性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f6d6e03dd3288a5b0ca71bb9e129e1a57abf7c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949323"
---
# <a name="parent-property-ado-md"></a>Parent 屬性 (ADO MD)
表示階層中目前[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)父系的成員。  
  
## <a name="return-values"></a>傳回值  
 傳回[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 位於階層最上層（根）的成員沒有父系。 只有屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件才支援這個屬性。 當這個屬性是從屬於[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的**成員**物件參考時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Children 屬性 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
