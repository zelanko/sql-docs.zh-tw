---
title: MoveRecordOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcdb825073b267c3e3351001ecc7b11c969582e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932040"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定[Record](../../../ado/reference/ado-api/record-object-ado.md)物件[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法的行為。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|預設值。 執行預設的移動作業：如果目的地檔案或目錄已經存在，作業就會失敗，而且作業會更新超文字連結。|  
|**adMoveOverWrite**|1|覆寫目的地檔案或目錄，即使它已經存在。|  
|**adMoveDontUpdateLinks**|2|藉由不更新來源**記錄**的超文字連結，修改**MoveRecord**方法的預設行為。 預設行為取決於提供者的功能。 如果提供者能夠運作，請移動作業更新連結。 如果提供者無法修正連結，或未指定此值，則即使未修正連結，移動也會成功。|  
|**adMoveAllowEmulation**|4|要求提供者嘗試模擬移動（使用下載、上傳和刪除作業）。 如果嘗試移動**記錄**失敗，因為目的地 URL 位於不同的伺服器上，或由不同于來源的提供者所服務，這可能會造成延遲或資料遺失增加，因為在提供者之間移動資源時，有不同的提供者功能。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
