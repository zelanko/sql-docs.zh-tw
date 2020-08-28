---
description: Type 屬性 (ADO Stream)
title: Type 屬性 (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a72fb3afba9ff1455cba3fde8ada4cf82cb6cd3d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988299"
---
# <a name="type-property-ado-stream"></a>Type 屬性 (ADO Stream)
表示 [資料流程](./stream-object-ado.md) 中包含的資料類型 (二進位或文字) 。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 [StreamTypeEnum](./streamtypeenum.md) 值，這個值會指定 **資料流程** 物件中所包含的資料類型。 預設值為 **adTypeText**。 但是，如果二進位資料一開始是寫入新的空白 **資料流程**，該 **型** 別就會變更為 **adTypeBinary**。  
  
## <a name="remarks"></a>備註  
 只有當目前的位置位於**資料流程**的開頭時，才會讀取/寫入**型**別屬性 ([位置](./position-property-ado.md)是 0) ，而且在任何其他位置都是唯讀的。  
  
 **Type**屬性會決定應該使用哪些方法來讀取和寫入**資料流程**。 若為文字 **資料流程**，請使用 [ReadText](./readtext-method.md) 和 [WriteText](./writetext-method.md)。 針對二進位 **資料流程**，請使用 [讀取](./read-method.md) 和 [寫入](./write-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 RecordType 屬性 ](./recordtype-property-ado.md)   
 [Type 屬性 (ADO)](./type-property-ado.md)