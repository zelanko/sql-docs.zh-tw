---
description: Fields 集合 (ADO)
title: " (ADO) 的欄位集合 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1374770ab86038d50c4dd8cafabff328a5275ace
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443730"
---
# <a name="fields-collection-ado"></a>Fields 集合 (ADO)
包含[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的所有[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="remarks"></a>備註  
 **記錄集**物件具有由**欄位**物件組成的**欄位**集合。 每個 **Field** 物件都會對應到 **記錄集中**的資料行。 您可以藉由呼叫集合上的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，在開啟**記錄集**之前填入**Fields**集合。  
  
> [!NOTE]
>  如需如何使用**欄位**物件的詳細說明，請參閱**field**物件主題。  
  
 **Fields**集合具有[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，Provisionally 會建立一個**欄位**物件，並將它加入至集合，以及完成任何新增或刪除的**Update**方法。  
  
 **記錄**物件具有兩個可使用[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常數來編制索引的特殊欄位。 其中一個常數會存取包含 **記錄**之預設資料流程的欄位，而另一個會存取包含 **記錄**之絕對 URL 字串的欄位。  
  
 某些提供者 (例如， [Microsoft OLE DB Provider For Internet 發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 可能會在 **fields** 集合中填入 **記錄** 或 **記錄集**可用欄位的子集。 其他欄位將不會加入至集合，直到第一次依名稱參考，或是由您的程式碼建立索引為止。  
  
 如果您嘗試依名稱參考不存在的欄位，新的 **欄位** 物件將會附加至 [ **欄位** ] 集合，其 [狀態](../../../ado/reference/ado-api/status-property-ado-field.md) 會是 [ **adFieldPendingInsert**]。 當您呼叫 [Update](../../../ado/reference/ado-api/update-method.md)時，如果您的提供者允許，ADO 會在您的資料來源中建立新欄位。  
  
 本節包含下列主題。  
  
-   [Fields 集合屬性、方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
