---
description: Size 屬性 (ADO Stream)
title: Size 屬性 (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: rothja
ms.author: jroth
ms.openlocfilehash: 92b546b95c1033b6222a0acc99355c5e0906de21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442130"
---
# <a name="size-property-ado-stream"></a>Size 屬性 (ADO Stream)
以位元組數表示資料流程的大小。  
  
## <a name="return-values"></a>傳回值  
 傳回 **Long** 值，指定資料流程大小（以位元組數為單位）。 預設值是資料流程的大小; 如果不知道資料流程的大小，則為-1。  
  
## <a name="remarks"></a>備註  
 **大小** 只能與開啟的 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件搭配使用。  
  
> [!NOTE]
>  任何數目的位都可以儲存在 **資料流程** 物件中，僅受限於系統資源。 如果 **資料流程** 所包含的位數超過可由 **長** 數值表示的位數，則會截斷 **大小** ，因此不會正確地表示 **資料流程**的長度。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Size 屬性 (ADO 參數)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
