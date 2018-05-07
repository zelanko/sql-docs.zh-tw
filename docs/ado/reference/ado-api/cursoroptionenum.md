---
title: CursorOptionEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51b30e8f2ccba9dd33979f0fb3cb9cb3b6d270c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
指定哪些功能[支援](../../../ado/reference/ado-api/supports-method.md)應該先測試方法。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|支援[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，將新的記錄。|  
|**adApproxPosition**|0x4000|支援[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性。|  
|**adBookmark**|0x2000|支援[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)屬性來存取特定的記錄。|  
|**adDelete**|0x1000800|支援[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法，以刪除記錄。|  
|**adFind**|0x80000|支援[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法來找出中的資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adHoldRecords**|0x100|擷取多個記錄或變更下一個位置不認可所有暫止的變更。|  
|**adIndex**|0x100000|支援[索引](../../../ado/reference/ado-api/index-property.md)屬性命名的索引。|  
|**adMovePrevious**|0x200|支援[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)和[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法，和[移動](../../../ado/reference/ado-api/move-method-ado.md)或[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)反向位置移動目前的記錄方法而不需要書籤。|  
|**adNotify**|0x40000|表示基礎資料提供者支援通知 (可判斷是否**資料錄集**支援事件)。|  
|**adResync**|0x20000|支援[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法，以更新資料指標會顯示在基礎資料庫中的資料。|  
|**adSeek**|0x200000|支援[搜尋](../../../ado/reference/ado-api/seek-method.md)方法來找出中的資料列**資料錄集**。|  
|**adUpdate**|0x1008000|支援[更新](../../../ado/reference/ado-api/update-method.md)方法來修改現有的資料。|  
|**adUpdateBatch**|0x10000|支援批次更新 ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)和[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法) 來傳送給提供者的變更群組。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>適用於  
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
