---
description: Append 方法 (ADOX Indexes)
title: 附加方法 (ADOX 索引) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b37055efe15f204049d02c337b54c228468419
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985509"
---
# <a name="append-method-adox-indexes"></a>Append 方法 (ADOX Indexes)
將新的 [索引](./index-object-adox.md) 物件加入至 [索引](./indexes-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 要附加的 **索引** 物件，或要建立和附加的索引名稱。  
  
 *資料行*  
 選擇性。 **Variant**值，指定要編制索引之資料行)  (的) 名稱 (s。 *Columns*參數對應到資料[行](./column-object-adox.md)物件的[Name](./name-property-adox.md)屬性 (s) 值。  
  
## <a name="remarks"></a>備註  
 *Columns*參數可以採用資料行的名稱或資料行名稱的陣列。  
  
 如果提供者不支援建立索引，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Indexes 集合 (ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的索引附加方法範例) ](./indexes-append-method-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](./append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](./append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)