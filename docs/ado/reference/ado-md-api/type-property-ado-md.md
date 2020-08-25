---
description: Type 屬性 (ADO MD)
title: 類型屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Type
- Type
helpviewer_keywords:
- Type property [ADO MD]
ms.assetid: 34698910-64b9-41d8-8531-9de12f2b1e32
author: rothja
ms.author: jroth
ms.openlocfilehash: 30cf3c161e30884d370aea0fefd81260bafe141e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777817"
---
# <a name="type-property-ado-md"></a>Type 屬性 (ADO MD)
指出目前 [成員](./member-object-ado-md.md)的類型。  
  
## <a name="return-values"></a>傳回值  
 傳回 [MemberTypeEnum](./membertypeenum.md) 值，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 只有屬於[層級](./level-object-ado-md.md)物件的[成員](./member-object-ado-md.md)物件才支援這個屬性。 從屬於[Position](./position-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](./member-object-ado-md.md)