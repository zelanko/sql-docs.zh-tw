---
title: "將屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::Position
helpviewer_keywords: Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d26a7c2640b855d34aceadf0369ccb2112d243d9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
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
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [Charset 屬性 (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
