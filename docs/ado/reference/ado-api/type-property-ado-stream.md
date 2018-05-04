---
title: 型別屬性 （ADO 資料流） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50d0dc9e59c3ff47f3de9cee33349b85a94ecc8c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="type-property-ado-stream"></a>型別屬性 （ADO 資料流）
表示包含的資料類型[資料流](../../../ado/reference/ado-api/stream-object-ado.md)（二進位或文字）。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)值，指定包含的資料類型**資料流**物件。 預設值是**adTypeText**。 不過，如果一開始，將二進位資料寫入至新，空白**資料流**、**類型**就會變更為**adTypeBinary**。  
  
## <a name="remarks"></a>備註  
 **類型**屬性是讀取/寫入時，才目前位置的開頭**資料流**([位置](../../../ado/reference/ado-api/position-property-ado.md)為 0)，且唯讀的任何其他位置。  
  
 **類型**屬性會決定哪些方法應用於讀取和寫入**資料流**。 文字**資料流**，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)。 二進位**資料流**，使用[讀取](../../../ado/reference/ado-api/read-method.md)和[寫入](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [RecordType 屬性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
