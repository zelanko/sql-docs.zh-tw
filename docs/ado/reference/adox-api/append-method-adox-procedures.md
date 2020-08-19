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
ms.openlocfilehash: 8571790b596f037bb528df375c43c98b6b77c3a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440480"
---
# <a name="append-method-adox-procedures"></a>Append 方法 (ADOX Procedures)
將新的[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)物件加入至[Procedure](../../../ado/reference/adox-api/procedure-object-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要建立和附加的程式名稱。  
  
 *命令*  
 ADO [命令](../../../ado/reference/ado-api/command-object-ado.md) 物件，代表要建立和附加的程式。  
  
## <a name="remarks"></a>備註  
 使用 **命令** 物件中指定的名稱和屬性，在資料來源中建立新的程式。  
  
 如果使用者指定的命令文字代表某個視圖，而不是程式，則行為取決於所使用的提供者。 如果提供者不支援保存命令，**附加**將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet 的 OLE DB 提供者時，procedure 集合**附加**方法可讓您在*命令***參數中指定****視圖**，而不**是程式。** 此 **視圖** 將會新增至資料來源，並加入至 **程式** 集合。 **附加**之後，如果已重新整理**程式**和**Views**集合，則**視圖**將不再位於**程式**集合中，而且會出現在**Views**集合中。  
  
## <a name="applies-to"></a>套用至  
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [程式附加方法範例 (VB) ](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [附加方法 (ADOX 資料表) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
