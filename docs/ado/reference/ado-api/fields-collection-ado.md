---
title: 欄位集合 (ADO) |Microsoft 文件
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
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4eebfb3b3e401585829446872545063448ec87d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fields-collection-ado"></a>欄位集合 (ADO)
包含所有[欄位](../../../ado/reference/ado-api/field-object.md)物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 A**資料錄集**物件具有**欄位**集合組成**欄位**物件。 每個**欄位**物件對應中的資料行**資料錄集**。 您可以填入**欄位**集合開頭之前**資料錄集**藉由呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)集合上的方法。  
  
> [!NOTE]
>  請參閱**欄位**物件使用方式的更詳細的說明主題**欄位**物件。  
  
 **欄位**集合具有[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，其部份會建立並新增**欄位**物件加入至集合，以及**更新**方法，完成新增或刪除。  
  
 A**記錄**物件具有兩個特殊欄位，可以使用索引的[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常數。 一個常數存取包含的預設資料流的欄位**記錄**，和其他存取包含的絕對 URL 字串的欄位**記錄**。  
  
 某些提供者 (例如， [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 可能會填入**欄位**子集的可用欄位的集合**記錄**或**資料錄集**。 不會將其他欄位加入至集合，直到第一次由名稱所參考或您的程式碼以編製索引。  
  
 如果您嘗試參考不存在的欄位名稱，新**欄位**物件將會附加至**欄位**集合[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的**adFieldPendingInsert**。 當您呼叫[更新](../../../ado/reference/ado-api/update-method.md)，ADO 會建立新的欄位資料來源中允許您的提供者。  
  
 本章節包含下列主題。  
  
-   [欄位集合的屬性、 方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
