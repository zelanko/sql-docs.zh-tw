---
title: Expression Scope for Totals，Aggregates，and Built-in Collections （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a8d24287-8557-4b03-bea7-ca087f449b62
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3e5c894c75002f95ed67c8383c5497db998dfa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240712"
---
# <a name="expression-scope-for-totals-aggregates-and-built-in-collections-report-builder-and-ssrs"></a>總計、彙總與內建集合的運算式範圍 (報表產生器及 SSRS)
  撰寫運算式時，您會發現 *「範圍」* (Scope) 一詞用於多個內容。 範圍可以指定要用於評估運算式的資料、轉譯頁面上的文字方塊集合、可以根據切換顯示或隱藏之報表項目的集合。 您將會在與運算式評估、彙總函式語法、條件式可用性相關的主題中，以及與這些領域相關的錯誤訊息中看 *「範圍」* (Scope) 一詞。 使用下列描述來協助區分 *「範圍」* (Scope) 適用的意義：  
  
-   **資料範圍** ：資料範圍是報表處理器所使用的範圍階層，因為它會結合報表資料和報表配置，並建立用來顯示資料的資料區，例如資料表及圖表。 了解資料範圍可協助您在執行下列動作時得到您希望的結果：  
  
    -   **撰寫使用彙總函式的運算式** ：指定要彙總的資料。 運算式在報表中的位置會影響彙總計算範圍的資料。  
  
    -   **將走勢圖加入至資料表或矩陣** ：指定要對齊資料表或矩陣中之巢狀執行個體的圖表座標軸最小和最大範圍。  
  
    -   **將指標加入至資料表或矩陣** ：指定要對齊資料表或矩陣中之巢狀執行個體的量測計最小和最大刻度。  
  
    -   **撰寫排序運算式** ：指定一個您可以用來同步處理多個相關報表項目之間的排序次序之包含範圍。  
  
-   **資料格範圍** ：資料格範圍是資料格所屬之 Tablix 資料區中資料列及資料行群組的集合。 依預設，每個 Tablix 資料格都包含一個文字方塊。 文字方塊的值為運算式。 資料格的位置會間接決定您可以在運算式中針對彙總函式指定的資料範圍。  
  
-   **報表項目範圍** ：報表項目範圍指的是轉譯之報表頁面上的項目集合。 報表處理器會結合資料與報表配置元素來產生已編譯的報表定義。 在此程序期間，資料區 (例如資料表和矩陣) 會依需要擴展以顯示所有報表資料。 接著，報表轉譯器會處理已編譯的報表。 報表轉譯器會決定每一頁所出現的報表項目。 在報表伺服器上，當您檢視每個頁面時，系統就會轉譯頁面。 匯出報表時，所有頁面都會經過轉譯。 了解報表項目範圍可協助您在執行下列動作時得到您希望的結果：  
  
    -   **加入切換項目** ：指定文字方塊來加入控制報表項目可見性的切換。 您只能將切換加入至您要切換之報表項目範圍中的文字方塊。  
  
    -   **在頁首與頁尾中撰寫運算式** ：在文字方塊或出現在轉譯頁面之其他報表項目中，指定運算式的值。  
  
 了解範圍可協助您成功撰寫能夠提供您希望之結果的運算式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DataScope"></a> 了解資料範圍和資料階層  
 資料範圍會指定一組報表資料。 資料範圍擁有自然階層以及繼承的內含項目關聯性。 階層上的範圍越高，包含的範圍在階層上越低。 下列資料範圍清單依序描述階層 (資料從最多到最少)：  
  
-   **套用資料集篩選後的資料集** ：指定連結到報表主體中之資料區或報表項目的報表資料集。 用於彙總的資料是在套用資料集篩選運算式之後取自報表資料集。 若是共用資料集，這表示共用資料集定義中的篩選與報表之共用資料集執行個體中的篩選。  
  
-   **資料區域** ：指定在套用資料區域篩選和排序運算式之後取自資料區域的資料。 在計算資料區的彙總時，不會使用群組篩選。  
  
-   **套用群組篩選後的資料區群組** ：指定在套用群組運算式和群組篩選之後父群組和子群組的資料。 若是資料表，這式資料列和資料行群組。 若是圖表，這是數列和類別目錄群組。 為了識別範圍內含項目，每個父群組都會包含其子群組。  
  
-   **巢狀資料區域** —針對要加入資料的資料格內容，指定在套用巢狀資料區域篩選和排序運算式之後的巢狀資料區域的資料。  
  
-   **巢狀資料區域的資料列和資料行群組** ：指定在套用巢狀資料區域的群組運算式和群組篩選之後的資料。  
  
 撰寫包含彙總函式的運算式時，了解包含和被包含的範圍相當重要。  
  
##  <a name="Aggregates"></a> 資料格範圍和運算式  
 當您指定範圍時，表示您向報表處理器指示要用於彙總計算的資料。 根據運算式和運算式的位置，有效範圍可能是 *「包含的範圍」*(Containing Scope) (亦稱為父範圍) 或 *「被包含的範圍」*(Contained Scope) (亦稱為子範圍或巢狀範圍)。 一般而言，您無法在彙總計算中指定個別的群組執行個體。 您可以跨所有群組執行個體指定彙總。  
  
 報表處理器會結合來自報表資料集中的資料以及 Tablix 資料區，因此，它會評估群組運算式，並建立表示群組執行個體所需的資料列和資料行。 在每個 Tablix 資料格中，文字方塊內的運算式值會在資料格範圍的內容中評估。 根據 Tablix 結構，資料格可以屬於多個資料列群組和資料行群組。 若是彙總函式，您可以使用下列其中一個範圍指定要使用的範圍：  
  
-   **預設範圍** ：報表處理器評估運算式時，位於計算範圍中的資料。 預設範圍資料格或資料點所屬的最內部一組群組。 若是 Tablix 資料區，此集合可以包含資料列和資料行群組。 若是圖表資料區，此集合可以包含類別目錄和數列群組。  
  
-   **具名範圍** ：位於運算式範圍中之資料集、資料區或資料區群組的名稱。 若是彙總計算，您可以指定一個包含的範圍。 您無法在單一運算式中同時指定資料列群組和資料行群組的具名範圍。 除非運算式是供彙總使用，否則您無法指定被包含的範圍。  
  
     下列運算式會產生 SellStartDate 與 LastReceiptDate 之間的間隔年數。 這些欄位位於兩個不同的資料集：DataSet1 和 DataSet2 中。 [First 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-first-function.md) 為彙總函式，它會傳回 DataSet1 中 SellStartDate 的第一個值，以及 DataSet2 中 LastReceiptDate 的第一個值。  
  
    ```  
    =DATEDIFF("yyyy", First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   **網域範圍** ：也稱為同步處理範圍。 一種資料範圍的類型，適用於巢狀資料區的運算式評估。 網域範圍用來跨所有群組執行個體指定彙總，讓系統可以對齊巢狀執行個體並輕鬆進行比較。 例如，您可以對齊資料表中內嵌之走勢圖的範圍和高度，讓這些值可以對齊。  
  
 在某些報表位置，您必須指定一個範圍。 例如，若是設計介面上的文字方塊，您必須指定要使用的資料集名稱： `=Max(Fields!Sales.Value,"Dataset1")`。 在某些位置，則有一個隱含的預設範圍。 例如，如果您沒有在群組範圍中指定文字方塊的彙總，則會先使用預設彙總。  
  
 每個彙總函式主題都會列出適用於其用途的範圍。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。  
  
##  <a name="Examples"></a> 資料表資料區的彙總運算式範例  
 撰寫指定非預設範圍的運算式需要一些練習。 為協助您了解不同範圍，請使用下列圖表與資料表。 此圖表會在銷售資訊資料表中標示每個資料格，依年度和季度以及銷售領域顯示銷售的項目數量。 請注意顯示資料列與資料行群組結構之資料列控制代碼和資料行控制代碼上，表示巢狀群組的視覺提示。 資料表的結構如下：  
  
-   包含邊角資料格與三個資料列 (包括資料行群組標頭) 的資料表標頭。  
  
-   以名稱為 Cat 之類別目錄和名稱為 SubCat 之子類別目錄為基礎的兩個巢狀資料列群組。  
  
-   以名稱為 Year 之年度與名稱為 Qtr 之季度為基礎的兩個巢狀資料行群組。  
  
-   標示為 Totals 的一個靜態總計資料行。  
  
-   以名稱為 Territory 之銷售領域為基礎的一個相鄰資料行群組。  
  
 領域群組的資料行標頭已針對顯示用途，分成兩個資料格。 第一個資料格會顯示領域名稱與總計，而第二個資料格中的預留位置文字會針對每個領域計算所有銷售量所佔的百分比。  
  
 ![rs_BasicTableSumCellScope](../media/rs-basictablesumcellscope.gif "rs_BasicTableSumCellScope")  
  
 假設資料集的名稱為 DataSet1，而資料表的名稱為 Tablix1。 下表列出資料格標籤、預設範圍和範例。 預留位置文字的值會以運算式語法顯示。  
  
|資料格|預設範圍|預留位置標籤|文字或預留位置的值|  
|----------|-------------------|------------------------|--------------------------------|  
|C01|Tablix1|[Sum(Qty)]|彙總和範圍<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C02|外部資料行群組 "Year"|[Year]<br /><br /> ([YearQty])|`=Fields!Year.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C03|Tablix1|[Sum(Qty)]|總計<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C04|對等資料行群組 "Territory"|([Total])|Territory<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C05|內部群組 "Qtr"|[Qtr]<br /><br /> ([QtrQty])|Q<br /><br /> `=Fields!Qtr.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C06|對等資料行群組 "Territory"|[Territory]<br /><br /> ([Tty])<br /><br /> [Pct]|`=Fields!Territory.Value`<br /><br /> `=Sum(Fields!Qty.Value)`<br /><br /> `=FormatPercent(Sum(Fields!Qty.Value,"Territory")/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C07|外部資料列群組 "Cat"|[Cat]<br /><br /> [Sum(Qty)]|`=Fields!Cat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C08|與 C07 相同|||  
|C09|外部資料列群組 "Cat" 和內部資料行群組 "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C10|與 C07 相同|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C11|外部資料列群組 "Cat" 和資料行群組 "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Territory"),0) & " of " & Sum(Fields!Qty.Value,"Territory")`|  
|C12|內部資料列群組 "Subcat"|[Subcat]<br /><br /> [Sum(Qty)]|`=Fields!SubCat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C13|內部資料列群組 "Subcat" 和內部資料行群組 "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C14|內部資料列群組 "Subcat"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Cat"),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
|C15|內部資料列群組 "Subcat" 和資料行群組 "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Code.CalcPercentage(Sum(Fields!Qty.Value),Sum(Fields!Qty.Value,"Cat")),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
  
 如需解譯 Tablix 資料區之視覺提示的詳細資訊，請參閱 [Tablix 資料區域資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。 如需 Tablix 資料區的詳細資訊，請參閱 [Tablix 資料區域資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。 如需運算式和彙總的詳細資訊，請參閱[報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) 和[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。  
  
  
  
##  <a name="Sparklines"></a> 同步處理走勢圖的縮放比例  
 若要針對內嵌在資料表或矩陣中的走勢圖，跨時間比較水平軸上的值，您可以同步處理類別目錄群組值。 這稱為對齊座標軸。 透過選取要對齊座標軸的選項，報表會自動設定座標軸的最小值和最大值，並提供預留位置給不存在於每個類別目錄中的彙總值。 這會使走勢圖中的值跨每個類別目錄對齊，並讓您比較彙總資料之每個資料列的值。 透過選取這個選項，表示您要從運算式評估的範圍變更為 *「網域範圍」*(Domain Scope)。 設定巢狀圖表的網域範圍也會間接地控制每個類別目錄在圖例中的色彩指派。  
  
 例如，在顯示每週趨勢的走勢圖中，假設某個城市有 3 個月的銷售資料，而另一個城市有 12 個月的銷售資料。 如果沒有同步處理的縮放比例，第一個城市的走勢圖只會有 3 個橫條，而且這 3 個橫條會比較寬，所佔用的空間會與第二個城市 12 個月的橫條相同。  
  
 如需詳細資訊，請參閱[在資料表或矩陣的圖表上對齊資料 &#40;報表產生器及 SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)。  
  
  
  
##  <a name="Indicators"></a> 同步處理指標的範圍  
 若要指定用於一組指標的資料值，您必須指定一個範圍。 根據包含指標之資料區的配置，您可以指定一個範圍或一個包含的範圍。 例如，在與 sales 類別目錄相關聯的群組標頭資料列中，一組箭頭 (向上、向下、側邊) 可以表示相對於臨界值的銷售值。 包含的範圍是包含指標之資料表或矩陣的名稱。  
  
 如需詳細資訊，請參閱 [設定同步處理範圍 &#40;報表產生器及 SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md)。  
  
  
  
##  <a name="Page"></a> 從頁首或頁尾指定範圍  
 若要在每個報表頁面上顯示不同的資料，您要將運算式加入至必須位於轉譯頁面上的報表項目中。 報表在轉譯時會分成好幾頁，因此，只有在轉譯期間可以決定要存在於頁面上的項目。 例如，詳細資料列中的資料格所擁有的文字方塊在一個頁面上有多個執行個體。  
  
 基於此目的，有一個稱為 ReportItems 的全域集合。 這是在目前頁面上的文字方塊集合。  
  
 如需詳細資訊，請參閱[頁首和頁尾 &#40;報表產生器及 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md) 和 [ReportItems 集合參考 &#40;報表產生器及 SSRS&#41;](built-in-collections-reportitems-collection-references-report-builder.md)。  
  
  
  
##  <a name="Toggles"></a> 指定向下鑽研和條件式可見性的切換項目  
 切換是加入到文字方塊中的加號或減號影像，使用者按一下就可以顯示或隱藏其他報表項目。 在多數報表項目屬性的 **[可見性]** 頁面上，您可以指定要加入切換的目標報表項目。 切換項目所在的內含項目範圍必須比要顯示或隱藏的項目高。  
  
 在 Tablix 資料區中，若要建立向下鑽研效果，讓您按一下某個文字方塊就可以展開資料表來顯示更多資料，您必須在群組上設定 **[可見性]** 屬性，然後在與包含的群組相關聯之群組標頭中選取一個文字方塊做為切換。  
  
 如需詳細資訊，請參閱 [將展開或摺疊動作加入項目中 &#40;報表產生器及 SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)。  
  
  
  
##  <a name="Sort"></a> 指定要同步處理排序次序的排序運算式  
 當您將互動式排序按鈕加入至資料表資料行時，您可以針對擁有通用包含範圍的多個項目，同步處理排序。 例如，您可以將排序按鈕加入至矩陣中的資料行標頭，然後指定包含的範圍做為繫結至矩陣之資料集的名稱。 當使用者按一下排序按鈕時，除了會排序矩陣資料列之外，也會排序繫結至相同資料集之圖表的圖表數列群組。 利用這個方式，與該資料集相依的所有資料區都可以進行同步處理，以顯示相同的排序次序。  
  
 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
  
  
##  <a name="Nulls"></a> 在資料格中隱藏 Null 或零值  
 對於許多報表而言，群組範圍的計算可能會建立許多值為零 (0) 或 Null 的資料格。 為減少報表中混亂的情形，加入一個運算式，以便在彙總值為 0 時，傳回空白。 如需詳細資訊，請參閱 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。  
  
  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](group-expression-examples-report-builder-and-ssrs.md)   
 [建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
