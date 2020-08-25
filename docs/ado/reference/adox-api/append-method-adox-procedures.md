---
description: Append 方法 (ADOX Procedures)
title: 附加方法 (ADOX 程式) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f416d8223e828d724f1eabbe4ab82061204af0f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771407"
---
# <a name="append-method-adox-procedures"></a>Append 方法 (ADOX Procedures)
將新的[程式](./procedures-collection-adox.md)物件加入至[Procedure](./procedure-object-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要建立和附加的程式名稱。  
  
 *命令*  
 ADO [命令](../ado-api/command-object-ado.md) 物件，代表要建立和附加的程式。  
  
## <a name="remarks"></a>備註  
 使用 **命令** 物件中指定的名稱和屬性，在資料來源中建立新的程式。  
  
 如果使用者指定的命令文字代表某個視圖，而不是程式，則行為取決於所使用的提供者。 如果提供者不支援保存命令，**附加**將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet 的 OLE DB 提供者時，procedure 集合**附加**方法可讓您在*命令***參數中指定****視圖**，而不**是程式。** 此 **視圖** 將會新增至資料來源，並加入至 **程式** 集合。 **附加**之後，如果已重新整理**程式**和**Views**集合，則**視圖**將不再位於**程式**集合中，而且會出現在**Views**集合中。  
  
## <a name="applies-to"></a>套用至  
 [Procedures 集合 (ADOX)](./procedures-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [程式附加方法範例 (VB) ](./procedures-append-method-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [附加方法 (ADOX 資料表) ](./append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)