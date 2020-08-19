---
description: MoveRecordOptionsEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 03728baab7882597cfba29d2f566d73ac98f9300
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443140"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定 [Record](../../../ado/reference/ado-api/record-object-ado.md) 物件 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) 方法的行為。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|預設值。 執行預設移動作業：如果目的地檔案或目錄已經存在，作業就會失敗，而且作業會更新超文字連結。|  
|**adMoveOverWrite**|1|覆寫目的地檔案或目錄（即使已存在）。|  
|**adMoveDontUpdateLinks**|2|藉由不更新來源**記錄**的超文字連結，修改**MoveRecord**方法的預設行為。 預設行為取決於提供者的功能。 如果提供者可以，移動作業更新連結。 如果提供者無法修正連結或未指定此值，則即使尚未修正連結，移動也會成功。|  
|**adMoveAllowEmulation**|4|要求提供者嘗試使用下載、上傳及刪除作業來模擬移動 () 。 如果嘗試移動 **記錄** 失敗，因為目的地 URL 位於不同的伺服器上，或由不同于來源的提供者提供服務，這可能會導致延遲或資料遺失，這可能會導致延遲或資料遺失，因為在提供者之間移動資源時，有不同的提供者功能。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
