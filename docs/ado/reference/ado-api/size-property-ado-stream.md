---
title: Size 屬性（ADO Stream） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e52d05cdbc0fe0ca397c3a7b417fec72703b8e1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916929"
---
# <a name="size-property-ado-stream"></a>Size 屬性 (ADO Stream)
以位元組數表示資料流程的大小。  
  
## <a name="return-values"></a>傳回值  
 傳回**Long**值，指定資料流程的大小（以位元組數為單位）。 預設值是資料流程的大小，如果資料流程的大小不已知，則為-1。  
  
## <a name="remarks"></a>備註  
 **大小**只能搭配開啟的[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件使用。  
  
> [!NOTE]
>  任何數目的位都可以儲存在**資料流程**物件中，只受限於系統資源。 如果**資料流程**所包含的位數超過可由**長**數值表示的位數，則會截斷**大小**，因此無法正確呈現**資料流程**的長度。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Size 屬性 (ADO 參數)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
