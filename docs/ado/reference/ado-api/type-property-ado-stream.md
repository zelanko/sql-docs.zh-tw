---
title: 型別屬性 (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c8cad8d669452fb5d3bdff154cd7c07239f25044
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710886"
---
# <a name="type-property-ado-stream"></a>Type 屬性 (ADO Stream)
指示中所包含的資料類型[Stream](../../../ado/reference/ado-api/stream-object-ado.md) （二進位或文字）。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)值，指定包含的資料類型**Stream**物件。 預設值是**adTypeText**。 不過，如果二進位資料一開始寫入至新時，空**Stream**，則**型別**就會變更為**adTypeBinary**。  
  
## <a name="remarks"></a>備註  
 **型別**屬性是讀取/寫入，只有在目前的位置是在開頭時，才**Stream** ([位置](../../../ado/reference/ado-api/position-property-ado.md)為 0)，且為唯讀狀態的任何其他位置。  
  
 **型別**屬性會決定哪些方法應用於讀取和寫入**Stream**。 文字**資料流**，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)並[WriteText](../../../ado/reference/ado-api/writetext-method.md)。 二進位**資料流**，使用[讀取](../../../ado/reference/ado-api/read-method.md)並[撰寫](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [RecordType 屬性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
