---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d35af0315460af8b110c7af38934e5d196a5c895
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192800"
---
# <a name="size-property-ado-stream"></a>Size 屬性 (ADO Stream)
表示資料流中的位元組數目的大小。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**值，指定的資料流大小的位元組數。 如果不知道資料流的大小，預設值是資料流，則為-1 的大小。  
  
## <a name="remarks"></a>備註  
 **大小**適用於僅開放[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
> [!NOTE]
>  可以儲存任意數目的位元**Stream**物件，只受限於系統資源。 如果**Stream**包含更多的位元比可以由**長**值**大小**截斷，並因此不會無法正確呈現長度**Stream**。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Size 屬性 (ADO Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
