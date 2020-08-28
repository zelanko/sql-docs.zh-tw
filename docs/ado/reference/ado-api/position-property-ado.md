---
description: Position 屬性 (ADO)
title: Position 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: rothja
ms.author: jroth
ms.openlocfilehash: 55ae275db06b8b0c73598977e78954bac0fd22be
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990059"
---
# <a name="position-property-ado"></a>Position 屬性 (ADO)
表示 [資料流程](./stream-object-ado.md) 物件內的目前位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，指定從資料流程開頭開始之目前位置的位移（以位元組數為單位）。 預設值為0，代表資料流程中的第一個位元組。  
  
## <a name="remarks"></a>備註  
 目前的位置可移至資料流程結尾之後的某個點。 如果您指定的目前位置超過資料流程的結尾，**資料流程**物件的[大小](./size-property-ado-stream.md)將會據此增加。 以這種方式新增的任何新位元組都將會是 null。  
  
> [!NOTE]
>  **Position** 一律會測量位元組。 若為使用多位元組字元集的文字資料流程，請將位置乘以字元大小，以判斷字元數。 例如，在雙位元組字元集中，第一個字元位於位置0、位置2的第二個字元、位置4的第三個字元等等。  
  
> [!NOTE]
>  負值不能用來變更 **資料流程**中的目前位置。 只有正數可以用於 **位置**。  
  
> [!NOTE]
>  針對唯讀的**資料流程**物件，如果將 [**位置**] 設定為大於**資料流程****大小**的值，則 ADO 不會傳回錯誤。 這不會變更 **資料流程**的大小，也不會以任何方式改變 **串流** 內容。 不過，您應該避免這種情況，因為它會產生無意義的 **位置**值。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Charset 屬性 (ADO)](./charset-property-ado.md)