---
title: MoveRecordOptionsEnum | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: eb86b01a42a097210801fd3654ff2af80df24e39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242452"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定的行為[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|預設值。 會執行預設的移動作業：如果目的地檔案或目錄已存在，而且此作業會更新超文字連結，此作業將會失敗。|  
|**adMoveOverWrite**|1|請覆寫目的地檔案或目錄，即使它已經存在。|  
|**adMoveDontUpdateLinks**|2|修改的預設行為**MoveRecord**方法不會更新來源的超文字連結**記錄**。 預設的行為取決於提供者的功能。 提供者是否能夠移動作業會更新連結。 如果提供者無法修復的連結，或未指定此值，然後移動成功，甚至當連結尚未修正。|  
|**adMoveAllowEmulation**|4|提供者嘗試模擬移動 （使用下載、 上傳和刪除作業） 的要求。 如果嘗試將移**記錄**會失敗，因為目的地 URL 是在不同的伺服器上或由不同的提供者，以比原始碼，這可能會導致增加的延遲或資料遺失，因為不同的提供者功能時提供者之間的移動資源。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
