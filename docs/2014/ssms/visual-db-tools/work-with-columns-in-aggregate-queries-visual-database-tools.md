---
title: 在彙總查詢中使用資料行 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19aca7390b0e7b56b9fecf568bb17820777dc680
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43807494"
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>在彙總查詢中使用資料行 (Visual Database Tools)
  當您建立彙總查詢時， [查詢和檢視表設計工具](visual-database-tools.md) 會做出特定假設，以便建構有效的查詢。 例如，如果您要建立彙總查詢並標記某資料行進行輸出，查詢和檢視設計師會自動將該資料行變成 GROUP BY 子句的一部分，如此一來您便不會不慎在摘要中顯示個別資料列的內容。  
  
## <a name="using-group-by"></a>使用群組依據  
 查詢和檢視設計師根據下列規則使用資料行：  
  
-   當您選擇 [群組依據] 選項或新增彙總函式至查詢時，所有標記為輸出或做為排序的資料行將自動新增至 GROUP BY 子句。 如果資料行已經是彙總函式的一部分，則不會新增至 GROUP BY 子句。  
  
     如果您不想要特定資料行變成 GROUP BY 子句的一部分，必須在 [準則] 窗格的 [群組依據] 資料行中選取不同的選項來進行手動變更。 但查詢和檢視設計師無法阻止您選擇造成查詢無法執行的選項。  
  
-   如果您手動新增查詢輸出資料行至 [準則] 或 [SQL] 窗格中的彙總函式，查詢和檢視設計師不會自動移除查詢的其他輸出資料行。 因此您必須移除查詢輸出中的其他資料行，或將它們變成 GROUP BY 子句或彙總函式的一部分。  
  
 當您將搜尋條件輸入 [準則] 窗格的 [篩選條件] 資料行時，查詢和檢視設計師將遵守下列規則：  
  
-   如果方格的 [群組依據] 資料行並未顯示 (因為您尚未指定彙總查詢)，則將搜尋條件放入 WHERE 子句。  
  
-   如果您已在彙總查詢中並已選取 [群組依據] 資料行中的 [Where] 選項，則將搜尋條件放入 WHERE 子句。  
  
-   如果 [群組依據] 資料行中含有任何 [Where] 以外的值，則將搜尋條件放入 HAVING 子句。  
  
## <a name="using-the-having-and-where-clauses"></a>使用 HAVING 和 WHERE 子句  
 以下原則說明如何在搜尋條件中參考彙總查詢中的資料行。 通常，您可以使用搜尋條件中的資料行來篩選應進行摘要的資料列 (WHERE 子句)，或決定最後輸出 (HAVING 子句) 中出現的群組結果。  
  
-   WHERE 或 HAVING 子句中可出現個別資料欄，視該資料欄在查詢中其他地方的使用情形而定。  
  
-   WHERE 子句可用來選取要進行摘要和群組化的資料列子集，因此可在完成群組化前套用之。 因此，您可以在 WHERE 子句中使用資料欄，即使該資料欄並非 GROUP BY 子句的一部分或者並不在彙總函式中。 例如，下列陳述式選取價錢超過 $10.00 和平均價格的所有書名：  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   如果您建立的搜尋條件中使用了 GROUP BY 子句或彙總函式所用的資料行，搜尋條件可 WHERE 子句或 HAVING 子句的形式出現；您可以在建立搜尋條件時決定其中一項。 例如，下列陳述式建立針對每個發行者建立書名的平均價格，然後針對發行者顯示平均價格超過 $10.00 的平均價格：  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   如果您在搜尋條件中使用彙總函式，搜尋條件將使用到摘要而且必須是 HAVING 子句的一部分。  
  
## <a name="see-also"></a>另請參閱  
 [摘要查詢結果&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [排序及分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
