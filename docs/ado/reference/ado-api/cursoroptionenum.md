---
title: CursorOptionEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba39c4bdc2bffc3198d780aa155e9ee60000d88a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308732"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
指定哪些功能[支援](../../../ado/reference/ado-api/supports-method.md)方法應該先進行測試。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|支援[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法來加入新的記錄。|  
|**adApproxPosition**|0x4000|支援[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)並[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性。|  
|**adBookmark**|0x2000|支援[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)屬性來存取特定的記錄。|  
|**adDelete**|0x1000800|支援[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法來刪除記錄。|  
|**adFind**|0x80000|支援[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法來找出中的資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adHoldRecords**|0x100|擷取更多記錄，或變更下一個位置，而不需要認可所有暫止的變更。|  
|**adIndex**|0x100000|支援[Index](../../../ado/reference/ado-api/index-property.md)屬性來命名的索引。|  
|**adMovePrevious**|0x200|支援[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)並[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法，並[移動](../../../ado/reference/ado-api/move-method-ado.md)或[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)向後位置移動目前的記錄方法而不需要書籤。|  
|**adNotify**|0x40000|表示基礎資料提供者支援通知 (可判斷是否**資料錄集**支援事件)。|  
|**adResync**|0x20000|支援[Resync](../../../ado/reference/ado-api/resync-method.md)方法來更新資料指標會顯示在基礎資料庫的資料。|  
|**adSeek**|0x200000|支援[Seek](../../../ado/reference/ado-api/seek-method.md)方法來找出中的資料列**資料錄集**。|  
|**adUpdate**|0x1008000|支援[更新](../../../ado/reference/ado-api/update-method.md)方法來修改現有的資料。|  
|**adUpdateBatch**|0x10000|支援批次更新 ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)並[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法) 來傳送給提供者的變更的群組。|  
  
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
