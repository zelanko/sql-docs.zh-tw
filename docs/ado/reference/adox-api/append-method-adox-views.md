---
title: Append 方法（ADOX Views） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637932fed7effb87705b3aa195578cfd506e1454
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967150"
---
# <a name="append-method-adox-views"></a>Append 方法 (ADOX Views)
建立新的[View](../../../ado/reference/adox-api/view-object-adox.md)物件，並將它附加至[Views](../../../ado/reference/adox-api/views-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要建立的視圖名稱。  
  
 *命令*  
 ADO [Command](../../../ado/reference/ado-api/command-object-ado.md)物件，代表要建立的視圖。  
  
## <a name="remarks"></a>備註  
 使用**命令**物件中指定的名稱和屬性，在資料來源中建立新的 view。  
  
 如果使用者指定的命令文字代表程式，而不是 view，則行為取決於提供者。 如果提供者不支援持續性命令，**附加**將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet 的 OLE DB 提供者時， **Views**集合**Append**方法可讓您在*命令*參數中指定程式 **，而不是** **View** 。 此**程式將會加入**至資料來源，並加入至**Views**集合。 在**附加**之後，如果**程式**和**Views**集合重新整理，則程式不會再出現在**Views**集合中，而且會顯示在 Procedure**集合中**。 ****  
  
## <a name="applies-to"></a>套用至  
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views Append 方法範例（VB）](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)
