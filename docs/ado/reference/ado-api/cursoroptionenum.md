---
description: CursorOptionEnum
title: CursorOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
author: rothja
ms.author: jroth
ms.openlocfilehash: 35846bf873ff98ff15e2581c36e1963b7ddcd08c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444270"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
指定 [支援](../../../ado/reference/ado-api/supports-method.md) 方法應該測試的功能。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|支援 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 方法來加入新的記錄。|  
|**adApproxPosition**|0x4000|支援 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 和 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 屬性。|  
|**adBookmark**|0x2000|支援 [書簽](../../../ado/reference/ado-api/bookmark-property-ado.md) 屬性以取得特定記錄的存取權。|  
|**adDelete**|0x1000800|支援刪除記錄的 [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 方法。|  
|**adFind**|0x80000|支援 [Find](../../../ado/reference/ado-api/find-method-ado.md) 方法以找出 [記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)的資料列。|  
|**adHoldRecords**|0x100|抓取更多記錄或變更下一個位置，而不認可所有暫止的變更。|  
|**adIndex**|0x100000|支援 [索引](../../../ado/reference/ado-api/index-property.md) 屬性來命名索引。|  
|**adMovePrevious**|0x200|支援 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 和 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 方法，並 [移動](../../../ado/reference/ado-api/move-method-ado.md) 或 [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) 方法將目前的記錄位置向後移動，而不需要書簽。|  
|**adNotify**|0x40000|表示基礎資料提供者支援通知 (判斷是否支援) 的 **記錄集** 事件。|  
|**adResync**|0x20000|支援重新 [同步](../../../ado/reference/ado-api/resync-method.md) 處理方法，以基礎資料庫中可見的資料來更新資料指標。|  
|**adSeek**|0x200000|支援 [Seek](../../../ado/reference/ado-api/seek-method.md) 方法來尋找 **記錄集中**的資料列。|  
|**adUpdate**|0x1008000|支援修改現有資料的 [Update](../../../ado/reference/ado-api/update-method.md) 方法。|  
|**adUpdateBatch**|0x10000|支援批次更新 ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 和 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 方法) 將變更的群組傳輸到提供者。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. CursorOption。 ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums. CursorOption. 書簽|  
|AdoEnums. CursorOption. DELETE|  
|AdoEnums. CursorOption. 尋找|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums. CursorOption. INDEX|  
|AdoEnums. CursorOption. MOVEPREVIOUS|  
|AdoEnums. CursorOption 通知|  
|AdoEnums. CursorOption 重新同步|  
|AdoEnums. CursorOption. SEEK|  
|AdoEnums. CursorOption. UPDATE|  
|AdoEnums. CursorOption|  
  
## <a name="applies-to"></a>套用至  
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
