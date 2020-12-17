---
description: ADOX 物件
title: ADOX 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: 1dfc4a2c44b6ea8c23b9cb56b3a2e6d844e9ca77
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641330"
---
# <a name="adox-objects"></a>ADOX 物件
## <a name="adox-object-summary"></a>ADOX 物件摘要  
  
|Object|描述|  
|------------|-----------------|  
|[目錄](./catalog-object-adox.md)|包含描述資料來源之架構目錄的集合。|  
|[資料行](./column-object-adox.md)|表示來自資料表、索引或索引鍵的資料行。|  
|[群組](./group-object-adox.md)|代表在安全資料庫中具有存取權限的群組帳戶。|  
|[Index](./index-object-adox.md)|表示資料庫資料表中的索引。|  
|[金鑰](./key-object-adox.md)|表示資料庫資料表中的 primary、foreign 或 unique 索引鍵欄位。|  
|[程式](./procedure-object-adox.md)|表示預存程式。|  
|[資料表](./table-object-adox.md)|表示資料庫資料表，包括資料行、索引和索引鍵。|  
|[使用者](./user-object-adox.md)|代表在安全資料庫中具有存取權限的使用者帳戶。|  
|[檢視](./view-object-adox.md)|表示已篩選的一組記錄或虛擬資料表。|  
  
 這些物件之間的關聯性會在 [ADOX 物件模型](./adox-object-model.md)中說明。  
  
 每個物件都可以包含在其對應的集合中。 例如， **資料表** 物件可以包含在 [Tables](./tables-collection-adox.md) 集合中。 如需詳細資訊，請參閱 [ADOX 集合](./adox-collections.md) 或特定集合主題。  
  
## <a name="see-also"></a>另請參閱  
 [ADOX API 參考](./adox-object-model.md)   
 [ADOX 集合](./adox-collections.md)   
 [ADOX 物件模型](./adox-object-model.md)   
 [資料定義語言和安全性的 ADO 延伸模組 (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)