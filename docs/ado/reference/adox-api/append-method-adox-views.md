---
description: Append 方法 (ADOX Views)
title: 附加方法 (ADOX Views) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e022afd65b6ea37eda07f6ddb4d35ab135664a8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440450"
---
# <a name="append-method-adox-views"></a>Append 方法 (ADOX Views)
建立新的 [View](../../../ado/reference/adox-api/view-object-adox.md) 物件，並將它附加至 [Views](../../../ado/reference/adox-api/views-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 指定要建立之視圖名稱的 **字串** 值。  
  
 *命令*  
 ADO [命令](../../../ado/reference/ado-api/command-object-ado.md) 物件，代表要建立的視圖。  
  
## <a name="remarks"></a>備註  
 使用 **命令** 物件中指定的名稱和屬性，在資料來源中建立新的視圖。  
  
 如果使用者指定的命令文字代表程式，而不是 view，則行為會視提供者而定。 如果提供者不支援保存命令，**附加**將會失敗。  
  
> [!NOTE]
>  使用 Microsoft Jet 的 OLE DB 提供者時， **Views**集合**附加**方法可讓您在*命令*參數中指定程式 **，而不是** **View** 。 此 **程式將會新增** 至資料來源，並將加入至 **Views** 集合。 **附加**之後，如果**程式**和**Views**集合重新整理，程式就不會再出現在**Views**集合中，而且會出現在**Procedure**集合**中**。  
  
## <a name="applies-to"></a>套用至  
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views 附加方法範例 (VB) ](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)
