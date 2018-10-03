---
title: 放置屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 333b06ef76ae6407ca8a5605f1917dc0bb609aca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615886"
---
# <a name="position-property-ado"></a>Position 屬性 (ADO)
指出目前的位置內[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，指定的位移，以從一開始的資料流目前位置的位元組數目。 預設值為 0，表示資料流中的第一個位元組。  
  
## <a name="remarks"></a>備註  
 目前的位置可以移至的點，資料流結尾後面。 如果您指定目前的位置，為資料流結尾之外[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**物件會隨之增加。 這種方式新增的任何新位元組將會是 null。  
  
> [!NOTE]
>  **位置**一律量值的位元組。 對於使用多位元組字元集的文字資料流，乘以字元的大小，以判斷的字元數中的位置。 比方說，是雙位元組字集，第一個字元位於位置 0，位於位置 2，第三個字元的第二個字元在位置 4，依此類推。  
  
> [!NOTE]
>  負數的值不能變更中目前的位置**Stream**。 適用於僅正數**位置**。  
  
> [!NOTE]
>  唯讀**Stream**物件，ADO 會傳回錯誤，如果**位置**設為值大於**大小**的**Stream**。 這不會變更的大小**Stream**，或改變**Stream**以任何方式的內容。 不過，執行此動作應避免，因為它會產生無意義**位置**值。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Charset 屬性 (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
