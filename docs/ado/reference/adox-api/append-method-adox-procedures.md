---
title: Append 方法 (ADOX Procedures) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 348b2876e4293ad912383859ace47e462da31bcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707961"
---
# <a name="append-method-adox-procedures"></a>Append 方法 (ADOX Procedures)
加入新[程序](../../../ado/reference/adox-api/procedure-object-adox.md)物件[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *[名稱]*  
 A**字串**值，指定要建立並附加的程序的名稱。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，表示要建立並附加的程序。  
  
## <a name="remarks"></a>備註  
 使用名稱和屬性中指定的資料來源中建立新的程序**命令**物件。  
  
 如果使用者指定的命令文字代表一個檢視，而不是程序，則行為是相依於所使用的提供者。 **附加**如果提供者不支援保存的命令將會失敗。  
  
> [!NOTE]
>  當使用 OLE DB Provider for Microsoft Jet**程序**集合**附加**方法可讓您指定**檢視**而不是**程序**中*命令*參數。 **檢視**將會加入至資料來源，並將加入**程序**集合。 之後**Append**，如果**程序**並**檢視**集合會重新整理，**檢視**中無法再**程序**集合會出現在**檢視**集合。  
  
## <a name="applies-to"></a>適用於  
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Procedures Append 方法範例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
