---
description: CursorOptionEnum
title: CursorOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a14102f57f2b328314e20e4124ca7e78258fb7e0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974349"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
指定 [支援](./supports-method.md) 方法應該測試的功能。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|支援 [AddNew](./addnew-method-ado.md) 方法來加入新的記錄。|  
|**adApproxPosition**|0x4000|支援 [AbsolutePosition](./absoluteposition-property-ado.md) 和 [AbsolutePage](./absolutepage-property-ado.md) 屬性。|  
|**adBookmark**|0x2000|支援 [書簽](./bookmark-property-ado.md) 屬性以取得特定記錄的存取權。|  
|**adDelete**|0x1000800|支援刪除記錄的 [delete](./delete-method-ado-recordset.md) 方法。|  
|**adFind**|0x80000|支援 [Find](./find-method-ado.md) 方法以找出 [記錄集中](./recordset-object-ado.md)的資料列。|  
|**adHoldRecords**|0x100|抓取更多記錄或變更下一個位置，而不認可所有暫止的變更。|  
|**adIndex**|0x100000|支援 [索引](./index-property.md) 屬性來命名索引。|  
|**adMovePrevious**|0x200|支援 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 和 [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 方法，並 [移動](./move-method-ado.md) 或 [GetRows](./getrows-method-ado.md) 方法將目前的記錄位置向後移動，而不需要書簽。|  
|**adNotify**|0x40000|表示基礎資料提供者支援通知 (判斷是否支援) 的 **記錄集** 事件。|  
|**adResync**|0x20000|支援重新 [同步](./resync-method.md) 處理方法，以基礎資料庫中可見的資料來更新資料指標。|  
|**adSeek**|0x200000|支援 [Seek](./seek-method.md) 方法來尋找 **記錄集中**的資料列。|  
|**adUpdate**|0x1008000|支援修改現有資料的 [Update](./update-method.md) 方法。|  
|**adUpdateBatch**|0x10000|支援批次更新 ([UpdateBatch](./updatebatch-method.md) 和 [CancelBatch](./cancelbatch-method-ado.md) 方法) 將變更的群組傳輸到提供者。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
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
 [Supports 方法](./supports-method.md)