---
title: "使用結果窗格中的資料 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7493784bc506c454ab0c230d549d0accae58c7c4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>使用結果窗格中的資料 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 在您執行查詢或檢視後，結果會顯示在 [結果] 窗格中。 接著您就可以使用這些結果。 例如，您可以加入與刪除資料列，輸入或變更資料，並且輕易地巡覽大筆的結果集。  
  
下列資訊可以協助您避免問題，並且有效率地使用結果集。  
  
## <a name="returning-the-results-set"></a>傳回結果集  
您可從查詢或檢視傳回結果，並選擇是否僅開啟結果窗格或開啟所有窗格。 不論使用哪一種方式，都會在 [查詢和檢視設計師] 中開啟查詢或檢視。 兩者的差異在於一個僅顯示 [結果] 窗格，另一個則開啟在 [選項] 對話方塊中所選取的所有視窗。 預設值是所有四個窗格 (結果、SQL、圖表與準則)。  
  
如需詳細資訊，請參閱[開啟查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)。  
  
若要變更查詢或檢視的設計，使其傳回不同的結果集，或依不同的順序傳回資料錄，請參閱[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md) 中所列的主題。  
  
您亦可以下列兩種方式來決定是否傳回全部或部份的結果集；當其執行時停止查詢，或在執行查詢前選擇要傳回的結果數量。  
  
## <a name="navigating-in-the-results-pane"></a>在結果窗格中巡覽  
您可使用在 [結果] 窗格下方的巡覽列快速巡覽資料錄。  
  
有按鈕可移至第一筆與最後一筆資料錄、下一筆與前一筆資料錄，以及移至特定資料錄。  
  
若要移至特定資料錄，在巡覽列文字方塊中輸入列號，然後按 ENTER。  
  
如需在查詢和檢視表設計工具中使用鍵盤快速鍵的詳細資訊，請參閱[在查詢和檢視表設計工具中巡覽 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md)。  
  
## <a name="committing-changes-to-the-database"></a>資料庫認可變更  
[結果] 窗格使用開放式並行存取控制，所以方格顯示的是資料庫資料的複本，而不是完整的即時檢視。 依此方式所產生之資料的變更，僅會在您完成資料列的檢視後，認可至資料庫。 此方式允許一個以上使用者同時使用資料庫。 若有衝突發生 (例如，其他使用者先變更了您要變更的同一資料列，並將該變更寫入至資料庫)，您會收到發生衝突的訊息，並提供解決方式。  
  
## <a name="undo-changes-using-esc"></a>使用 ESC 恢復變更  
您僅能恢復資料庫尚未認可的變更。 若您尚未完成確認資料錄，或完成確認後但仍收到資料庫將不會認可變更的錯誤訊息，資料庫都將不會認可該資料。 若資料庫尚未認可該變更，可使用 ESC 鍵將其恢復。  
  
若要恢復資料列中所有的變更，請移至尚未編輯的資料列中的資料格，然後按下 ESC 鍵。  
  
若要恢復已編輯之特定資料格的變更，請移至該資料格，並按下 ESC 鍵。  
  
## <a name="adding-or-deleting-data-in-the-database"></a>在資料庫中加入或刪除資料  
若要了解資料庫設計的運作方式，您可能必須將資料範例加入資料庫中。 您可將它直接輸入至結果窗格，或從另一個程式 (例如，記事本或 Excel) 複製並貼至結果窗格。  
  
除了複製資料列至 [結果] 窗格，您還可以加入新的資料錄，或是修改或刪除現有的資料錄。 如需詳細資訊，請參閱[在結果窗格中新增資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-new-rows-in-the-results-pane-visual-database-tools.md)、[在結果窗格中刪除資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/delete-rows-in-the-results-pane-visual-database-tools.md) 和[在結果窗格中編輯資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/edit-rows-in-the-results-pane-visual-database-tools.md)。  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>NULL 值與空資料格的使用提示  
當您按一下空資料列以加入新資料錄時，所有資料行的初始值將為 *NULL*。 若資料行允許 null 值，您可讓它保持原狀。  
  
若想要以 null 值取代非 null 值，則輸入大寫的 NULL。 [結果] 窗格將會以斜體格式顯示該字，表示其被識別為 null 值而非字串。  
  
若要輸入字串 "null"，請輸入不帶有引號之字母。 若其中至少有一個字母為小寫，則其值將會被視為字串，而不是 null 值。  
  
二進位資料類型的資料行預設值為 NULL。 這些值無法在 [結果] 窗格中進行變更。  
  
若要輸入空格取代 null，請刪除現有的文字，並移開資料格。  
  
## <a name="validating-data"></a>驗證資料  
[查詢和檢視設計師] 可以根據資料行屬性來驗證某些資料。 例如，若在具有 float 資料類型的資料行中輸入 "abc"，您將會收到錯誤訊息，且資料庫將不會認可這個變更。  
  
在 [結果] 窗格中檢視資料行資料類型最快速的方法就是，開啟 [圖表] 窗格，將滑鼠指標停留在資料表或資料表值物件中的資料行名稱上。  
  
> [!NOTE]  
> [結果] 窗格所能顯示之文字資料類型的最大長度為 2,147,483,647。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>保持結果集與查詢定義同步  
當您在處理查詢或檢視結果時，[結果] 窗格中的資料錄可能未與查詢定義保持同步。 例如，若您在資料表中執行五個資料行其中四個的查詢，然後使用 [圖表] 窗格在查詢定義中加入第五個資料行，則第五個資料行的資料將不會自動加入至結果窗格中。 若要讓 [結果] 窗格反映新的查詢定義，請再次執行查詢。  
  
您能夠判斷是否有這樣的情況發生 -- 在 [結果] 窗格的右下角會有警告圖示以及出現「已變更的查詢」文字，且圖示會在窗格的左上角重複出現。  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>協調多位使用者進行的變更  
當您在處理查詢或檢視的結果時，正在使用資料庫的其他使用者可能會變更資料錄。  
  
若發生這種情形，您會在移開資料格時收到衝突通知。 然後您便可以覆寫其他使用者的變更、更新其他使用者的變更至 [結果] 窗格或是忽略該變更並繼續您的編輯。 如果選擇忽略該變更，則資料庫將不會認可您所做的變更。  
  
## <a name="limitations-in-the-results-pane"></a>結果窗格中的限制  
  
### <a name="what-can-not-be-updated"></a>何者無法更新  
這些提示有助於順利使用 [結果] 窗格中的資料。  
  
-   包含來自一個以上資料表或檢視的資料行之查詢，無法更新。  
  
-   檢視僅能在資料庫條件約束允許時進行更新。  
  
-   由預存程序所傳回的結果無法更新。  
  
-   使用 GROUP BY、DISTINCT 或 TO XML 子句的查詢或檢視無法更新。  
  
-   資料表值函數所傳回的結果，只能在某些情況下更新。  
  
-   來自查詢運算式結果之資料行中的資料。  
  
-   提供者未順利轉譯的資料。  
  
### <a name="what-can-not-be-represented-fully"></a>何者無法完整表示  
從資料庫傳回 [結果] 窗格的資料，大部份是由您所使用之資料來源的提供者控制。 [結果] 窗格未必能轉譯來自所有資料庫管理系統之資料。 此處的範例即有這種情形。  
  
-   通常二進位資料類型對於在 [結果] 窗格中工作的人不太有用，而且下載要花費很長的時間。 因此，它們由 *<Binary data>* 或 *Null*代表。  
  
-   有效位數與小數位數未必會被保留。 例如，[結果] 窗格支援 27 位數的有效位數。 若資料具有較高有效位數的資料類型，則資料可能會被截斷或由 *<Unable to read data>*代表。  
  
## <a name="see-also"></a>另請參閱  
[執行查詢的基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
