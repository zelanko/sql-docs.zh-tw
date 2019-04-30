---
title: Append 方法 (ADOX Views) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 584c3d0144197425b307f2d4a04bd8a09f27a36c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184214"
---
# <a name="append-method-adox-views"></a>Append 方法 (ADOX Views)
建立新[檢視](../../../ado/reference/adox-api/view-object-adox.md)物件，並將其附加至[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A**字串**值，指定要建立之檢視的名稱。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，表示要建立的檢視。  
  
## <a name="remarks"></a>備註  
 使用名稱和屬性中指定的資料來源中建立新的檢視**命令**物件。  
  
 如果使用者指定的命令文字代表程序，而不是檢視，則行為是取決於提供者。 **附加**如果提供者不支援保存的命令將會失敗。  
  
> [!NOTE]
>  當使用 OLE DB Provider for Microsoft Jet**檢視**集合**附加**方法可讓您指定**程序**而不是**檢視**中*命令*參數。 **程序**將會加入至資料來源，並將加入**檢視**集合。 之後**Append**，如果**程序**並**檢視**集合會重新整理，**程序**中無法再**檢視**集合會出現在**程序**集合。  
  
## <a name="applies-to"></a>適用於  
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views Append 方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)
