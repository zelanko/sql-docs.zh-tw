---
title: 選取不符合某值的資料列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b664c5a99e362ca09096e745cb1fae49799ef81e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266875"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>選取不符合某值的資料列 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要尋找不符合某值的資料列，請使用 NOT 運算子。  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>若要尋找不符合值的資料列  
  
1.  如果尚未這麼做，請將想要在搜尋條件中使用的資料行或運算式新增至[準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中。  
  
2.  尋找包含想要搜尋之資料行或運算式的資料列，然後在 [篩選條件]  方格資料行中輸入 NOT 運算子，後面再加上搜尋值。  
  
例如，若要尋找 `products` 資料表中產品代碼資料行不是以 "A," 為開頭的所有資料列，則可以輸入如下所示的搜尋條件：  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>另請參閱  
[輸入搜尋值的規則 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[指定搜尋條件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
