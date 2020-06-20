---
title: 詞彙擷取轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextractiontrans.f1
helpviewer_keywords:
- word boundaries [Integration Services]
- extracting data [Integration Services]
- sentence boundaries
- word extractions [Integration Services]
- Term Extraction transformation
- tagging words
- normalized data [Integration Services]
- tokenizing text [Integration Services]
- parts of speech [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- stemming words [Integration Services]
ms.assetid: d0821526-1603-4ea6-8322-2d901568fbeb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1655b50f84fae99249b2170d92a49459a143d5b4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939263"
---
# <a name="term-extraction-transformation"></a>詞彙擷取轉換
  「詞彙擷取」轉換會從轉換輸入資料行的文字中擷取詞彙，然後將這些詞彙寫入轉換輸出資料行。 轉換只適用於英文字，它使用自己的英文字典和有關英文的語言資訊。  
  
 您可以使用「詞彙擷取」轉換來探索資料集的內容。 例如，包含電子郵件訊息的文字可能會提供有關產品的有用意見反應，這樣您可以使用「詞彙擷取」轉換來擷取訊息中討論的主題，做為分析意見反應的方法。  
  
## <a name="extracted-terms-and-data-types"></a>擷取的詞彙和資料類型  
 「詞彙擷取」轉換可以僅擷取名詞、僅擷取名詞片語，或同時擷取名詞和名詞片語。 名詞為單個名詞；名詞片語則至少為兩個單字，其中一個為名詞，另一個為名詞或形容詞。 例如，如果轉換使用「單獨名詞」選項，則它會擷取類似 *bicycle* 和 *landscape*的詞彙；如果轉換使用名詞片語選項，則它會擷取類似 *new blue bicycle*、 *bicycle helmet*和 *boxed bicycles*的詞彙。  
  
 轉換不會擷取冠詞和代名詞。 例如，「詞彙擷取」轉換會從文字 *the bicycle* 、 *my bicycle*，及 *that bicycle*中擷取詞彙 *bicycle*。  
  
 「詞彙擷取」轉換會為其擷取的每個詞彙產生一個分數。 此分數可以是 TFIDF 值或原始頻率，表示正規化詞彙在輸入中出現的次數。 在任何一種情況下，分數都會由大於 0 的實數來表示。 例如，TFIDF 分數可能是值 0.5，而頻率則可能是類似 1.0 或 2.0 的值。  
  
 「詞彙擷取」轉換的輸出僅包含兩個資料行。 一個資料行包含擷取的詞彙，另一資料行則包含分數。 資料行的預設名稱是**Term**和 `Score` 。 因為輸入中的文字資料行可能包含多個詞彙，所以「詞彙擷取」轉換的輸出一般比輸入擁有更多的資料列。  
  
 如果將擷取的詞彙寫入資料表，則它們可以被其他查閱轉換 (例如「詞彙查閱」、「模糊查閱」和「查閱」轉換) 使用。  
  
 「詞彙擷取」轉換僅能使用資料類型為 DT_WSTR 或 DT_NTEXT 之資料行中的文字。 如果資料行包含文字，但不具有這些資料類型的其中之一，則可以使用「資料轉換」將資料類型為 DT_WSTR 或 DT_NTEXT 的資料行加入資料流程，並將資料行值複製到新資料行。 然後，「資料轉換」的輸出可以用作「詞彙擷取」轉換的輸入。 如需詳細資訊，請參閱 [Data Conversion Transformation](data-conversion-transformation.md)。  
  
## <a name="exclusion-terms"></a>排除詞彙  
 (選擇性)「詞彙擷取」轉換可以參考包含排除詞彙 (是指當轉換從資料集中擷取詞彙時應略過的詞彙) 之資料表中的資料行。 如果一組詞彙在特殊商務和產業中視為不合理 (通常因為該詞彙出現的頻率太高，而成為一個非搜尋字)，則這個功能會非常有用。 例如，當從包含有關特殊品牌汽車的客戶支援資訊之資料集中擷取詞彙時，該品牌名稱自身可能會被排除，因為它被提及的頻率太高，而失去意義。 因此，排除清單中的值必須自訂到您要使用的資料集。  
  
 當您將詞彙新增至排除清單時，包含該詞彙的所有詞彙 (單字或名詞片語) 也會被排除。 例如，如果排除清單包含單一字 *data*，則包含這個字的所有詞彙 (例如 *data*、 *data mining*、 *data integrity*和 *data validation* ) 也會被排除。 如果您只想排除包含 *data*單字的複合字，則必須明確將這些複合詞彙加入至排除清單。 例如，如果您要擷取含 *data*的個體，但要排除 *data validation*，則將 *data validation* 加入至排除清單，並確定 *data* 已從排除清單中移除。  
  
 參考資料表必須是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 Access 資料庫中的資料表。 「詞彙擷取」轉換會使用個別 OLE DB 連接，以連接到參考資料表。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md)。  
  
 「詞彙擷取」轉換以完全預先快取模式運作。 在執行階段，「詞彙擷取」轉換在處理任何轉換輸入資料列之前，會從參考資料表讀取排除詞彙，並將其儲存於其私用記憶體中。  
  
## <a name="extraction-of-terms-from-text"></a>從文字中擷取詞彙  
 若要從文字中擷取詞彙，「詞彙擷取」轉換則需執行下列工作。  
  
### <a name="identification-of-words"></a>單字的識別  
 首先，「詞彙擷取」轉換透過執行下列工作來識別單字：  
  
-   使用空格、分行符號和英文中的其他單字結束字元將文字分隔成單字。 例如，類似 *?* 和 *:* 等標點符號是斷字字元。  
  
-   保留由連字號或底線符號連接的單字。 例如，單字 *copy-protected* 和 *read-only* 保留為一個單字。  
  
-   保留包含句號的完整縮寫字。 例如， *A.B.C* Company 會 Token 化為 **ABC** 和 **Company**。  
  
-   分割特殊字元的單字。 例如，單字 *date/time* 會擷取為 *date* 和 *time*， *(bicycle)* 會擷取為 *bicycle*，而 C# 則會處理為 C。特殊字元會被捨棄，不能詞彙化。  
  
-   辨識特殊字元 (例如撇號) 不應分割單字的情況。 例如，單字 *bicycle's* 不會分割為兩個單字，而會產生單一詞彙 *bicycle* (名詞)。  
  
-   分割時間運算式、貨幣運算式、電子郵件地址和郵遞地址。 例如，日期 *January 31, 2004* 會分割為三個 Token， *January*、 *31*和 *2004*。  
  
### <a name="tagged-words"></a>標記的單字  
 第二，「詞彙擷取」轉換會將單字標記為下列其中一種詞類：  
  
-   單數形式的名詞。 例如， *bicycle* 和 *potato*。  
  
-   複數形式的名詞。 例如， *bicycles* 和 *potatoes*。 所有未還原的複數名詞都會進行詞幹分析。  
  
-   單數形式的專有名詞。 例如， *April* 和 *Peter*。  
  
-   複數形式的專有名詞。 例如， *April* 和 *Peters*。 要進行詞幹分析的專有名詞必須是內部詞素的一部分 (限於標準英文單字)。  
  
-   形容詞。 例如， *blue*。  
  
-   比較兩項事物的比較級形容詞。 例如， *higher* 和 *taller*。  
  
-   識別一項事物具有高於或低於其他至少兩項事物之品質的最高級形容詞。 例如， *highest* 和 *tallest*。  
  
-   數字。 例如， *62* 和 *2004*。  
  
 不屬於這些詞性的單字會被捨棄。 例如，動詞和代名詞會被捨棄。  
  
> [!NOTE]  
>  部分詞類的標記以統計模型為基礎，標記可能不完全精確。  
  
 如果「詞彙擷取」轉換設定為僅擷取名詞，則僅會擷取標記為單數或複數形式之名詞和專有名詞的單字。  
  
 如果「詞彙擷取」轉換設定為僅擷取名詞片語，則標記為名詞、專有名詞、形容和數字的單字可以組合成名詞片語，但片語必須包含至少一個標記為單數或複數形式之名詞和專有名詞的單字。 例如，名詞片語 *highest mountain* 由標記為最高級形容詞的單字 (*highest*) 和標記為名詞的單字 (*mountain*) 組成。  
  
 如果「詞彙擷取」設定為擷取名詞和名詞片語，則會套用名詞規則和名詞片語規則。 例如，轉換會從文字 *many beautiful blue bicycles* 中擷取 *bicycle* 和 *beautiful blue bicycle*。  
  
> [!NOTE]  
>  擷取的詞彙依然受限於轉換使用的最大詞彙長度和頻率臨界值。  
  
### <a name="stemmed-words"></a>詞幹分析的單字  
 「詞彙擷取」轉換也會分析名詞的詞幹，僅擷取名詞的單數形式。 例如，轉換從 *men* 擷取 *man*，從 *mice* 擷取 *mouse*，從 *bicycles* 擷取 *bicycle*。 轉換會使用其字典來分析名詞的詞幹。 如果動名詞存在於字典中，則它們將做為名詞進行處理。  
  
 「詞彙擷取」轉換會透過使用「詞彙擷取」轉換內部的字典，對單字進行詞幹分析 (如以下範例所示)，使之成為在其字典中的形式。  
  
-   移除名詞中的 *s* 。 例如， *bicycles* 會成為 *bicycle*。  
  
-   移除名詞中的 *es* 。 例如， *stories* 會成為 *story*。  
  
-   從字典中擷取不規則名詞的單數形式。 例如， *geese* 會成為 *goose*。  
  
### <a name="normalized-words"></a>正規化單字  
 「詞彙擷取」轉換會正規化僅由於在句子中的位置而大寫的詞彙，改用它們的小寫形式。 例如，在片語 *Dogs chase cats* 和 *Mountain paths are steep*中， *Dogs* 和 *Mountain* 將會標準化為 *dog* 和 *mountain*。  
  
 「詞彙擷取」轉換會正規化單字，這樣單字的大寫版本和小寫版本就不會視作不同的詞彙進行處理。 例如，在文字 *You see many bicycles in Seattle* 和 *Bicycles are blue*中， *bicycles* 和 *Bicycles* 被視為相同的詞彙，轉換僅會保留 *bicycle*。 沒有列在內部字典中的專有名詞和單字不會被正規化。  
  
### <a name="case-sensitive-normalization"></a>區分大小寫正規化  
 「詞彙擷取」轉換可以設定為將小寫和大寫單字視為不同的詞彙，或做為同一個詞彙的不同變數。  
  
-   如果設定轉換辨識大小寫的不同，則類似 *Method* 和 *method* 的詞彙將作為兩個不同的詞彙進行擷取。 並非句子中第一個單字的大寫單詞絕不會正規化，而是標記為專有名詞。  
  
-   如果設定轉換不區分大小寫，則類似 *Method* 和 *method* 的詞彙將視為一個詞彙的兩個不同變數。 擷取的詞彙之清單可能包含 *Method* 或 *method*，視哪個單字第一個出現在輸入資料集中而定。 如果 *Method* 僅因為是句子中的第一個單字而大寫，則它將會以正規化的形式擷取。  
  
## <a name="sentence-and-word-boundaries"></a>句子和單字的界限  
 「詞彙擷取」轉換使用下列字元作為句子界限，將文字分隔為句子：  
  
-   ASCII 分行符號字元 0x0d (歸位字元) 和 0x0a (換行字元)。 若要使用此字元作為句子界限，則資料列中必須有兩個或兩個以上的分行符號字元。  
  
-   連字號 (-)。 若要使用此字元作為句子界限，則連字號左邊或右邊字元都不能是字母。  
  
-   底線符號 (_)。 若要使用此字元作為句子界限，則連字號左邊或右邊字元都不能是字母。  
  
-   所有小於或等於 0x19 或者大於或等於 0x7b 的 Unicode 字元。  
  
-   數字、標點符號和字母字元的組合。 例如， *A23B#99* 會傳回詞彙 *A23B*。  
  
-   字元、%、@、&、$、#、 \* 、：、;、、 **、、** !,?, \<, > 、+、=、^、~、|、 \\ 、/、（、）、[、]、{、}、"和 '。  
  
    > [!NOTE]  
    >  包含一或多個句號 (.) 的縮寫字不會分隔為多個句子。  
  
 然後「詞彙擷取」轉換會使用下列單字界限，將句子分隔為單字：  
  
-   Space  
  
-   索引標籤  
  
-   ASCII 0x0d (歸位字元)  
  
-   ASCII 0x0a (換行字元)  
  
    > [!NOTE]  
    >  如果撇號在縮寫字的單字中，例如 *we're* 或 *it's*，則該單字會在撇號處斷開；否則，撇號後面的字母將被刪除。 例如， *we're* 會分割為 *we* 和 *'re*，而 *bicycle's* 則會刪減為 *bicycle*。  
  
## <a name="configuration-of-the-term-extraction-transformation"></a>詞彙擷取轉換的組態  
 「詞彙擷取」轉換會使用內部演算法和統計模型來產生結果。 您可能須執行「詞彙擷取」轉換多次，並檢查結果來設定轉換，以便產生對您的文字採礦解決方案有效的結果類型。  
  
 「詞彙擷取」轉換有一個規則輸入、一個輸出及一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [詞彙擷取轉換編輯器]**** 對話方塊中設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [詞彙擷取轉換編輯器 &#40;詞彙擷取索引標籤&#41;](../../term-extraction-transformation-editor-term-extraction-tab.md)  
  
-   [詞彙擷取轉換編輯器 &#40;排除索引標籤&#41;](../../term-extraction-transformation-editor-exclusion-tab.md)  
  
-   [詞彙擷取轉換編輯器 &#40;進階索引標籤&#41;](../../term-extraction-transformation-editor-advanced-tab.md)  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
