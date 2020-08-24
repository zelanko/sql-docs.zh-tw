---
description: Procedure 物件 (ADOX)
title: Procedure 物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8932d2b71f631f24a9ce825804074b9094f932b9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769707"
---
# <a name="procedure-object-adox"></a>Procedure 物件 (ADOX)
表示預存程式。 當與 ADO [命令](../ado-api/command-object-ado.md) 物件一起使用時，可以使用 **Procedure** 物件來加入、刪除或修改預存程式。  
  
## <a name="remarks"></a>備註  
 **Procedure**物件可讓您建立預存程式，而不需要知道或使用提供者的 "create Procedure" 語法。  
  
 使用 **程式物件的** 屬性，您可以：  
  
-   使用 [Name](./name-property-adox.md) 屬性來識別程式。  
  
-   指定可以用來建立或執行程式的 ADO **命令** 物件，方法是使用 [Command](./command-property-adox.md) 屬性。  
  
-   傳回具有 [DateCreated](./datecreated-property-adox.md) 和 [DateModified](./datemodified-property-adox.md) 屬性的日期資訊。  
  
 本節包含下列主題。  
  
-   [Procedure 物件屬性、方法和事件](./procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令和 CommandText 屬性範例 (VB) ](./command-and-commandtext-properties-example-vb.md)   
 [Parameters 集合、Command 屬性範例 (VB) ](./parameters-collection-command-property-example-vb.md)   
 [程式附加方法範例 (VB) ](./procedures-append-method-example-vb.md)   
 [程式 Delete 方法範例 (VB) ](./procedures-delete-method-example-vb.md)   
 [Procedures 集合 (ADOX)](./procedures-collection-adox.md)