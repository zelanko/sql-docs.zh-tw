---
title: "將屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a3d94b97fa32e372cd6cc67367450d2f62530b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="position-property-ado"></a>Position 屬性 (ADO)
指出目前的位置內[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，指定的位移，以資料流的目前位置開始的位元組數目。 預設值為 0，代表資料流中的第一個位元組。  
  
## <a name="remarks"></a>備註  
 目前的位置可以移至的點，資料流結尾之後。 如果您指定目前的位置超出資料流，結尾[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**資料流**物件會隨之增加。 以此種方式新增任何新位元組將會是 null。  
  
> [!NOTE]
>  **位置**一律會測量位元組。 使用多位元組字元集的文字資料流，乘以字元的大小來決定的字元數中的位置。 例如，雙位元組字元集，第一個字元位於位置 0，位置 2、 第三個字元的第二個字元位於位置 4，依此類推。  
  
> [!NOTE]
>  負數的值不能變更中的目前位置**資料流**。 適用於僅正數**位置**。  
  
> [!NOTE]
>  針對唯讀**資料流**物件，ADO 會傳回錯誤，如果**位置**設定的值大於**大小**的**資料流**。 這不會變更大小**資料流**，或改變**資料流**以任何方式的內容。 不過，執行此動作應避免，因為它會產生無意義**位置**值。  
  
## <a name="applies-to"></a>適用於  
 [資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [字元集屬性 (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)

