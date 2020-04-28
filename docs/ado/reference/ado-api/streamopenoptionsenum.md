---
title: StreamOpenOptionsEnum |Microsoft Docs
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
ms.openlocfilehash: 562e79590a2a5f1f5e9bb609b9a0ad0ea8b2bfd9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928680"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定用來開啟[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件的選項。 這些值可以與或作業結合。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|以非同步模式開啟**資料流程**物件。|  
|**adOpenStreamFromRecord**|4|將*來源*參數的內容識別為已開啟的[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 預設行為是將*Source*視為直接指向樹狀結構中之節點的 URL。 隨即開啟與該節點相關聯的預設資料流程。|  
|**adOpenStreamUnspecified**|-1|預設值。 指定以預設選項開啟**資料流程**物件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
