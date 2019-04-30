---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1e7e685e9d3f23d4d1c3317e24f63d7bdac23db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180739"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定選項，開啟[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。 值可以結合 OR 運算。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|會開啟**Stream**處於非同步模式下的物件。|  
|**adOpenStreamFromRecord**|4|識別的內容*來源*已開啟的參數[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 預設行為是將*來源*做為直接指向的節點樹狀結構中的 URL。 開啟與該節點相關聯的預設資料流。|  
|**adOpenStreamUnspecified**|-1|預設值。 指定左**Stream**物件使用預設選項。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
