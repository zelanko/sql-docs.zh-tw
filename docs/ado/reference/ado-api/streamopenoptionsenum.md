---
title: "StreamOpenOptionsEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 268d495d2163d03244a6bec57762b93a26ab32ea
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定選項，開啟[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。 值可以與 OR 運算結合。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|開啟**資料流**處於非同步模式下的物件。|  
|**adOpenStreamFromRecord**|4|識別的內容*來源*參數必須為已開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 預設行為是將視為*來源*為直接指向的節點在樹狀結構中的 URL。 會開啟與該節點相關聯的預設資料流。|  
|**adOpenStreamUnspecified**|-1|預設值。 指定開啟**資料流**預設選項的物件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)
