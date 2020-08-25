---
description: CursorLocationEnum
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
ms.openlocfilehash: 950d6310bff0bf27affe70899ba63914c9ae0ec4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775527"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定資料指標服務的位置。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用本機資料指標程式庫所提供的用戶端資料指標。 本機資料指標服務通常會允許驅動程式提供的資料指標可能不會有許多功能，因此使用此設定可提供將啟用之功能的相關優勢。 為了回溯相容性，也支援同義字 **adUseClientBatch** 。|  
|**adUseNone**|1|不使用資料指標服務。  (這個常數已過時，而且只為了回溯相容性而出現。 ) |  
|**adUseServer**|2|預設值。 使用資料提供者或驅動程式所提供的資料指標。 這些資料指標有時候具有極大的彈性，並允許對資料來源進行其他變更的敏感度。 不過，OLE DB 的 Microsoft 資料 [指標服務](../../guide/data/the-microsoft-cursor-service-for-ole-db.md)的一些功能，例如解除關聯<br /><br /> [記錄集](./recordset-object-ado.md) 物件，無法使用伺服器端資料指標進行模擬，而且這些功能將無法透過此設定使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. CursorLocation. 用戶端|  
|AdoEnums. CursorLocation。無|  
|AdoEnums. CursorLocation|  
  
## <a name="applies-to"></a>套用至  
 [CursorLocation 屬性 (ADO)](./cursorlocation-property-ado.md)