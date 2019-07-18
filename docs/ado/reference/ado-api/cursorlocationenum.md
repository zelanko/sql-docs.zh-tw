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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3af18120af91fe06da48c2e3636bf8a7c572161
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919296"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定資料指標服務的位置。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用本機資料指標程式庫所提供的用戶端資料指標。 本機資料指標服務通常可讓驅動程式提供的資料指標不是，可能的許多功能而使用這項設定可能會提供一項優點對於將啟用的功能。 回溯相容性，同義字**adUseClientBatch**也支援。|  
|**adUseNone**|1|不使用資料指標服務。 （這個常數已經過時，僅為了回溯相容性會出現）。|  
|**adUseServer**|2|預設值。 使用提供的資料提供者或驅動程式的資料指標。 這些資料指標時有時候相當有彈性，並允許其他人對資料來源所做變更的其他敏感性。 不過，某些功能[OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)，例如解除關聯<br /><br /> [資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)無法模擬與伺服器端資料指標的物件，以及這些功能將無法使用這項設定。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>適用於  
 [CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
