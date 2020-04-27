---
title: 選擇建立全文檢索索引時的語言 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5f045933735d2a26b1e9007868f96680bef4fc47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012726"
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>選擇建立全文檢索索引時的語言
  建立全文檢索索引時，您必須針對索引資料行指定資料行層級語言。 此資料行的全文檢索查詢將會使用指定之語言的 [斷詞工具與詞幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md) 。 在建立全文檢索索引並選擇資料行語言時，必須考慮一些事項。 這些考量與文字如何 Token 化，然後如何由全文檢索引擎編製索引有關。  
  
> [!NOTE]  
>  若要針對全文檢索索引的資料行指定資料行層級語言，請在指定資料行時，使用 LANGUAGE *language_term* 子句。 如需詳細資訊，請參閱 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql) 和 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
##  <a name="language-support-in-full-text-search"></a><a name="langsupp"></a> 全文檢索搜尋中的語言支援  
 本節提供斷詞工具與字幹分析器的簡介，並且討論了全文檢索搜尋如何使用資料行層級語言的 LCID。  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>斷詞工具與字幹分析器的簡介  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本包含全新系列的斷詞工具與字幹分析器，這些工具明顯比先前 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所提供的工具更好。  
  
> [!NOTE]  
>  Microsoft Natural Language Group (MS NLG) 已實作而且支援這些新的語言元件。  
  
 新的斷詞工具提供下列優勢：  
  
-   健全性  
  
     經測試顯示，新的斷詞工具在高度壓力的查詢環境中仍然保持健全狀態。  
  
-   安全性  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]由於語言元件中的安全性改進，預設會啟用新的斷詞工具。 我們強烈建議您應該簽署外部元件 (例如，斷詞工具和篩選)，以便改善 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的整體安全性和健全性。 您可以設定全文檢索來確認這些元件是否已簽署，方法如下所示：  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   品質  
  
     斷詞工具已經重新設計過，而且經測試顯示，新的斷詞工具會比先前的斷詞工具提供較佳的語意品質。 這會增加重新叫用精確度。  
  
-   大部分語言的斷詞工具都已包含在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中而且預設已啟用。  
  
 如需[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]包含斷詞工具和字幹分析器的語言清單，請參閱[fulltext_languages &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。  
  

  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>全文檢索搜尋如何使用資料行層級語言的名稱  
 建立全文檢索索引時，您必須針對每個資料行指定有效的語言名稱。 如果某個語言名稱有效，但是 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) 目錄檢視並未傳回該語言名稱，全文檢索搜尋就會尋求相同語系中最接近的可用語言名稱 (如果有的話)。 否則，全文檢索搜尋會尋求中性斷詞工具。 這種尋求的行為可能會影響重新叫用精確度。 因此，在建立全文檢索索引時，我們強烈建議您針對每個資料行指定有效且可用的語言名稱。  
  
> [!NOTE]  
>  系統會針對適用於全文檢索索引的所有資料類型 (例如 `char` 或 `nchar`) 使用 LCID。 如果您將 `char`、`varchar` 或 `text` 類型資料行的排序次序設定為與 LCID 所識別之語言不同的語言設定，在全文檢索索引和查詢這些資料行期間，系統仍然會使用 LCID。  
  

  
##  <a name="word-breaking"></a><a name="breaking"></a> 斷詞  
 斷詞工具會針對文字分界 (語言特有) 將索引的文字 Token 化。 因此，不同語言之間的斷詞行為便有所差異。 如果您使用某種語言 x 來索引一些語言 {x、y 和 z}，某些行為可能會產生非預期的結果。 例如，在某種語言中，破折號 (-) 或逗號 (,) 可能是棄而不用的斷詞元素，但在另一種語言中則不是。 此外，由於給定的字詞可能會在不同的語言中以不同方式進行詞幹分析，因此有時可能也會發生非預期的詞幹分析行為。 例如，在英文中，文字分界通常是空白字元或某種形式的標點符號。 在其他語言中，例如德文，字詞或字元可能會結合在一起。 因此，您所選擇的資料行層級語言應該代表您預期會儲存在該資料行之資料列中的語言。  
  
### <a name="western-languages"></a>西方語言  
 對於西方語系而言，如果您不確定哪些語言會儲存在資料行中，或者您預期會儲存多種語言，一般的解決方法是使用可能儲存在資料行中之最複雜語言的斷詞工具。 例如，您可能預期會在單一資料行中儲存英文、西班牙文和德文的內容。 這三種西方語言都擁有非常相似的斷詞模式，其中德文的模式最複雜。 因此，在這個情況下，使用德文斷詞工具是不錯的選擇，因為它能夠正確地處理英文和西班牙文的文字。 相較之下，英文斷詞工具可能無法完美地處理德文的文字，因為德文含有複合字。  
  
 請注意，使用某個語系中最複雜語言的斷詞工具並不保證能夠針對該語系中的每種語言建立完美的索引。 極特殊的情況可能存在，此時最複雜的斷詞工具也無法正確地處理以另一種語言所撰寫的文字。  
  

  
### <a name="non-western-languages"></a>非西方語言  
 對於非西方語言 (例如，中文、日文、印度文等) 而言，基於語言的原因，上述解決方法不一定有用。 若為非西方語言，請考慮採用下列其中一個解決方法：  
  
-   不同語系的語言  
  
     如果資料行可能包含完全不同的語言 (例如，西班牙文和日文)，請考慮將不同語言的內容儲存在個別的資料行中。 這樣做可讓您針對每個資料行使用語言特有的斷詞工具。 如果您選擇這種解決方案，但是不知道查詢時所使用的查詢語言，可能就必須針對這兩個資料行發出查詢，以便確保查詢會尋找正確的資料列或文件。  
  
-   二進位內容 (例如 Microsoft Word 文件)  
  
     當索引的內容是 `binary` 類型時，將文字內容傳送至斷詞工具之前先進行處理的全文檢索搜尋篩選可能會接受存在二進位檔案中的特定語言標記。 在此情況下，篩選會在建立索引時，針對文件或文件的區段發出正確的 LCID。 然後，全文檢索引擎會針對具有該 LCID 的語言呼叫斷詞工具。 不過，建立多語言內容的索引之後，我們建議您確認是否已正確建立內容的索引。  
  
-   純文字內容  
  
     當您的內容是純文字時，您可以將它轉換成 `xml` 資料類型，並加入語言標記，以便表示對應至每份特定文件或文件區段的語言。 不過，若要讓此解決方法有用，您必須在建立全文檢索索引之前，了解所使用的語言。  
  

  
##  <a name="stemming"></a><a name="stemming"></a> 詞幹分析  
 選擇資料行層級語言時的其他考量是詞幹分析。 在全文檢索查詢中，「詞幹分析」  是指搜尋某特定語言之所有字根 (字形變化) 的過程。 當您使用一般斷詞工具來處理許多語言時，詞幹分析程序只會針對指定給資料行的語言運作，而不會針對資料行中的其他語言運作。 例如，德文字幹分析器不會針對英文或西班牙文 (等語言) 運作。 這可能會影響重新叫用，端視您在查詢時選擇的語言而定。  
  

  
##  <a name="effect-of-column-type-on-full-text-search"></a><a name="type"></a> 資料行類型對全文檢索搜尋的影響  
 選擇語言時的另一個考量與呈現資料的方式有關。 對於儲存在 `varbinary(max)` 資料行以外的資料而言，系統不會執行特殊篩選。 相反地，文字可以其原始格式傳送，而不會受限於文字分隔元件。  
  
 此外，斷詞工具主要設計成處理一般撰寫內容。 所以，如果您的文字上有任何類型的標記 (如 HTML)，則在編製索引和搜尋語言時可能會不夠精確。 在此情況下，您有兩個選擇：慣用的方法是將文字資料儲存在`varbinary(max)`資料行中，並指示其檔案類型，以便進行篩選。 如果不使用這個選項，您可以考慮使用中性斷詞工具，而且若可行的話，請將標記資料 (例如 HTML 中的 'br') 加入至非搜尋字清單。  
  
> [!NOTE]  
>  當您指定中性語言時，以語言為基礎的字根檢索功能將不會發生作用。  
  

  
##  <a name="specifying-a-non-default-column-level-language-in-a-full-text-query"></a><a name="nondef"></a> 在全文檢索查詢中指定非預設資料行層級語言  
 依預設，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，全文檢索搜尋會使用指定給包含在全文檢索子句中之每個資料行的語言來剖析查詢字詞。 若要覆寫此行為，請在查詢時指定非預設語言。 若為已安裝資源的支援語言，您就可以使用 *CONTAINS* 、 [CONTAINSTABLE](/sql/t-sql/queries/contains-transact-sql)、 [FREETEXT](/sql/relational-databases/system-functions/containstable-transact-sql)或 [FREETEXTTABLE](/sql/t-sql/queries/freetext-transact-sql)查詢的 LANGUAGE [language_term](/sql/relational-databases/system-functions/freetexttable-transact-sql) 子句來指定用於查詢字詞之斷詞、詞幹分析、同義字和停用字詞處理的語言。  
  

  
## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
