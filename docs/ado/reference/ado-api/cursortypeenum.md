---
description: CursorTypeEnum
title: CursorTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e0d37d5aad3f27a61cf3ae7c8dad9b27149e09b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775467"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定 [記錄集](./recordset-object-ado.md) 物件中使用的資料指標類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用動態資料指標。 其他使用者可以看到新增、變更和刪除專案，並允許透過 **記錄集** 的所有類型移動，但如果提供者不支援書簽，則會允許所有類型的移動。|  
|**adOpenForwardOnly**|0|預設值。 使用順向資料指標。 與靜態資料指標相同，不同之處在于您只能向前滾動記錄。 當您只需要一次通過 **記錄集**時，這樣做可改善效能。|  
|**adOpenKeyset**|1|使用索引鍵集資料指標。 和動態資料指標相同，不同之處在于您看不到其他使用者新增的記錄，但無法從您的 **記錄集**存取其他使用者所刪除的記錄。 其他使用者的資料變更仍會顯示。|  
|**adOpenStatic**|3|使用靜態資料指標，這是一組記錄的靜態複本，可用來尋找資料或產生報表。 其他使用者的新增、變更或刪除都不會顯示。|  
|**adOpenUnspecified**|-1|未指定資料指標的類型。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. CursorType 動態|  
|AdoEnums. CursorType. FORWARDONLY|  
|AdoEnums. CursorType. 索引鍵集|  
|AdoEnums. CursorType 靜態|  
|AdoEnums. CursorType。未指定|  
  
## <a name="applies-to"></a>套用至  
 [CursorType 屬性 (ADO)](./cursortype-property-ado.md)