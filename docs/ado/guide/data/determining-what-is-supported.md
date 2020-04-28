---
title: 判斷支援的內容 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc42e9128ccc1ccb43996f554ffe280916884307
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925526"
---
# <a name="determining-what-is-supported"></a>判斷支援的項目
**支援**方法是用來判斷指定的**記錄集**物件是否支援特定類型的功能。 其語法如下：  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>備註  
 **支援**方法會傳回布林值，指出提供者是否支援 CursorOptions 引數所識別的所有功能。 您可以使用**支援**方法，來判斷**記錄集**物件所支援的功能類型。 如果**記錄集**物件支援其對應常數在*CursorOptions*中的功能，**支援**方法會傳回**True**。 否則，它會傳回**False**。  
  
 使用**支援**方法，您可以檢查**記錄集**物件是否能夠加入新的記錄、使用書簽、使用**Find**方法、使用滾動、使用**索引**屬性，以及執行批次更新。 如需常數及其意義的完整清單，請參閱[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)。  
  
 雖然針對指定的功能，**支援**方法可能會傳回**True** ，但並不保證提供者可以在所有情況下提供此功能。 **支援**方法只會傳回提供者是否可支援指定的功能（假設符合特定條件）。 例如，**支援**方法可能表示**記錄集**物件支援更新，即使資料指標是以多重資料表聯結為基礎，但有些資料行無法更新。
