---
description: Procedures 集合 (ADOX)
title: 程式集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
author: rothja
ms.author: jroth
ms.openlocfilehash: b3f98420fc85cabd2ccc584817ac6ca9a9203081
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983569"
---
# <a name="procedures-collection-adox"></a>Procedures 集合 (ADOX)
包含目錄 [的所有程式](./procedure-object-adox.md) 物件。  
  
## <a name="remarks"></a>備註  
 **程式**集合的[APPEND](./append-method-adox-procedures.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的程式加入至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 屬性存取集合中的程式。  
  
-   傳回集合中包含 [Count](../ado-api/count-property-ado.md) 屬性的程式數目。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法，從集合中移除程式。  
  
-   使用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前的資料庫架構。  
  
 本節包含下列主題。  
  
-   [Indexes 集合屬性、方法和事件](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令和 CommandText 屬性範例 (VB) ](./command-and-commandtext-properties-example-vb.md)   
 [Parameters 集合、Command 屬性範例 (VB) ](./parameters-collection-command-property-example-vb.md)   
 [程式附加方法範例 (VB) ](./procedures-append-method-example-vb.md)   
 [程式 Delete 方法範例 (VB) ](./procedures-delete-method-example-vb.md)   
 [程式 Refresh 方法範例 (VB) ](./procedures-refresh-method-example-vb.md)   
 [程式集合屬性、方法和事件](./procedures-collection-properties-methods-and-events.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [Procedure 物件 (ADOX)](./procedure-object-adox.md)