---
title: "MoveRecordOptionsEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: MoveRecordOptionsEnum
helpviewer_keywords: MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d602d52933b6f940131ffbb9cbe9198e6c13699
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定的行為[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|預設值。 會執行預設移動作業： 如果目的地檔案或目錄已存在，而且此作業會更新超文字連結，則作業會失敗。|  
|**adMoveOverWrite**|1|請覆寫目的地檔案或目錄，即使它已經存在。|  
|**adMoveDontUpdateLinks**|2|修改預設行為的**MoveRecord**方法藉由不更新來源的超文字連結**記錄**。 預設的行為取決於提供者的功能。 提供者是否能夠移動作業會更新連結。 如果提供者無法修正連結，或未指定此值，然後移動會成功，即使當連結尚未修正。|  
|**adMoveAllowEmulation**|4|提供者嘗試模擬移動 （使用下載、 上傳和刪除作業） 的要求。 如果嘗試移動**記錄**會失敗，因為目的地 URL 是在不同的伺服器或服務的不同來源的提供者，這可能會導致增加的延遲或資料遺失，因為不同的提供者功能，所以當提供者之間的移動資源。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
