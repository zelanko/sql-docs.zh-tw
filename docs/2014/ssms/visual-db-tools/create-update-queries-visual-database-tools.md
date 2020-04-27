---
title: 建立更新查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47951e101a5f8f480496c8570a22cd1a950b3309
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63270577"
---
# <a name="create-update-queries-visual-database-tools"></a>建立更新查詢 (Visual Database Tools)
  您可以使用更新查詢，在一次作業中變更多個資料列的內容。 例如，在 `titles` 資料表中，您可以使用更新查詢，將特定發行者所有書籍的價格增加 10%。  
  
 在建立更新查詢時，您指定：  
  
-   要更新的資料表。  
  
-   要更新內容的資料行。  
  
-   用來更新個別資料行的值或運算式。  
  
-   定義要更新資料列的搜尋條件。  
  
 例如，下列查詢會更新 `titles` 資料表，將一個發行者所有書籍的價格增加 10%：  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
>  更新查詢執行的動作無法恢復。 為安全起見，在執行查詢前請先備份資料。  
  
### <a name="to-create-an-update-query"></a>若要建立更新查詢  
  
1.  將要更新的資料表加入至 [圖表] 窗格。  
  
2.  從 [查詢設計工具]  功能表中，指向 [變更類型]  ，然後按一下 [更新]  。  
  
    > [!NOTE]  
    >  在啟動更新查詢時，如果 [圖表] 窗格中顯示一個以上的資料表，查詢和檢視表設計工具會顯示[選擇插入值的目標資料表對話方塊](visual-database-tools.md)，以詢問要更新的資料表名稱。  
  
3.  在 [圖表] 窗格中，按一下要提供新值之各資料行的核取方塊。 這些資料行將顯示在 [準則] 窗格中。 只有加入查詢中的資料行才會更新。  
  
4.  在 [準則] 窗格的 [新值]  資料行中，輸入資料行的更新值。 您可輸入常值、資料行名稱或運算式。 該值必須符合 (或相容於) 正在更新之資料行的資料類型。  
  
    > [!CAUTION]  
    >  [查詢和檢視設計師] 不會檢查值是否符合所更新資料行的長度。 如果提供的值太長，它可能會無預警地被截斷。 例如，如果 `name` 資料行的長度是 20 個字元，但是您指定 25 個字元的更新值，則最後 5 個字元可能會被截斷。  
  
5.  在 [篩選條件]  資料行中輸入搜尋條件，以定義要更新的資料列。 如需詳細資訊，請參閱[指定搜尋準則 &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)。  
  
     如果不指定搜尋條件，則指定資料表中的所有資料列會更新。  
  
    > [!NOTE]  
    >  在資料行加入至 [準則] 窗格以做為搜尋條件時，[查詢和檢視設計師] 也會將其加入至要更新的資料行清單中。 如果想使用資料行做為搜尋條件但不想更新它，請在代表資料表或資料表值物件的矩形中，清除資料行名稱旁的核取方塊。  
  
 當執行更新查詢時， [結果窗格](results-pane-visual-database-tools.md)不會報告結果。 而是出現訊息指出已經變更了多少資料列。  
  
## <a name="see-also"></a>另請參閱  
 [支援的查詢類型 &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [設計查詢和觀看 how to 主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
