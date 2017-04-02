---
title: "模糊群組轉換 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzygroupingtrans.f1"
helpviewer_keywords: 
  - "清除資料"
  - "比較資料"
  - "Token 分隔符號 [Integration Services]"
  - "暫存索引 [Integration Services]"
  - "模糊群組轉換"
  - "暫存資料表 [Integration Services]"
  - "群組資料"
  - "標準化資料 [Integration Services]"
  - "資料行 [Integration Services], 標準化"
  - "相似度臨界值 [Integration Services]"
  - "資料清除 [Integration Services]"
  - "重複資料 [Integration Services]"
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 模糊群組轉換
  「模糊群組」轉換會透過識別可能重複的資料列並選取用於標準化資料的標準資料列，執行資料清除工作。  
  
> [!NOTE]  
>  如需模糊群組轉換 (包括效能和記憶體限制) 的詳細資訊，請參閱 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604) (SQL Server Integration Services 2005 中的模糊查閱和模糊群組) 白皮書。  
  
 「模糊群組」轉換需要連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體，以建立轉換演算法執行其工作所需的暫存 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 連接必須解析為具有在資料庫中建立資料表之權限的使用者。  
  
 若要設定轉換，您必須選取要在識別重複項目時使用的輸入資料行，還必須為每個資料行選取相符類型 (模糊或完全)。 完全相符保證只會將該資料行中具有相同值的那些資料列分組。 完全比對可套用到任何 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型的資料行，但 DT_TEXT、DT_NTEXT 和 DT_IMAGE 除外。 模糊相符會將有近似相同值的資料列分組。 資料之近似比對的方法以使用者指定的相似度分數為基礎。 只有具有 DT_WSTR 和 DT_STR 資料類型的資料行可用於模糊比對。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 轉換輸出包括所有輸入資料行、一或多個具有標準化資料的資料行，以及包含相似度分數的資料行。 分數是介於 0 到 1 之間的十進位值。 標準資料列的分數是 1。 模糊群組中其他資料列的分數指出資料列與標準資料列的相符程度。 分數愈接近於 1，資料列與標準資料列的相符程度就愈高。 如果模糊群組包括的資料列是與標準資料列完全重複的資料列，則這些資料列的分數也是 1。 轉換不會移除重複的資料列，而是建立一個將標準資料列與相似資料列產生關聯的索引鍵，將這些重複的資料列分組。  
  
 轉換會為每個輸入資料列產生一個輸出資料列，並具有下列其他資料行：  
  
-   **_key_in**，唯一識別每個資料列的資料行。  
  
-   **_key_out**，識別一組重複資料列的資料行。 **_key_out** 資料行具有標準資料列中 **_key_in** 資料行的值。 具有與 **_key_out** 相同值的資料列屬於同一群組。 群組的 **_key_out** 值與標準資料列中 **_key_in** 的值相對應。  
  
-   **_score**，介於 0 與 1 之間的值，指出輸入資料列與標準資料列的相似度。  
  
 以上名稱是預設資料行名稱，您可以設定「模糊分組」轉換使用其他名稱。 輸出也為參與模糊群組的每個資料行提供相似度分數。  
  
 「模糊群組」轉換包括兩個自訂其所執行之群組的功能：Token 分隔符號和相似度臨界值。 轉換會提供用於Token 化資料的預設分隔符號集，但您可以加入新的分隔符號，以改進資料的 Token 化。  
  
 相似度臨界值指出轉換識別重複項目的嚴格程度。 相似度臨界值可在元件和資料行層級進行設定。 資料行層級相似度臨界值只可用於執行模糊相符的資料行。 相似度範圍是從 0 到 1。 臨界值愈接近 1，資料列和資料行就愈近似於重複項目。 透過在元件和資料行層級設定 MinSimilarity 屬性，可以指定資料列和資料行間的相似度臨界值。 為滿足在元件層級指定的相似度，所有資料列之所有資料行的相似度都必須大於或等於在元件層級指定的相似度臨界值。  
  
 「模糊群組」轉換會計算相似度的內部量值，且不會將與 MinSimilarity 中指定之值不相似的資料列分組。  
  
 若要識別資料所使用的相似度臨界值，您可能必須使用不同的最小相似度臨界值，數次套用「模糊群組」轉換。 在執行階段，轉換輸出中的分數資料行會包含群組中每個資料列的相似度分數。 您可以使用這些值識別適用於資料的相似度臨界值。 如果您要增加相似度，則應該將 MinSimilarity 設為大於分數資料行中之值的值。  
  
 透過在「模糊群組」轉換輸入中設定資料行的屬性，可以自訂轉換所執行的群組。 例如，FuzzyComparisonFlags 屬性會指定轉換如何比較資料行中的字串資料，ExactFuzzy 屬性則指定轉換是執行模糊相符還是完全相符。  
  
 您可以透過設定 MaxMemoryUsage 自訂屬性來設定模糊群組轉換所使用的記憶體數量。 您可以指定百萬位元組 (MB) 數，或是使用 0 值，讓轉換能夠依據其需求與可用實體記憶體，使用動態的記憶體數量。 屬性運算式可以在載入封裝時更新 MaxMemoryUsage 自訂屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
## 資料列比較  
 設定模糊群組轉換時，您可以指定轉換在比較轉換輸入中的資料列時所使用的比較演算法。 如果您將 Exhaustive 屬性設為 **true**，則轉換會比較輸入中的每一個資料列與輸入中的每個其他資料列。 此比較演算法可產生更精確的結果，但很可能會讓轉換的執行速度更慢，除非輸入中的資料列數目較小。 為避免效能問題，建議僅在封裝開發期間將 Exhaustive 屬性設為 **true**。  
  
## 暫存資料表和索引  
 在執行階段，「模糊群組」轉換會在轉換連接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中建立暫存物件，例如資料表和索引 (它們的大小可能相當大)。 資料表和索引的大小與轉換輸入中的資料列數目和「模糊群組」轉換所建立的 Token 數目成正比。  
  
 轉換還會查詢暫存資料表。 因此，您應該考量將「模糊群組」轉換連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的非生產執行個體，特別是當生產伺服器的可用磁碟空間十分有限時。  
  
 如果此轉換所使用的資料表和索引在本機電腦上，則轉換的效能會有所改進。  
  
## 模糊群組轉換的組態  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [模糊群組轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [模糊群組轉換編輯器 &#40;連線管理員索引標籤&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [模糊群組轉換編輯器 &#40;資料行索引標籤&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [模糊群組轉換編輯器 &#40;進階索引標籤&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../Topic/Common%20Properties.md)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## 相關工作  
 如需有關如何設定此工作屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用模糊群組轉換來識別相似的資料列](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## 請參閱＜  
 [模糊查閱轉換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  