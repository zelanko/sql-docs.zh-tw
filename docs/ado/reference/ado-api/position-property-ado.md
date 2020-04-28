---
title: Position 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dba8636f07b88f1c05d465b844376c6ef3e61240
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931651"
---
# <a name="position-property-ado"></a>Position 屬性 (ADO)
表示[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件中目前的位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Long**值，指定從資料流程開頭到目前位置的位移（以位元組數為單位）。 預設值為0，表示資料流程中的第一個位元組。  
  
## <a name="remarks"></a>備註  
 目前的位置可以移至資料流程結尾之後的點。 如果您指定的目前位置超出資料流程的結尾，**資料流程**物件的[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)也會隨之增加。 以這種方式新增的任何新位元組都會是 null。  
  
> [!NOTE]
>  **位置**一律會測量個位元組。 針對使用多位元組字元集的文字資料流程，將位置乘以字元大小，以決定字元數。 例如，如果是兩個位元組的字元集，第一個字元位於位置0，第二個字元位於位置2，第三個字元位於位置4，依此類推。  
  
> [!NOTE]
>  負值不能用來變更**資料流程**中的目前位置。 只有正數可以用於**位置**。  
  
> [!NOTE]
>  對於唯讀**資料流程**物件，如果**Position**設定為大於**資料流程****大小**的值，ADO 將不會傳回錯誤。 這不會變更**資料流程**的大小，也不會以任何方式改變**串流**內容。 不過，應該避免這麼做，因為它會產生無意義的**位置**值。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Charset 屬性 (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
