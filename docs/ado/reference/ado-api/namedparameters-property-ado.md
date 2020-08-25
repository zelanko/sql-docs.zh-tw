---
description: NamedParameters 屬性 (ADO)
title: " (ADO) 的 NamedParameters 屬性 |Microsoft Docs"
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
ms.openlocfilehash: b520f60f9e08c5580e2f825a76d25c2cdcda6ae0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774117"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 屬性 (ADO)
指出是否應將參數名稱傳遞給提供者。  
  
## <a name="remarks"></a>備註  
 當此屬性為 true 時，ADO 會在[命令物件](./command-object-ado.md)的**參數**集合中傳遞每個參數的**Name**屬性值。 提供者會使用參數名稱來比對 **CommandText** 或 **CommandStream** 屬性中的參數。 如果這個屬性為 false (預設) ，則會忽略參數名稱，而提供者會使用參數的順序，將值與 **CommandText** 或 **CommandStream** 屬性中的參數相符。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 CommandText 屬性 ](./commandtext-property-ado.md)   
 [ (ADO) 的 CommandStream 屬性 ](./commandstream-property-ado.md)   
 [Parameters 集合 (ADO)](./parameters-collection-ado.md)