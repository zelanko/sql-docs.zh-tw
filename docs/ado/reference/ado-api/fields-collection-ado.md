---
title: 欄位集合 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8483a908e31b9e4554c5594ecc5bbf186bbef88f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695038"
---
# <a name="fields-collection-ado"></a>Fields 集合 (ADO)
包含所有[欄位](../../../ado/reference/ado-api/field-object.md)的物件[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)或是[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 A **Recordset**物件具有**欄位**組成的集合**欄位**物件。 每個**欄位**物件中的資料行對應**資料錄集**。 您可以填入**欄位**集合，再開啟**資料錄集**藉由呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)集合上的方法。  
  
> [!NOTE]
>  請參閱**欄位**如需如何使用的更詳細說明的物件主題**欄位**物件。  
  
 **欄位**集合中有[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，它部份建立，並將**欄位**物件加入至集合，以及**更新**方法，這個方法會完成任何新增或刪除。  
  
 A**記錄**物件具有可以使用編製索引的兩個特殊欄位[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常數。 一個常數存取欄位，其中包含的預設資料流**記錄**，和其他存取包含的絕對 URL 字串的欄位**記錄**。  
  
 某些提供者 (例如[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 可能會填入**欄位**子集的可用欄位的集合**記錄**或是**資料錄集**。 不會將其他欄位加入至集合，直到第一次參考依名稱或由您的程式碼編製索引。  
  
 如果您嘗試參考不存在的欄位名稱，新**欄位**物件將會附加至**欄位**集合[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)的**adFieldPendingInsert**。 當您呼叫[更新](../../../ado/reference/ado-api/update-method.md)，ADO 會建立新的欄位。 在您的資料來源中如果您的提供者所允許的。  
  
 本章節包含下列主題。  
  
-   [欄位集合屬性、 方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
