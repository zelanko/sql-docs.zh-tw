---
title: 指定搜尋條件 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1cdf4fc43478a8c1a6e4eca052abbec5c788263f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263554"
---
# <a name="specify-search-conditions-visual-database-tools"></a>指定搜尋條件 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以藉由指定搜尋條件來指定出現在查詢中的資料列。 例如，若是正在查詢 `employee` 資料表，可以指定只尋找在特定區域工作的員工。  
  
使用運算式指定搜尋條件。 通常運算式包含運算子和搜尋值。 例如，若要尋找在特定銷售區域的員工，可以在 `region` 資料行指定下列搜尋準則：  
  
```  
='UK'  
```  
  
> [!NOTE]  
> 如果使用多個資料表，[查詢和檢視設計師] 會檢查每個搜尋條件，判斷您所做的比較是否會產生聯結。 若是如此，[查詢和檢視設計師] 會自動將搜尋條件轉換至聯結。 如需詳細資訊，請參閱[自動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)。  
  
### <a name="to-specify-search-conditions"></a>若要指定搜尋條件  
  
1.  如果尚未這麼做，請將想要在搜尋條件中使用的資料行或運算式加入至 [準則] 窗格中。  
  
    如果您正在建立選取查詢，而不想讓搜尋資料行或運算式出現在查詢輸出中，請清除每一個搜尋資料行或運算式的 [輸出]  欄位，將它們當成輸出資料行而加以移除。  
  
2.  尋找包含想要搜尋之資料行或運算式的資料列，然後在 [篩選條件]  欄位中輸入搜尋條件。  
  
    > [!NOTE]  
    > 如果尚未輸入運算子，[查詢和檢視設計師] 會自動插入相等運算子「=」。  
  
查詢和檢視表設計工具藉由加入或修改 WHERE 子句，更新 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 中的 SQL 陳述式。  
  
## <a name="see-also"></a>另請參閱  
[輸入搜尋值的規則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
