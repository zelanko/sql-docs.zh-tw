---
title: Append 方法（ADOX 程式） |Microsoft Docs
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
ms.openlocfilehash: c703843781558839a3f4f275a8427f69770a8690
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764069"
---
# <a name="append-method-adox-procedures"></a>Append 方法 (ADOX Procedures)
將新的[Procedure](../../../ado/reference/adox-api/procedure-object-adox.md)物件加入至[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要建立和附加的程式名稱。  
  
 *命令*  
 ADO [Command](../../../ado/reference/ado-api/command-object-ado.md)物件，代表要建立和附加的程式。  
  
## <a name="remarks"></a>備註  
 使用**命令**物件中指定的名稱和屬性，在資料來源中建立新的程式。  
  
 如果使用者指定的命令文字代表視圖，而不是程式，則行為取決於所使用的提供者。 如果提供者不支援持續性命令，**附加**將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet 的 OLE DB 提供者時，**程式**集合**附加**方法可讓您在*命令*參數中指定**View** ，而**不是程式**。 此**視圖**會加入至資料來源，並加入至**程式**集合。 在**附加**之後，如果**程式**和**Views**集合重新整理，則此**視圖**將不再位於**程式**集合中，而且會出現在**Views**集合中。  
  
## <a name="applies-to"></a>套用至  
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [程式 Append 方法範例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX Users）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
