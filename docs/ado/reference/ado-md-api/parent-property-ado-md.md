---
description: Parent 屬性 (ADO MD)
title: 父屬性 (ADO MD) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c599bd75388dc0b2ea7e4a5c16f495817f917ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440790"
---
# <a name="parent-property-ado-md"></a>Parent 屬性 (ADO MD)
指出成員是階層中目前 [成員](../../../ado/reference/ado-md-api/member-object-ado-md.md) 的父系。  
  
## <a name="return-values"></a>傳回值  
 傳回 [成員](../../../ado/reference/ado-md-api/member-object-ado-md.md) 物件，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 位於階層最上層 (根) 沒有父系的成員。 只有屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件才支援這個屬性。 從屬於[Position](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Children 屬性 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
