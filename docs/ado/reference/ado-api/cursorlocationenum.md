---
title: CursorLocationEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: rothja
ms.author: jroth
ms.openlocfilehash: 278f69e504ed4af7589b7e2be2c281e5de5957fa
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760174"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定資料指標服務的位置。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用本機資料指標程式庫所提供的用戶端資料指標。 本機資料指標服務通常會允許驅動程式提供的資料指標可能不會有許多功能，因此使用此設定可能會提供將啟用之功能的相關優勢。 為了回溯相容性，也支援同義字**adUseClientBatch** 。|  
|**adUseNone**|1|不會使用資料指標服務。 （這個常數已經過時，只是為了回溯相容性而顯示）。|  
|**adUseServer**|2|預設值。 使用資料提供者或驅動程式所提供的資料指標。 這些資料指標有時非常有彈性，並允許其他對資料來源所做之變更的敏感度。 不過，[適用于 OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)的某些功能，例如解除關聯<br /><br /> [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件無法使用伺服器端資料指標來模擬，而且這些功能將無法透過此設定來使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. CursorLocation. 用戶端|  
|AdoEnums. CursorLocation. NONE|  
|AdoEnums. CursorLocation. 伺服器|  
  
## <a name="applies-to"></a>套用至  
 [CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
