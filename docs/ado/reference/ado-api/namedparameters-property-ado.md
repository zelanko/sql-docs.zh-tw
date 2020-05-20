---
title: NamedParameters 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: rothja
ms.author: jroth
ms.openlocfilehash: 432a4968a301e51c1ca69e3b84ea80e0a19e32bb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762409"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 屬性 (ADO)
指出參數名稱是否應該傳遞至提供者。  
  
## <a name="remarks"></a>備註  
 當這個屬性為 true 時，ADO 會針對[Command 物件](../../../ado/reference/ado-api/command-object-ado.md)，傳遞**參數**集合中每個參數的**Name**屬性值。 提供者會使用參數名稱來比對**CommandText**或**CommandStream**屬性中的參數。 如果此屬性為 false （預設值），則會忽略參數名稱，而提供者會使用參數的順序，將值與**CommandText**或**CommandStream**屬性中的參數比對。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CommandText 屬性（ADO）](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream 屬性（ADO）](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
