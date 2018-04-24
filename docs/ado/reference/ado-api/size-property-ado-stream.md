---
title: Size 屬性 （ADO 資料流） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b1ecbc53ec085ec67b827338dbf7899245278e9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="size-property-ado-stream"></a>Size 屬性 （ADO 資料流）
表示資料流的位元組數的大小。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**值，指定的資料流大小的位元組數。 預設值是資料流，則為-1 的大小，如果不知道資料流的大小。  
  
## <a name="remarks"></a>備註  
 **大小**可以僅能搭配開啟[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
> [!NOTE]
>  任何數目的位元可以儲存在**資料流**物件，只受限於系統資源。 如果**資料流**包含更多的位元，比可以由**長**值**大小**會被截斷，因此沒有精確地表示長度**資料流**。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Size 屬性 (ADO Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
