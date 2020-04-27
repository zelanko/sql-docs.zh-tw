---
title: Fields 集合（ADO） |Microsoft Docs
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
ms.openlocfilehash: 9c9216ee655e371633837c5653ebac56fac1a782
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918710"
---
# <a name="fields-collection-ado"></a>Fields 集合 (ADO)
包含[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的所有[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="remarks"></a>備註  
 **記錄集**物件具有由**欄位**物件組成的**Fields**集合。 每個**Field**物件都會對應至**記錄集**內的資料行。 您可以在集合上呼叫[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，先填入**Fields**集合，然後再開啟**記錄集**。  
  
> [!NOTE]
>  如需如何使用**欄位**物件的詳細說明，請參閱**Field**物件主題。  
  
 **Fields**集合具有[Append](../../../ado/reference/ado-api/append-method-ado.md)方法，它會 provisionally 建立**欄位**物件並將其加入至集合，並使用**Update**方法來完成任何新增或刪除。  
  
 **記錄**物件有兩個特殊欄位，可以使用[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常數來編制索引。 一個常數存取包含**記錄**之預設資料流程的欄位，另一個則存取包含**記錄**之絕對 URL 字串的欄位。  
  
 某些提供者（例如， [Microsoft OLE DB 提供者用於網際網路發行](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)）可能會在**fields**集合中填入**記錄**或**記錄集**可用欄位的子集。 其他欄位將不會新增至集合，直到第一次以名稱參考，或由您的程式碼編制索引為止。  
  
 如果您嘗試依名稱參考不存在的欄位，新的**欄位**物件將會附加至 [**欄位**] 集合，其[狀態](../../../ado/reference/ado-api/status-property-ado-field.md)為 [ **adFieldPendingInsert**]。 當您呼叫[Update](../../../ado/reference/ado-api/update-method.md)時，如果您的提供者允許，ADO 將會在您的資料來源中建立新的欄位。  
  
 本章節包含下列主題。  
  
-   [Fields 集合屬性、方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
