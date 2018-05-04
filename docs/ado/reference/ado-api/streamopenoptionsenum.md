---
title: StreamOpenOptionsEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2594a0a2095d49a0819b21967ee7e2a45c8337c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定選項，開啟[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。 值可以與 OR 運算結合。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|開啟**資料流**處於非同步模式下的物件。|  
|**adOpenStreamFromRecord**|4|識別的內容*來源*參數必須為已開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 預設行為是將視為*來源*為直接指向的節點在樹狀結構中的 URL。 會開啟與該節點相關聯的預設資料流。|  
|**adOpenStreamUnspecified**|-1|預設值。 指定開啟**資料流**預設選項的物件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
