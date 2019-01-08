---
title: 建立插入結果查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebffc2246f0940c4643af2267086e727882a0633
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763110"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>建立插入結果查詢 (Visual Database Tools)
  您可以使用插入結果查詢，將某個資料表的資料列複製到另一個資料表，或者在資料表中複製資料列。 例如，在 `titles` 資料表中，您可以使用插入結果查詢，將關於某個簽發者所有標題的資訊，複製到可供該簽發者使用的第二份資料表。 插入結果查詢與製成資料表查詢 (Make Table Query) 類似，但是可以將資料列複製到現有的資料表中。  
  
> [!TIP]  
>  您也可以使用剪貼的方式將某個資料表的資料列複製到另一個資料表。 針對每個資料表建立一項查詢，並執行查詢。 從其中一個結果方格，將需要的資料列複製到另一個結果方格。  
  
 在建立插入結果查詢時，您指定：  
  
-   將資料列複製到其中的資料庫資料表 (目的資料表)。  
  
-   從中複製資料列的一或多個資料表 (來源資料表)。 這一或多個來源資料表會成為子查詢 (Subquery) 的一部份。 如果您是在資料表中進行複製，來源資料表便與目的資料表相同。  
  
-   要從中複製內容的來源資料表資料行。  
  
-   將資料複製到其中的目標資料表目標資料行。  
  
-   搜尋條件，用來定義要複製的資料列。  
  
-   排序次序 (若要以特定次序複製資料列)。  
  
-   [群組依據] 選項 (如果只要複製摘要資訊)。  
  
 例如，下列查詢會將 `titles` 資料表的標題資訊複製到名稱為 `archivetitles`的封存資料表中。 此查詢會複製特定簽發者所屬全部標題的四個資料行內容：  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  若要將值插入至新資料行，請使用插入值查詢 (Insert Value Query)。  
  
 您可以複製資料列中選取資料行的內容或所有資料行的內容。 不論是哪種情況，您複製的資料都必須與複製的目標資料列資料行相容。 例如，若要複製 `price`之類資料行的內容，複製的目標資料列資料行就必須接受含小數位數的數字資料。 如果您要複製整個資料列，目的資料表與來源資料表的相對應欄位必須相容。  
  
 建立插入結果查詢時，[準則] 窗格將會變更，以反映可以用來複製資料的選項。 窗格中會加入一個 [附加] 欄位，供您指定複製資料的目標資料行。  
  
> [!CAUTION]  
>  插入結果查詢執行的動作無法恢復。 為安全起見，在執行查詢前請先備份資料。  
  
### <a name="to-create-an-insert-results-query"></a>若要建立插入結果查詢  
  
1.  建立新查詢，並加入您要從中複製資料列的資料表 (來源資料表)。 如果您是在資料表中複製資料列，您可以加入來源資料表做為目的資料表。  
  
2.  在 [ **查詢設計工具** ] 功能表中指向 [ **變更類型**]，再按 [ **插入結果**]。  
  
3.  在 [選擇插入結果的目標資料表對話方塊](visual-database-tools.md)中，選取將資料列複製到其中的資料表 (目的資料表)。  
  
    > [!NOTE]  
    >  [查詢和檢視設計師] 無法預先判斷您可以更新哪些資料表和檢視。 因此，[從查詢選擇要插入的資料表] 對話方塊的 [資料表名稱] 清單會顯示正在查詢之資料連接中的所有可用資料表和檢視，甚至包括您無法將資料列複製到其中的資料表和檢視。  
  
4.  在表示資料表或資料表值物件的矩形中，選擇您想複製內容的資料行名稱。 若要複製整個資料列，選擇 **\* （所有資料行）**。  
  
     查詢和檢視表設計工具會將您選擇的資料行新增至 [準則] 窗格的 [資料行] 欄位中。  
  
5.  在 [準則] 窗格的 [附加] 欄位中，在目的資料表中，為您要複製的每個資料行選取目標資料行。 選擇*tablename。\** 如果您要複製整個資料列。 目的資料表的資料行必須與來源資料表的資料行具有相同 (或相容) 的資料類型。  
  
6.  若要以特定次序複製資料列，請指定排序次序。 如需詳細資訊，請參閱[排序及分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)。  
  
7.  在 [篩選條件] 欄位中輸入搜尋條件，以指定要複製的資料列。 如需詳細資訊，請參閱[指定搜尋準則 &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)。  
  
     如果沒有指定搜尋條件，便會將來源資料表的所有資料列複製到目的資料表中。  
  
    > [!NOTE]  
    >  當將要搜尋的資料行加入至 [準則] 窗格時，[查詢和檢視設計師] 也會將它加入至要複製的資料行清單中。 如果想使用某一資料行進行搜尋但不想複製它，請在代表資料表或資料表值物件的矩形中，清除資料行名稱旁的核取方塊。  
  
8.  若要複製摘要資訊，請指定 [群組依據] 選項。 如需詳細資訊，請參閱[摘要查詢結果 &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)。  
  
 在執行插入結果查詢時，[結果窗格](results-pane-visual-database-tools.md)中不會報告結果， 而是出現訊息指出已經複製了多少資料列。  
  
## <a name="see-also"></a>另請參閱  
 [查詢類型的&#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)   
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
