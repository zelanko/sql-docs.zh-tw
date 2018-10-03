---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 059d6bb8e621839ccf21bb4eb4251db08f427523
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761396"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
指定資料指標中所使用的型別[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|使用動態資料指標。 新增、 變更及刪除由其他使用者是可見的而所有類型的移動**資料錄集**允許，除了書籤，如果提供者不支援。|  
|**adOpenForwardOnly**|0|預設值。 使用順向資料指標。 相同的靜態資料指標，，不同之處在於您可以只捲動轉寄資料錄。 這可改善效能，當您需要只執行一次通過**資料錄集**。|  
|**adOpenKeyset**|1|使用索引鍵集資料指標。 讓動態資料指標，不同之處在於雖然從無法存取其他使用者刪除的記錄，您無法看到其他使用者新增，記錄您**資料錄集**。 由其他使用者的資料變更是仍然可見。|  
|**adOpenStatic**|3|使用靜態資料指標，也就是靜態的一組可用來尋找資料，或產生報表的記錄複本。 新增、 變更或刪除由其他使用者不會顯示。|  
|**adOpenUnspecified**|-1|未指定資料指標的類型。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
 [CursorType 屬性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
