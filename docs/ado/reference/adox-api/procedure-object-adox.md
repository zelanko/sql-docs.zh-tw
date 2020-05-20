---
title: Procedure 物件（ADOX） |Microsoft Docs
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
ms.openlocfilehash: 4a56088e47a9f794f1862ef87bf142a8d3ab12c4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763689"
---
# <a name="procedure-object-adox"></a>Procedure 物件 (ADOX)
表示預存程式。 搭配 ADO [Command](../../../ado/reference/ado-api/command-object-ado.md)物件使用時，**程式物件可以**用來加入、刪除或修改預存程式。  
  
## <a name="remarks"></a>備註  
 **Procedure**物件可讓您建立預存程式，而不需要知道或使用該提供者的「create Procedure」語法。  
  
 利用**Procedure**物件的屬性，您可以：  
  
-   使用[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性來識別程式。  
  
-   指定可以用來建立或執行具有[命令](../../../ado/reference/adox-api/command-property-adox.md)屬性之程式的 ADO**命令**物件。  
  
-   傳回具有[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性的日期資訊。  
  
 本章節包含下列主題。  
  
-   [Procedure 物件屬性、方法和事件](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 和 CommandText 屬性範例（VB）](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Parameters 集合、Command 屬性範例（VB）](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [程式 Append 方法範例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [程式 Delete 方法範例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
