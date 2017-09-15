---
title: "判斷支援的項目 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e15f52d48f5870cfe4df8cd6149d56012b42abf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="determining-what-is-supported"></a>判斷支援的項目
**支援**方法用來判斷是否指定**資料錄集**物件支援特定類型的功能。 它有下列語法：  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>備註  
 **支援**方法會傳回布林值，指出提供者是否支援所有 CursorOptions 引數所識別的功能。 您可以使用**支援**方法來判斷哪些類型的功能**資料錄集**物件支援。 如果**資料錄集**物件支援的功能，其對應的常數位於*CursorOptions*、**支援**方法會傳回**True**. 否則，它會傳回**False**。  
  
 使用**支援**方法，您可以檢查的能力**資料錄集**新增新記錄、 使用書籤，請使用物件**尋找**方法，請使用向下捲動，使用**索引**屬性，以及執行批次更新。 常數，其意義的完整清單，請參閱[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)。  
  
 雖然**支援**方法可能會傳回**True**給定的功能，它並不保證，提供者可以讓此功能可以在所有情況下。 **支援**方法只會傳回是否提供者可支援指定的功能，假設某些條件成立。 比方說，**支援**方法可能表示**資料錄集**物件支援更新，即使資料指標為基礎的多個資料表聯結，其中的某些資料行不是可更新。
