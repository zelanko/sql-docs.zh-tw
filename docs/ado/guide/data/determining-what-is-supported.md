---
title: 判斷支援的功能 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925526"
---
# <a name="determining-what-is-supported"></a>判斷支援的項目
**支援**方法來判斷是否指定**資料錄集**物件支援特定類型的功能。 它有下列語法：  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>備註  
 **支援**方法會傳回布林值，指出提供者是否支援所有 CursorOptions 引數所識別的功能。 您可以使用**支援**方法，以判斷哪些類型的功能**資料錄集**物件支援。 如果**Recordset**物件支援的功能，其對應的常數位於*CursorOptions*，則**支援**方法會傳回**True**. 否則，它會傳回**False**。  
  
 使用**支援**方法，您可以檢查的能力**資料錄集**物件，以新增新的記錄、 使用書籤，請使用**尋找**方法，請使用向下捲動，使用**索引**屬性，以及執行批次更新。 常數及其意義的完整清單，請參閱 < [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)。  
  
 雖然**支援**方法可能會傳回 **，則為 True**針對指定的功能，它並不保證，提供者可以提供此功能在所有情況下。 **支援**方法只會傳回是否提供者可支援指定的功能，假設某些條件成立。 例如，**支援**方法可能表示**資料錄集**物件支援更新，即使資料指標以多個資料表加入-其中的某些資料行不是可更新為基礎。
