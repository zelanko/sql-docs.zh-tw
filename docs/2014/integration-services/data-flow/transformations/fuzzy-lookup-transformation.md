---
title: 模糊查閱轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0b77d45ca55adaa85e4e37e9da817f325ce0fc7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900313"
---
# <a name="fuzzy-lookup-transformation"></a>模糊查閱轉換
  「模糊查閱」轉換會執行資料清除工作，例如標準化資料、更正資料及提供遺漏值。  
  
> [!NOTE]  
>  如需模糊查閱轉換 (包括效能和記憶體限制) 的詳細資訊，請參閱 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(SQL Server Integration Services 2005 中的模糊查閱和模糊群組) 白皮書。  
  
 「模糊查詢」轉換與「查閱」轉換的不同之處在於其使用模糊比對。 「查閱」轉換使用等聯結 (Equi-Join)，在參考資料表中尋找相符的資料錄。 它會傳回至少有一項相符資料錄的資料錄，以及傳回沒有任何相符資料錄的資料錄。 相反地，「模糊查閱」轉換會使用模糊比對，傳回參考資料表中的一個或多個相近相符項目。  
  
 在封裝資料流程中，「模糊查閱」轉換經常在「查閱」轉換後發生。 首先，「查閱」轉換會嘗試尋找完全相符項目。 如果找不到，「模糊查閱」轉換會提供參考資料表中的相近相符項目。  
  
 轉換需要存取包含用於清除和擴充輸入資料之值的參考資料來源。 參考資料來源必須是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中的資料表。 輸入資料行中的值與參考資料表中的值之間的比對可能是完全相符或模糊相符。 不過，轉換至少需要一個資料行相符，才能設定進行模糊比對。 如果只想要使用完全比對，請改為使用「查閱」轉換。  
  
 此轉換有一個輸入和一個輸出。  
  
 只有具有 `DT_WSTR` 和 `DT_STR` 資料類型的輸入資料行可用於模糊比對。 完全比對可使用任何 DTS 資料類型，但 `DT_TEXT`、`DT_NTEXT` 和 `DT_IMAGE` 除外。 如需詳細資訊，請參閱 [Integration Services 資料類型](../integration-services-data-types.md)。 參與輸入與參考資料表之間聯結的資料行必須具有相容的資料類型。 比方說，它是用於將具有 DTS 資料行聯結`DT_WSTR`行的資料型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]`nvarchar`加入的資料行的資料類型，但是無效`DT_WSTR`資料行的資料型別`int`資料型別。  
  
 您可以指定最大記憶體數量、資料列比較演算法，以及轉換使用的索引和參考資料表快取，以自訂此轉換。  
  
 您可以透過設定 MaxMemoryUsage 自訂屬性來設定模糊查閱轉換所使用的記憶體數量。 您可以指定百萬位元組 (MB) 數，或是使用 0 值，讓轉換依據其需求與可用實體記憶體，使用動態的記憶體數量。 屬性運算式可以在載入封裝時更新 MaxMemoryUsage 自訂屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; Expressions](../../expressions/integration-services-ssis-expressions.md) (Integration Services (SSIS) 運算式)、[Use Property Expressions in Packages](../../expressions/use-property-expressions-in-packages.md) (在封裝中使用屬性運算式) 和[轉換自訂屬性](transformation-custom-properties.md)。  
  
## <a name="controlling-fuzzy-matching-behavior"></a>控制模糊比對行為  
 「模糊查閱」轉換包含三種用於自訂其所執行之查閱的功能：每個輸入資料列傳回的相符項目上限、Token 分隔符號，以及相似度臨界值。  
  
 轉換會傳回零或多個相符項目，最多可傳回指定的相符項目數。 指定相符項目上限並不會保證轉換傳回最大數目的相符項目，而只會保證轉換最多傳回該數目的相符項目。 如果您將相符項目上限設為大於 1 的值，則每個查閱的轉換輸出可能會包含一個以上的資料列，且部分資料列可能是重複的。  
  
 轉換會提供用於 Token 化資料的預設分隔符號集，但您可以加入 Token 分隔符號，以符合資料的需要。 Delimiters 屬性包含預設分隔符號。 Token 化是十分重要的，這是因為它會定義資料內相互比較的單位。  
  
 相似度臨界值可在元件和聯結層級進行設定。 僅當轉換在輸入和參考資料表中的資料行之間執行模糊比對時，聯結層級相似度臨界值才可用。 相似度範圍是從 0 到 1。 臨界值愈接近 1，資料列和資料行就愈近似於重複項目。 透過在元件和聯結層級設定 MinSimilarity 屬性，可以指定相似度臨界值。 為滿足在元件層級指定的相似度，所有資料列之所有相符項目的相似度都必須大於或等於在元件層級指定的相似度臨界值。 也就是說，您無法在元件層級指定非常相近的相符，除非資料列或聯結層級的相符具有相同的相似度。  
  
 每個相符都包括相似度分數和信心分數。 相似度分數是輸入資料錄與「模糊查閱」轉換從參考資料表傳回之資料錄之間文字相似度的數學量值。 信心分數是指特定值在參考資料表眾多相符項目中為最相符項目之可能性的量值。 指派給資料錄的信心分數會視傳回的其他相符資料錄而定。 例如，比對 *St.* 與 *Saint* 會傳回較低的相似度分數，無論其他相符項目為何。 如果 *Saint* 是傳回的唯一相符項目，則信心分數會很高。 如果 *Saint* 和 *St.* 都在參考資料表中，則 *St.* 的信心較高，而 *Saint* 的信心較低。 不過，高相似度可能並不意味著高信心。 例如，如果您是在查閱值 *Chapter 4*，則所傳回的結果 *Chapter 1*、 *Chapter 2*和 *Chapter 3* 都會具有很高的相似度分數，但信心分數卻都較低，原因是並不清楚結果中的哪一個項目是最相符的項目。  
  
 相似度分數由介於 0 與 1 之間的十進位值表示，其中相似度分數 1 表示輸入資料行中的值與參考資料表中的值之間完全相符。 信心分數也是介於 0 與 1 之間的十進位值，它表示對相符的信心。 如果找不到可用的相符項目，則會將相似度和信心分數 0 指派給資料列，且從參考資料表複製的輸出資料行將包含 Null 值。  
  
 有時，「模糊查閱」在參考資料表中可能找不到適當的相符項目。 如果查閱中使用的輸入值是單一短字，則可能會發生這種狀況。 例如，如果該資料行或資料列的任何其他資料行中沒有其他 Token，則 *helo* 與參考資料表中的值 *hello* 不相符。  
  
 轉換輸出資料行包括標示為傳遞資料行的輸入資料行、在查閱資料表中選取的資料行，以及下列其他資料行：  
  
-   **_Similarity**，描述輸入與參考資料行中值之間相似度的資料行。  
  
-   **_Confidence**，描述相符品質的資料行。  
  
 轉換會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫連接，以建立模糊比對演算法所使用的暫存資料表。  
  
## <a name="running-the-fuzzy-lookup-transformation"></a>執行模糊查閱轉換  
 當封裝首次執行轉換時，轉換會複製參考資料表、將具有整數資料類型的索引鍵加入新資料表，並在索引鍵資料行上建立索引。 接著，轉換會在參考資料表的副本上建立索引，稱為相符索引。 相符索引會將值的 Token 化結果儲存在轉換輸入資料行中，轉換接著會在查閱作業中使用該 Token。 相符索引是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中的資料表。  
  
 當封裝再次執行時，轉換可使用現有的相符索引，也可建立新索引。 如果參考資料表是靜態的，則封裝可以避免發生費時的程序，以便為資料清除的重複工作階段重建索引。 如果選擇使用現有的索引，則該索引是在封裝首次執行時建立的。 如果多個「模糊查閱」轉換使用相同的參考資料表，則它們都可使用同一索引。 若要重複使用索引，查閱作業必須是相同的，且查閱必須使用相同的資料行。 您可以命名索引，並選取儲存索引之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的連接。  
  
 如果轉換儲存相符索引，則該相符索引可自動維護。 這表示每次更新參考資料表中的資料錄時，也會更新相符索引。 維護相符索引可節約處理時間，因為封裝執行時無需重建索引。 您可以指定轉換如何管理相符索引。  
  
 下表描述相符索引選項。  
  
|選項|描述|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|建立、儲存並維護新索引。 轉換會在參考資料表上安裝觸發程序，以讓參考資料表與索引資料表同步。|  
|**GenerateAndPersistNewIndex**|建立並儲存新索引，但不對其進行維護。|  
|**GenerateNewIndex**|建立新索引，但不對其進行儲存。|  
|**ReuseExistingIndex**|重複使用現有的索引。|  
  
### <a name="maintenance-of-the-match-index-table"></a>相符索引資料表的維護  
 **GenerateAndMaintainNewIndex** 選項會在參考資料表上安裝觸發程序，讓相符索引資料表與參考資料表同步。 如果您必須移除已安裝的觸發程序，則必須執行 **sp_FuzzyLookupTableMaintenanceUnInstall** 預存程序，並提供 MatchIndexName 屬性中指定的名稱作為輸入參數值。  
  
 在執行 **sp_FuzzyLookupTableMaintenanceUnInstall** 預存程序之前，您不應刪除所維護的相符索引資料表。 一旦刪除相符索引資料表，參考資料表上的觸發程序就無法再正確執行。 參考資料表的所有後續更新都將失敗，直到您手動卸除參考資料表上的觸發程序為止。  
  
 SQL TRUNCATE TABLE 命令不會叫用 DELETE 觸發程序。 如果在參考資料表上使用 TRUNCATE TABLE 命令，則參考資料表和相符索引將不再同步，且「模糊查閱」轉換會失敗。 在參考資料表上安裝維護相符索引資料表的觸發程序時，您應該使用 SQL DELETE 命令，而不是 TRUNCATE TABLE 命令。  
  
> [!NOTE]  
>  當您在 **[模糊查閱轉換編輯器]** 的 **[參考資料表]** 索引標籤上選取 **[維護儲存的索引]** 時，轉換會使用具名預存程序來維護索引。 這些 Managed 預存程序會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的 Common Language Runtime (CLR) 整合功能。 根據預設，不會啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 CLR 整合功能。 若要使用 **[維護儲存的索引]** 功能，您必須啟用 CLR 整合。 如需詳細資訊，請參閱 [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md)。  
>   
>  因為 [維護儲存的索引]  選項需要 CLR 整合，因此只有當您在已啟用 CLR 整合的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上選取參考資料表時，這項功能才有效。  
  
## <a name="row-comparison"></a>資料列比較  
 設定模糊查閱轉換時，您可以指定轉換在參考資料表中尋找相符記錄時所使用的比較演算法。 如果您將 Exhaustive 屬性設定為`True`，則轉換會比較輸入與參考資料表中的每個資料列中的每個資料列。 此比較演算法可產生更精確的結果，但很可能會讓轉換的執行速度更慢，除非參考資料表中的資料列數目較小。 如果將 Exhaustive 屬性設為`True`，將整個參考資料表載入記憶體。 若要避免效能問題，建議您將 Exhaustive 屬性設為`True`套件僅在開發期間。  
  
 如果將 Exhaustive 屬性設為`False`，模糊查閱 」 轉換會傳回只具有至少一個索引的 token 或子字串相符項目 (此子字串稱為*q 字母組*) 與輸入記錄相同。 為了達到最高的查閱效率，模糊查閱轉換只會在它用來尋找相符項目的反向索引結構中，檢索資料表內每個資料列中的一個 Token 子集。 如果輸入資料集很小，您可以將 Exhaustive 設定為`True`為了避免遺漏，存在於索引資料表中沒有通用 token 的相符項目。  
  
## <a name="caching-of-indexes-and-reference-tables"></a>索引和參考資料表的快取  
 設定「模糊查閱」轉換時，您可以指定在轉換執行其工作之前，是否在記憶體中部分快取索引和參考資料表。 如果您將 WarmCaches 屬性設`True`，索引和參考資料表載入記憶體。 當輸入中的多個資料列，將 WarmCaches 屬性設定為`True`可改進轉換的效能。 如果輸入資料列數目很小，將 WarmCaches 屬性設定為`False`可重複使用大型索引更快。  
  
## <a name="temporary-tables-and-indexes"></a>暫存資料表和索引  
 在執行階段，「模糊查閱」轉換會在轉換連接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中建立暫存物件，例如資料表和索引。 這些暫存資料表和索引的大小，與參考資料表中的資料列和 Token 數目，以及「模糊查閱」轉換所建立的 Token 數目成正比，因此它們會佔用相當大的磁碟空間。 轉換還會查詢這些暫存資料表。 因此，您應該考量將「模糊查閱」轉換連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的非生產執行個體，特別是當生產伺服器的可用磁碟空間十分有限時。  
  
 如果此轉換所使用的資料表和索引在本機電腦上，則轉換的效能會有所改進。 如果「模糊查閱」轉換所使用的參考資料表在生產伺服器上，則應考量將資料表複製到非生產伺服器，並設定「模糊查閱」轉換存取該副本。 如此一來，您就可避免查閱查詢耗用生產伺服器上的資源。 此外，如果「模糊查閱」轉換維護相符索引 (也就是說，如果將 MatchIndexOptionsis 設為 **GenerateAndMaintainNewIndex**)，則轉換可能會在資料清除作業期間鎖定參考資料表，以防止其他使用者和應用程式存取該資料表。  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>設定模糊查閱轉換  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可在 **[模糊查閱轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [模糊查閱轉換編輯器 &#40;參考資料表索引標籤&#41;](../../fuzzy-lookup-transformation-editor-reference-table-tab.md)  
  
-   [模糊查閱轉換編輯器 &#40;資料行索引標籤&#41;](../../fuzzy-lookup-transformation-editor-columns-tab.md)  
  
-   [模糊查閱轉換編輯器 &#40;進階索引標籤&#41;](../../fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定資料流程元件屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [查閱轉換](lookup-transformation.md)   
 [模糊群組轉換](fuzzy-grouping-transformation.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
