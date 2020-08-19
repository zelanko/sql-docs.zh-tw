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
ms.openlocfilehash: beb6afdd93d69ea920acee3840dc6c0bc44d181e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444240"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件中使用的資料指標類型。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用動態資料指標。 其他使用者可以看到新增、變更和刪除專案，並允許透過 **記錄集** 的所有類型移動，但如果提供者不支援書簽，則會允許所有類型的移動。|  
|**adOpenForwardOnly**|0|預設值。 使用順向資料指標。 與靜態資料指標相同，不同之處在于您只能向前滾動記錄。 當您只需要一次通過 **記錄集**時，這樣做可改善效能。|  
|**adOpenKeyset**|1|使用索引鍵集資料指標。 和動態資料指標相同，不同之處在于您看不到其他使用者新增的記錄，但無法從您的 **記錄集**存取其他使用者所刪除的記錄。 其他使用者的資料變更仍會顯示。|  
|**adOpenStatic**|3|使用靜態資料指標，這是一組記錄的靜態複本，可用來尋找資料或產生報表。 其他使用者的新增、變更或刪除都不會顯示。|  
|**adOpenUnspecified**|-1|未指定資料指標的類型。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. CursorType 動態|  
|AdoEnums. CursorType. FORWARDONLY|  
|AdoEnums. CursorType. 索引鍵集|  
|AdoEnums. CursorType 靜態|  
|AdoEnums. CursorType。未指定|  
  
## <a name="applies-to"></a>套用至  
 [CursorType 屬性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
