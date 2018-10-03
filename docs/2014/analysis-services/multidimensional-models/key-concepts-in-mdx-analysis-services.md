---
title: 重要的概念在 MDX (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b13e80ce8ad0c721ea7cbde0188d73fec15b2e89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049539"
---
# <a name="key-concepts-in-mdx-analysis-services"></a>MDX 的關鍵概念 (Analysis Services)
  在您使用多維度運算式 (MDX) 查詢 Cube 中的多維度資料，或在 Cube 中建立 MDX 運算式之前，先了解多維度的概念與詞彙會相當有助益。  
  
 最好先從您已經知道的資料摘要開始著手，然後觀察 MDX 如何與此資料摘要相關聯。 以下是在 Excel 中建立的樞紐分析表，其中已填入了 Analysis Services 範例 Cube 的資料。  
  
 ![量值和維度所呼叫的樞紐分析表](../media/ssas-keyconcepts-pivot1-measures-dimensions.png "具有量值和維度叫出樞紐分析表")  
  
## <a name="measures-and-dimensions"></a>量值與維度  
 Analysis Services Cube 包含量值、維度以及維度屬性，這些在樞紐分析表範例中都很容易看見。  
  
 **量值** 是可在資料格中找到的數值資料值，其可會彙總成總和、計數、百分比、最小值、最大值或平均值。 量值為動態項目，且會即時進行計算，以回應使用者導覽以及與樞紐分析表的互動。 在此範例中，資料格會依據軸的展開或折疊，顯示增加或減少的「轉售商銷售數量」。 您可以透過「日期」(年、季、月或日期) 及「銷售領域」(國家/地區群組、國家/地區、地區) 的任意組合，取得特定內容的加總「轉售商銷售數量」。 與「量值」同義的其他詞彙包括「事實」(用於資料倉儲) 及「計算所得欄位」(用於表格式模型及 Excel 資料模型)。  
  
 **維度** 是樞紐分析表中的資料行軸與資料列軸，可提供量值背後的意義。 維度與關聯式資料模型中的資料表類似。 維度的常見範例包含時間、地理位置、產品、客戶、員工等等。 此範例有兩個維度，資料列上的「銷售領域」，以及橫跨頂端的「日期」，但您可以輕鬆地拖放與「轉售商銷售」相關聯的其他維度，例如「促銷」或「產品」，以檢視這些維度的銷售績效。 您是否可以使用特定的方式探索資料，取決於您所建立的維度，以及這些維度是否與您資料來源中的事實資料表相關聯。  
  
 **維度屬性** 是維度中的具名項目，與資料表中的資料行類似。 在此範例中，「銷售領域」維度屬性包含「國家/地區群組」(歐洲、北美、亞太)、「國家 (地區)」(加拿大、美國) 以及「地區」(中部、東北部、西北部、東南部、西南部)。  
  
 每個屬性都有一個與之相關聯的資料值或成員集合。 在此範例中，「國家/地區群組」屬性為歐洲、北美和亞太。 **成員** 是屬於屬性的實際資料值。  
  
> [!NOTE]  
>  資料模型化的其中一部份，就是將資料中本身已存在的模式和關聯性定形。 使用屬於自然階層的資料時，例如國家/地區-地區-城市，您可以透過建立 **屬性關聯性**，將關聯性定形。 屬性關聯性是屬性與屬性間一對多的關聯性，例如省/市與城市之間的關聯性，其中省/市可以有多個城市，但城市只歸屬於一個省/市。 在模型中建立屬性關聯性，可以加快查詢效能；因此，在該資料支援的情況下，最佳作法就是建立屬性關聯性。 您可以在 SQL Server Data Tools 的維度設計師中建立屬性關聯性。 請參閱＜ [Define Attribute Relationships](attribute-relationships-define.md)＞。  
  
 在 Excel 中，會在樞紐分析表欄位清單中顯示模型中繼資料。  將上方的樞紐分析表與下方的欄位清單進行比較。 請注意，欄位清單包含「銷售領域」、「群組」、「國家/地區」、「地區」(中繼資料)，但樞紐分析表只包含成員 (資料值)。 了解圖示外觀有助於您輕鬆地將多維度模型的各個部分，與 Excel 中的樞紐分析表相關聯。  
  
 ![樞紐分析表欄位清單](../media/ssas-keyconcepts-ptfieldlist.png "樞紐分析表欄位清單")  
  
## <a name="attribute-hierarchies"></a>屬性階層  
 幾乎不用思考就可以知道，樞紐分析表中的值會隨著您展開或折疊每個軸的階層，而有所增加或減少，但為什麼會這樣呢？ 答案就在屬性階層中。  
  
 摺疊所有階層，並觀察「國家/地區群組」與「日曆年度」的總計。 此值衍生自階層中稱為 **(全部) 成員** 的部分。 「(全部) 成員」是屬性階層中所有成員的計算值。  
  
-   所有「國家/地區群組」與「日期」組合的「(全部) 成員」為 $80,450,596.98  
  
-   CY2008 的「(全部) 成員」為 $16,038,062.60  
  
-   亞太的「(全部) 成員」為 $1,594,335.38  
  
 類似的彙總會與先計算並預先儲存，這就是 Analysis Services 為何具有查詢效能快速的秘密之一。  
  
 ![與所呼叫的所有成員的樞紐分析表](../media/ssas-keyconcepts-pivot2-allmember.png "標註的所有成員的樞紐分析表")  
  
 展開階層，最後您會來到最底層。 這稱為 **分葉成員**。 分葉成員是階層中沒有子系的成員。@@@ 在此範例中，Australia 為分葉成員。  
  
 ![樞紐分析表與標註-成員分葉](../media/ssas-keyconcepts-pivot3-leafparent.PNG "具有標註-成員分葉樞紐分析表")  
  
 而其上層的所有項目均稱為 **父成員**。 Pacific 是 Australia 的父系。  
  
 **屬性階層的元件**  
  
 總而言之，所有這些概念都是針對 **屬性階層**的概念而建立。 屬性階層是包含下列層級之屬性成員的樹狀結構：  
  
-   包含每個相異屬性成員的分葉層級，分葉層級的每個成員也稱為 **「分葉成員」**。  
  
-   中繼層級，如果屬性階層是父子式階層 (稍後將詳細討論)。  
  
-   包含所有子屬性之彙總值的 (全部) 成員。 您也可以在 (全部) 層級對資料而言沒有意義時，隱藏或關閉 (全部) 層級。 例如，雖然「產品代碼」為數值，卻對於總和或平均而言沒有意義 (否則會彙總所有產品代碼)。  
  
> [!NOTE]  
>  BI 開發人員通常會在屬性 (Attribute) 階層上設定屬性 (Properties)，以實現應用戶端應用程式中的特定行為，或取得某種效能優勢。 例如，您會在 (全部) 成員沒有意義的屬性 (Attribute) 上設定 AttributeHierarchyEnabled=False。 或者，您只是想要隱藏 (全部) 成員，此時可以設定 AttributeHierarchyVisible=False。 如需屬性 (Properties) 的詳細資訊，請參閱＜ [Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md) ＞。  
  
## <a name="navigation-hierarchies"></a>導覽階層  
 在樞紐分析表中 (至少在此範例中)，資料列軸和資料行軸為展開並顯示較低層級的屬性。 您可以透過在模型中建立導覽階層完成可展開的樹狀結構。  在 AdventureWorks 範例模型中，[銷售領域] 維度具有多層級階層，且層級依序為 [國家 (地區) 群組]、[國家 (地區)]、[地區]。  
  
 如您所見，會使用階層提供 PivotTable 中的導覽路徑或其他資料摘要物件。 階層有對稱及不對稱這兩種基本類型。  
  
 **對稱的階層**  
  
|||  
|-|-|  
|![標註對稱階層的樞紐分析表](../media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "標註對稱階層的樞紐分析表")|**對稱的階層** 是最上層和任何分葉成員之間存在有相同層級數目的階層。<br /><br /> **自然階層** 是從基礎資料自然轉換出的階層。 常見的範例是國家 (地區)-地區-省市，或年-月-日期，或類別目錄-子類別目錄-模型，且其中每個從屬層級會如預期般從父系跑出來。<br /><br /> 在多維度模型中，多數階層均為對稱的階層，且其中也有許多都是自然階層。<br /><br /> 另一個相關的模型化詞彙是`user-defined hierarchy`，通常用於和屬性階層進行比較。 相對於當您定義屬性時由 Analysis Services 所自動產生的屬性階層，該階層為 BI 開發人員所建立的階層。|  
  
 **不對稱的階層**  
  
|||  
|-|-|  
|![樞紐分析表與標註不完全階層](../media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "標註不完全階層的樞紐分析表")|**不完全階層** 或 **不對稱的階層** 是最上層成員和分葉成員之間存在有不同層級數目的階層。 這也是由 BI 開發人員所建立的階層，但在此情況中，資料中具有間距。<br /><br /> 在 AdventureWorks 範例模型中，[銷售領域] 維度就是不完全階層的示範，因為 United States 具有此範例中的其他國家 (地區) 所沒有的額外層級 (地區)。<br /><br /> 若用戶端應用程式不是以適當的方式處理不完全階層，則不完全階層對 BI 開發人員而言是項挑戰。 在 Analysis Services 模型中，您可以建立明確定義多層級資料間的關聯性的 **父子式階層** ，並排除某個層級如何與下一個層級相關聯中所有的模稜兩可。 請參閱[父子式階層](parent-child-dimension.md)如需詳細資訊。|  
  
## <a name="key-attributes"></a>索引鍵屬性  
 模型是相關物件的集合，且這些相關物件是依賴索引鍵和索引來建立關聯。 Analysis Services 模型也一樣。 每個維度 (請記得它相當於關聯式模型中的資料表) 都有一個索引鍵屬性。 **索引鍵屬性** 用於事實資料表 (量值群組) 的外部索引鍵關聯性。 維度中所有非索引鍵屬性均會連結至 (直接或間接) 索引鍵屬性。  
  
 一般而言 (但不一定)，索引鍵屬性也是 **資料粒度屬性**。 資料粒度是資料中的詳細資料層級或有效位數層級。 同樣地，我們要使用常見範例作為說明的最快途徑。 請思考日期值：若為每日銷售額，您必須為日期使用特定日期值；若為配額，使用每季可能便已足夠，但您的分析資料若包含體育活動的競賽結果，則資料粒度就很可能要使用毫秒。 您資料中的有效位數層級就是資料粒度。  
  
 另一個例子是貨幣：財務應用程式可能會追蹤金額至多個小數位數，但您當地學校的資金募集者也許只需要四捨五入後的整數金額。 若您想要避免儲存不必要的資料，就很需要了解資料粒度。 刪減時間戳記的毫秒，或是刪減銷售額金額中的幾分美金，都可以在詳細資料層級與您的分析無關時，節省儲存空間和處理時間。  
  
 若要設定資料粒度屬性，可使用 SQL Server Data Tools 中 Cube 設計師的 [維度使用方式] 索引標籤。 在 AdventureWorks 範例模型中，[日期] 維度的索引鍵屬性是 [日期] 索引鍵。 對於 [銷售訂單階層]，資料粒度屬性相當於索引鍵屬性。 對於 [銷售目標]，資料粒度層級為每季，所以資料粒度屬性便據此設為 [日曆季]。  
  
 ![建立顯示資料粒度屬性的模型](../media/ssas-keyconcepts-granularityattrib.png "模型顯示資料粒度屬性")  
  
> [!NOTE]  
>  若資料粒度屬性和索引鍵屬性不同，則必須將非索引鍵屬性直接或間接連結至資料粒度屬性。 在 Cube 內，資料粒度屬性會定義維度的資料粒度。  
  
## <a name="query-scope-cube-space"></a>查詢範圍 (Cube 空間)  
 查詢範圍是選取資料的界限。 範圍可從整個 Cube (Cube 是最大的查詢物件) 到某個資料格。  
  
 **Cube 空間** 是具有 Cube 量值之 Cube 屬性階層中成員的乘積。  
  
 **Subcube** 是代表已篩選之 Cube 檢視的 Cube 子集。 Subcube 可以使用 MDX 計算指令碼的 Scope 陳述式、MDX 查詢的 subselect 子句或當做工作階段 Cube 加以定義。  
  
 **資料格** 是量值維度的成員與 Cube 中每個屬性階層之成員的交集空間。  
  
## <a name="other-modeling-terms"></a>其他模型化詞彙  
 本節的概念和詞彙集合可能不完全適用於其他章節，但您還是需要了解。  
  
 **導出成員** 是在查詢時定義及計算的維度成員。 導出成員可以定義在使用者查詢或 MDX 計算指令碼中，並且儲存在伺服器。 導出成員會對應到定義所在之維度中的資料表資料列。  
  
 **相異計數** 是特殊的量值類型，用於只應計數一次的資料項目。 AdventureWorks 範例模型包含 [網際網路訂單]、[轉售商訂單] 和 [銷售訂單階層] 的相異計數量值。  
  
 **量值群組** 是一或多個量值的集合。 大多數的量值群組都是使用者定義，且可讓您用於使相關的量值聚在一起。 相異計數量值為例外狀況。 相異計數量值會一律放在只包含相異量值的專用量值群組中。 您無法在樞紐分析表範例圖中看到此量值群組，但此量值群組確實會在樞紐分析表欄位清單中顯示為為具名的量值集合。  
  
 **量值維度** 是包含 Cube 中所有量值的維度。 它不會顯示在您於 SQL Server Data Tools 中建立的多維度模型中，但它仍然是存在的。 因為它包含量值，而量值維度的所有成員一般而言都已經匯總 (通常是使用總和或計數)。  
  
 **資料庫維度和 Cube 維度**。 您可以在模型中定義獨立維度，然後獨立維度便會包含在相同模型中任意數量的 Cube 中。 當您將維度加入 Cube 時，維度又稱為 Cube 維度。 而單獨在專案中作為物件總管中的獨立項目時，則稱為資料庫維度。 為何要如此區分？ 因為這樣您才可以分別對它們設定屬性 (Property)。 您會在產品文件中看到同時使用這兩個詞彙，所以了解它們的含意有其價值。  
  
## <a name="next-steps"></a>後續步驟  
 現在您已經認識了重要的概念和術語，您可以繼續閱讀這些其他主題，以進一步了解 Analysis Services 中的基本概念：  
  
-   [基本 MDX 查詢&#40;MDX&#41;](mdx/mdx-query-the-basic-query.md)  
  
-   [基本 MDX 指令碼&#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md)  
  
-   [多維度模型化&#40;Adventure Works 教學課程&#41;](../multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cube 空間](mdx/cube-space.md)   
 [Tuple](mdx/tuples.md)   
 [「 自動存在 」](mdx/autoexists.md)   
 [使用成員、 Tuple 和集合&#40;MDX&#41;](mdx/working-with-members-tuples-and-sets-mdx.md)   
 [視覺化總計和非視覺化總計](mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 查詢基礎觀念&#40;Analysis Services&#41;](mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 指令碼基礎觀念&#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [MDX 語言參考&#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [多維度運算式&#40;MDX&#41;參考](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
