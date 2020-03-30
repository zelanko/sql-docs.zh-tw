---
title: 模糊群組轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fuzzygroupingtrans.f1
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e8cec010923591d3fc05ef2920578bdebc4f9f5c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297940"
---
# <a name="fuzzy-grouping-transformation"></a>模糊群組轉換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「模糊群組」轉換會透過識別可能重複的資料列並選取用於標準化資料的標準資料列，執行資料清除工作。  
  
> [!NOTE]  
>  如需模糊群組轉換 (包括效能和記憶體限制) 的詳細資訊，請參閱 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(SQL Server Integration Services 2005 中的模糊查閱和模糊群組) 白皮書。  
  
 「模糊群組」轉換需要連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體，以建立轉換演算法執行其工作所需的暫存 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 連接必須解析為具有在資料庫中建立資料表之權限的使用者。  
  
 若要設定轉換，您必須選取要在識別重複項目時使用的輸入資料行，還必須為每個資料行選取相符類型 (模糊或完全)。 完全相符保證只會將該資料行中具有相同值的那些資料列分組。 完全比對可套用到任何 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型的資料行，但 DT_TEXT、DT_NTEXT 和 DT_IMAGE 除外。 模糊相符會將有近似相同值的資料列分組。 資料之近似比對的方法以使用者指定的相似度分數為基礎。 只有具有 DT_WSTR 和 DT_STR 資料類型的資料行可用於模糊比對。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
 轉換輸出包括所有輸入資料行、一或多個具有標準化資料的資料行，以及包含相似度分數的資料行。 分數是介於 0 到 1 之間的十進位值。 標準資料列的分數是 1。 模糊群組中其他資料列的分數指出資料列與標準資料列的相符程度。 分數愈接近於 1，資料列與標準資料列的相符程度就愈高。 如果模糊群組包括的資料列是與標準資料列完全重複的資料列，則這些資料列的分數也是 1。 轉換不會移除重複的資料列，而是建立一個將標準資料列與相似資料列產生關聯的索引鍵，將這些重複的資料列分組。  
  
 轉換會為每個輸入資料列產生一個輸出資料列，並具有下列其他資料行：  
  
-   **_key_in**，唯一識別每個資料列的資料行。  
  
-   **_key_out**，識別一組重複資料列的資料行。 **_key_out** 資料行具有標準資料列中 **_key_in** 資料行的值。 具有與 **_key_out** 相同值的資料列屬於同一群組。 群組的 **_key_out**值與標準資料列中 **_key_in** 的值相對應。  
  
-   **_score**，介於 0 與 1 之間的值，指出輸入資料列與標準資料列的相似度。  
  
 以上名稱是預設資料行名稱，您可以設定「模糊分組」轉換使用其他名稱。 輸出也為參與模糊群組的每個資料行提供相似度分數。  
  
 「模糊群組」轉換包括兩個自訂其所執行之群組的功能：Token 分隔符號和相似度臨界值。 轉換會提供用於Token 化資料的預設分隔符號集，但您可以加入新的分隔符號，以改進資料的 Token 化。  
  
 相似度臨界值指出轉換識別重複項目的嚴格程度。 相似度臨界值可在元件和資料行層級進行設定。 資料行層級相似度臨界值只可用於執行模糊相符的資料行。 相似度範圍是從 0 到 1。 臨界值愈接近 1，資料列和資料行就愈近似於重複項目。 透過在元件和資料行層級設定 MinSimilarity 屬性，可以指定資料列和資料行間的相似度臨界值。 為滿足在元件層級指定的相似度，所有資料列之所有資料行的相似度都必須大於或等於在元件層級指定的相似度臨界值。  
  
 「模糊群組」轉換會計算相似度的內部量值，且不會將與 MinSimilarity 中指定之值不相似的資料列分組。  
  
 若要識別資料所使用的相似度臨界值，您可能必須使用不同的最小相似度臨界值，數次套用「模糊群組」轉換。 在執行階段，轉換輸出中的分數資料行會包含群組中每個資料列的相似度分數。 您可以使用這些值識別適用於資料的相似度臨界值。 如果您要增加相似度，則應該將 MinSimilarity 設為大於分數資料行中之值的值。  
  
 透過在「模糊群組」轉換輸入中設定資料行的屬性，可以自訂轉換所執行的群組。 例如，FuzzyComparisonFlags 屬性會指定轉換如何比較資料行中的字串資料，ExactFuzzy 屬性則指定轉換是執行模糊相符還是完全相符。  
  
 您可以透過設定 MaxMemoryUsage 自訂屬性來設定模糊群組轉換所使用的記憶體數量。 您可以指定百萬位元組 (MB) 數，或是使用 0 值，讓轉換能夠依據其需求與可用實體記憶體，使用動態的記憶體數量。 屬性運算式可以在載入封裝時更新 MaxMemoryUsage 自訂屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
## <a name="row-comparison"></a>資料列比較  
 設定模糊群組轉換時，您可以指定轉換在比較轉換輸入中的資料列時所使用的比較演算法。 如果您將 Exhaustive 屬性設為 **true**，則轉換會比較輸入中的每一個資料列與輸入中的每個其他資料列。 此比較演算法可產生更精確的結果，但很可能會讓轉換的執行速度更慢，除非輸入中的資料列數目較小。 為避免效能問題，建議僅在封裝開發期間將 Exhaustive 屬性設為 **true** 。  
  
## <a name="temporary-tables-and-indexes"></a>暫存資料表和索引  
 在執行階段，「模糊群組」轉換會在轉換連接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中建立暫存物件，例如資料表和索引 (它們的大小可能相當大)。 資料表和索引的大小與轉換輸入中的資料列數目和「模糊群組」轉換所建立的 Token 數目成正比。  
  
 轉換還會查詢暫存資料表。 因此，您應該考量將「模糊群組」轉換連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的非生產執行個體，特別是當生產伺服器的可用磁碟空間十分有限時。  
  
 如果此轉換所使用的資料表和索引在本機電腦上，則轉換的效能會有所改進。  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>模糊群組轉換的組態  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何設定此工作屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用模糊群組轉換來識別相似的資料列](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>模糊群組轉換編輯器 (連接管理員索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[連接管理員]** 索引標籤，來選取現有的連接或建立新的連接。  
  
> [!NOTE]  
>  連接所指定的伺服器必須正在執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 模糊群組轉換會在 tempdb 中建立暫存資料物件，而這個物件可能會與轉換的完整輸出一樣大。 當轉換執行時，它會對這些暫存物件發出伺服器查詢。 這樣會影響伺服器的整體效能。  
  
### <a name="options"></a>選項。  
 **[無快取]**  
 使用清單方塊來選取現有的 OLE DB 連接管理員，或使用 [新增]  按鈕來建立新的連接。  
  
 **新增**  
 使用 [設定 OLE DB 連接管理員]  對話方塊來建立新的連接。  
  
## <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>模糊群組轉換編輯器 (資料行索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[資料行]** 索引標籤，即可指定用於將具有重複值之資料列分組的資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 從清單中選取輸入資料行，即可依據該資料行將具有重複值的資料列分組。  
  
 **名稱**  
 檢視可用之輸入資料行的名稱。  
  
 **通過**  
 選取轉換的輸出是否包含輸入資料行。 用來分組的所有資料行，都會自動複製到輸出。 您可以核取此資料行來包含其他資料行。  
  
 **輸入資料行**  
 選取先前在 [可用的輸入資料行]  清單中選取的其中一個輸入資料行。  
  
 **輸出別名**  
 輸入對應之輸出資料行的描述性名稱。 依預設，輸出資料行的名稱會與輸入資料行的名稱相同。  
  
 **群組輸出別名**  
 輸入資料行的描述性名稱，資料行包含已分組重複項目的標準值。 此輸出資料行的預設名稱，是輸入資料行的名稱後面附加「_clean」。  
  
 **比對類型**  
 選取模糊相符或完全相符。 如果資料列在具有模糊比對類型的所有資料行之間非常相似，資料列才會被視為重複項目。 如果您同時在特定資料行上指定完全相符，則只有當需要完全相符之資料行中的資料列值完全相同時，資料列才會被視為可能重複的項目。 因此，如果您知道特定資料行不會有錯誤或不一致的情形，就可以在該資料行上指定完全相符，以提高其他資料行的模糊比對精確度。  
  
 **最小相似度**  
 使用滑桿設定聯結層級的相似度臨界值。 此值越接近 1，查閱值與來源值的相似度必須越接近才能認定為相符。 增加臨界值可改善比對速度，因為需要考慮的候選記錄越少。  
  
 **相似度輸出別名**  
 指定新輸出資料行的名稱，此資料行包含所選取聯結的相似度分數。 如果您將此值保留空白，就不會建立輸出資料行。  
  
 **數字**  
 指定比較資料行資料時，開頭和尾端數字的顯著性。 例如，假設開頭數字屬於顯著，則 "123 Main Street" 和 "456 Main Street" 將不會被分到相同的群組中。  
  
|值|描述|  
|-----------|-----------------|  
|**兩者皆非**|開頭和尾端數字皆屬於不顯著。|  
|**開頭**|僅開頭數字屬於顯著。|  
|**尾端**|僅尾端數字屬於顯著。|  
|**LeadingAndTrailing**|開頭和尾端數字皆屬於顯著。|  
  
 **比較旗標**  
 如需字串比較選項的資訊，請參閱 [比較字串資料](../../../integration-services/data-flow/comparing-string-data.md)。  
  
## <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>模糊群組轉換編輯器 (進階索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[進階]** 索引標籤，即可指定輸入和輸出資料行、設定類似度臨界值，以及定義分隔符號。  
  
> [!NOTE]  
>  在 **[模糊群組轉換編輯器]** 中無法使用模糊群組轉換的 **Exhaustive** 和 **MaxMemoryUsage**屬性，但可使用 **[進階編輯器]** 來設定這兩個屬性。 如需有關這些屬性的詳細資訊，請參閱＜ [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)＞的「模糊群組轉換」一節。  
  
### <a name="options"></a>選項。  
 **輸入索引鍵資料行名稱**  
 針對每個輸入資料列，指定包含資料列之唯一識別碼的輸出資料行名稱。 **_key_in** 資料行具有能唯一識別每個資料列的值。  
  
 **輸出索引鍵資料行名稱**  
 針對由一組重複資料列組成的標準資料列，指定包含標準資料列之唯一識別碼的輸出資料行名稱。 **_key_out** 資料行會對應至標準資料之資料列的 **_key_in** 值。  
  
 **相似度分數資料行名稱**  
 指定包含相似度分數之資料行的名稱。 相似度分數是介於 0 與 1 的值，以表示輸入資料列與標準資料列的相似度。 分數愈接近於 1，資料列與標準資料列的相符程度就愈高。  
  
 **相似度臨界值**  
 使用滑桿來設定相似度臨界值。 臨界值越接近 1，資料列就必須彼此更相似才能判定為重複。 增加臨界值可以改善比對的速度，因為需要考慮的候選記錄比較少。  
  
 **Token 分隔符號**  
 此項轉換提供了 Token 化資料所用的預設分隔符號集，但您可以依需要編輯清單來新增或移除分隔符號。  
  
## <a name="see-also"></a>另請參閱  
 [模糊查閱轉換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
