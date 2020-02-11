---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d5cc44950754c4b63e644d2d9210edcc94bd9ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933268"
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
指定[支援](../../../ado/reference/ado-api/supports-method.md)方法應測試的功能。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|支援[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法來加入新的記錄。|  
|**adApproxPosition**|0x4000|支援[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性。|  
|**adBookmark**|0x2000|支援 [[書簽](../../../ado/reference/ado-api/bookmark-property-ado.md)] 屬性，以取得特定記錄的存取權。|  
|**adDelete**|0x1000800|支援 delete[方法來刪除記錄](../../../ado/reference/ado-api/delete-method-ado-recordset.md)。|  
|**adFind**|0x80000|支援[Find](../../../ado/reference/ado-api/find-method-ado.md)方法以尋找[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內的資料列。|  
|**adHoldRecords**|0x100|抓取更多記錄或變更下一個位置，而不認可所有暫止的變更。|  
|**adIndex**|0x100000|支援[index](../../../ado/reference/ado-api/index-property.md)屬性來命名索引。|  
|**adMovePrevious**|0x200|支援[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)和[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法，並[移動](../../../ado/reference/ado-api/move-method-ado.md)或[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)方法，將目前的記錄位置向後移動，而不需要書簽。|  
|**adNotify**|0x40000|指出基礎資料提供者支援通知（判斷是否支援**記錄集**事件）。|  
|**adResync**|0x20000|支援[Resync](../../../ado/reference/ado-api/resync-method.md)方法，以在基礎資料庫中顯示的資料來更新游標。|  
|**adSeek**|0x200000|支援[Seek](../../../ado/reference/ado-api/seek-method.md)方法以尋找**記錄集**內的資料列。|  
|**adUpdate**|0x1008000|支援修改現有資料的[Update](../../../ado/reference/ado-api/update-method.md)方法。|  
|**adUpdateBatch**|0x10000|支援批次更新（[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)和[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法），以將變更群組傳輸至提供者。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. CursorOption. ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums. CursorOption. 書簽|  
|AdoEnums. CursorOption. DELETE|  
|AdoEnums. CursorOption. FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums. CursorOption. INDEX|  
|AdoEnums. CursorOption. MOVEPREVIOUS|  
|AdoEnums. CursorOption. NOTIFY|  
|AdoEnums. CursorOption. RESYNC|  
|AdoEnums. CursorOption. SEEK|  
|AdoEnums. CursorOption. UPDATE|  
|AdoEnums. CursorOption. UPDATEBATCH|  
  
## <a name="applies-to"></a>套用至  
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
