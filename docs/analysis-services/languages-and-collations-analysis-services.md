---
title: "語言和定序 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
keywords: "測試 Analysis Services"
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3992b6ea5ff2dedbb18571919041407a8545fd4a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="languages-and-collations-analysis-services"></a>語言和定序 (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 作業系統所提供的語言和定序。 **Language** 和 **Collation** 屬性會在安裝期間於執行個體層級進行初始設定，但之後可在物件階層的不同層級進行變更。  
  
 在多維度模型中 (僅限多維度模型)，您可以在資料庫或 Cube 上設定這些屬性，您也可以在為 Cube 中物件所建立的翻譯上設定這些屬性。 在表格式模型中，語言和定序會繼承自主機作業系統。  
  
 在多維度模型中設定 **Language** 和 **Collation** 時，您可以指定資料模型在處理和查詢執行期間所使用的設定，或者提供多種翻譯給模型，讓外語人士可以母語使用模型。 在針對不同地區設定對開發環境和生產伺服器進行設定的情況下，需要在物件 (資料庫、模型或 Cube) 上明確設定 **Language** 和 **Collation** 屬性，您也需要確定語言和定序符合預定目標環境的語言和定序。  
  
##  <a name="bkmk_object"></a> 支援語言和定序屬性的物件  
 **Language** 和 **Collation** 屬性通常會一起公開 (設定 **Language**的位置也可以設定 **Collation**)。  
  
 您可以在下列物件上設定 **Language** 和 **Collation** ：  
  
-   **執行個體**： 部署至執行個體的所有專案會採用執行個體的語言和定序 (假設未定義語言和定序)。 多維度模型預設會將語言和定序保留空白。 部署專案之後，產生的資料庫和 Cube 會取得執行個體的語言和定序。  
  
     語言和定序屬性一開始會在安裝期間建立，但系統管理員可在 Management Studio 中覆寫這些屬性。 如需詳細資訊，請參閱＜ [變更執行個體上的預設語言或定序](#bkmk_defaultLang) ＞。  
  
-   **資料庫**： 若要中斷繼承，您可以在專案層級明確設定資料庫內含之所有 Cube 使用的語言和定序。 除非您另外指定，否則資料庫中的所有 Cube 會取得您在這個層級所指定的語言和定序。 如果您經常撰寫程式碼並部署至不同的地區設定 (例如，在中文版電腦上開發方案，但部署至法國子公司所擁有的伺服器)，在資料庫層級設定語言和定序是確保方案在目標環境中有效的首要步驟。 設定這些屬性的最佳位置是在專案內 (透過專案上的 [編輯資料庫]  命令)。  
  
-   **資料庫維度**： 雖然設計工具會在資料庫維度上公開 **Language** 和 **Collation** 屬性，但在這個物件上設定屬性並沒有幫助。 資料庫維度不會做為獨立物件使用，因此可能很難或不可能利用您定義的屬性。 在 Cube 中，維度一律會從其 Cube 父系繼承 **Language** 和 **Collation** ， 並忽略您之前在獨立資料庫維度物件上設定的所有值。  
  
-   **Cube**： 至於主要查詢結構，您可以在 Cube 層級設定語言和定序。 例如，您可能想要在同一個專案中建立多種語言版本的 Cube (例如英文版和中文版)，其中每個 Cube 會有自己的語言和定序。  
  
     不論您在 Cube 上設定的語言和定序為何，都可供 Cube 中含有的所有量值和維度使用。 只有在維度屬性上建立翻譯時，才能進一步設定定序屬性。 否則會假設屬性層級沒有翻譯，而且每個 Cube 有一個定序。  
  
 此外，您可以在 **翻譯**物件上只設定 **Language** 。  
  
 您將翻譯加入 Cube 或維度時，會建立翻譯物件。 **Language** 是翻譯定義的一部分。 相反地，**Collation**會在 Cube 或更高層級設定，並供所有翻譯共用。 這在含有翻譯之 Cube 的 XMLA 中會很明顯，其中您會看到多個語言屬性 (每個翻譯一個屬性)，但只會看到一個定序。 請注意，維度屬性翻譯是例外；在這種情況下，您可以覆寫 Cube 定序，來指定符合來源資料行的屬性定序 (資料庫引擎支援在個別資料行上設定定序，並且通常可設定個別翻譯，從不同的來源資料行取得成員資料)。 否則，對於其他所有翻譯而言，會使用 **Language** 本身，而不會使用 **Collation** 。 如需詳細資訊，請參閱 [Analysis Services 中的翻譯支援](../analysis-services/translation-support-in-analysis-services.md) 。  
  
##  <a name="bkmk_lang"></a> Analysis Services 中的語言支援  
 **Language** 屬性會設定物件的地區設定，可用於處理和查詢期間，以及搭配 **Captions** 和 **Translations** 支援多語系案例。 地區設定是以語言識別碼 (例如英文) 和領域 (例如美國或澳洲) 為基礎，並進一步精簡日期和時間表示法。  
  
 在執行個體層級，屬性會在安裝期間根據 Windows Server 作業系統的語言來設定 (37 種語言之一並假設已安裝語言套件)。 您無法變更安裝程式的語言。  
  
 安裝後，您可以使用 Management Studio 中的 [伺服器屬性] 頁面，或在 msmdsrv.ini 組態檔中覆寫 **Language** 。 您可以選擇更多語言，包括 Windows 用戶端支援的所有語言。 在執行個體層級設定時，伺服器上的 **Language** 會決定後續部署之所有資料庫的地區設定。 例如，如果您將 **Language** 設為德文，部署至執行個體的所有資料庫都會有語言屬性 1031，也就是德文的 LCID。  
  
###  <a name="bkmk_lcid"></a> 語言屬性的值是地區設定識別碼 (LCID)  
 有效值包括出現在下拉式清單中的任何 LCID。 在 Management Studio 和 SQL Server Data Tools 中，LCID 會以對等字串來表示。 不論工具為何，只要公開 **Language** 屬性的位置都會顯示相同的語言。 具有相同的語言清單可確保您可以在整個模型中一致地實作及測試翻譯。  
  
 雖然 Analysis Services 會依名稱列出語言，但是針對屬性儲存的實際值會是 LCID。 以程式設計方式或透過 msmdsrv.ini 檔案設定語言屬性時，請使用 [地區設定識別碼 (LCID)](http://en.wikipedia.org/wiki/Locale) 作為值。 LCID 是由語言識別碼、排序識別碼和保留的位元 (用於識別特定語言) 所組成的 32 位元值。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用 LCID 為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體和物件指定選定語言。  
  
 您可以使用十六進位或十進位格式設定 LCID。 [語言]  屬性的一些有效值範例包括：  
  
-   0x0409 或 1033，代表 [英文 (美國)]   
  
-   0x0411 或 1041，代表 [日文]   
  
-   0x0407 或 1031，代表 [德文 (德國)]   
  
-   0x0416 或 1046，代表 [葡萄牙文 (巴西)] 。  
  
 若要檢視較長的清單，請參閱 [Microsoft 指派的地區設定識別碼](http://msdn.microsoft.com/goglobal/bb964664.aspx)。 如需更多背景，請參閱 [編碼方式和字碼頁](http://msdn.microsoft.com/goglobal/bb688114.aspx)。  
  
> [!NOTE]  
>  **Language** 屬性不會決定用於傳回系統訊息的語言，也不會決定要在使用者介面中顯示的字串。 錯誤、警告和訊息會當地語系化成 Office 和 Office 365 中支援的所有語言，並且會在用戶端連接指定其中一個支援的地區設定時自動使用。  
  
##  <a name="bkmk_collations"></a> Analysis Services 中的定序支援  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 只會使用 Windows (版本 _90 和 _100) 和二進位定序。 而不會使用舊版 SQL Server 定序。 在 Cube 中，會完全使用單一定序，但不包括屬性層級的翻譯。 如需定義屬性翻譯的詳細資訊，請參閱 [Analysis Services 中的翻譯支援](../analysis-services/translation-support-in-analysis-services.md)。  
  
 定序可控制複合字集中所有字串的區分大小寫，但不包括物件識別碼。 請注意，如果您在物件識別碼中使用大寫和小寫字元，物件識別碼的區分大小寫不是取決於定序，而是取決於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 以英文字撰寫物件識別碼時，不論定序為何，物件識別碼一律不會區分大小寫。 斯拉夫文和其他複合語言則相反 (一律區分大小寫)。 如需詳細資訊，請參閱＜ [全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) ＞。  
  
 Analysis Services 的定序與 SQL Server 關聯式資料庫引擎的定序相容 (假設您為每項服務選取的排序選項保持同位)。 例如，如果關聯式資料庫區分腔調字，您應該以相同方式來設定 Cube。 當定序設定有所分歧時，可能會發生問題。 如需範例和解決方法，請參閱 [Unicode 字串中的空格根據定序而有不同的處理結果](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)。 若要深入了解定序和資料庫引擎，請參閱 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
###  <a name="bkmk_collationtype"></a> 定序類型  
 Analysis Services 支援兩種定序類型：  
  
-   **Windows 定序 (版本 _90 和 _100)**  
  
     Windows 定序版本為 _90 (未標記的較舊版本) 和較新的 _100 版。 只有 _100 版會在定序名稱中顯示版本號碼︰  
  
    -   latin1_general  
  
    -   latin1_general_100  
  
     Windows 定序會根據語言的語言和文化特性來排序字元。 在 Windows 中，由於許多語言共用常見的字母和規則來排序和比較字元，因此定序數目會多於搭配使用的地區設定 (或語言) 數目。 例如，有 33 個 Windows 地區設定 (包括所有葡萄牙文和英文 Windows 地區設定) 使用 Latin1 字碼頁 (1252)，並遵循一組共同規則來排序和比較字元。  
  
    > [!NOTE]  
    >  當您決定定序時，應該使用基礎資料庫所使用的相同定序。 不過，如果您可以選擇，_100 版是較新版本並提供在語言上更精確的文化排序慣例。  
  
-   **二進位定序 (BIN 或 BIN2)**  
  
     二進位定序會根據 Unicode 字碼指標 (而非語言值) 排序。 例如，Latin1_General_BIN 和 Japanese_BIN 若使用於 Unicode 資料，會產生相同排序結果。 語言排序可能會產生類似 aAbBcCdD 的結果，而二進位排序則是 ABCDabcd，因為所有大寫字元的字碼指標總計會高於小寫字元的字碼指標。  
  
###  <a name="bkmk_sortorder"></a> 排序順序選項  
 排序選項可根據區分大小寫、腔調字、假名和全半形，來精簡排序和比較規則。 例如， **之** Collation [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 組態屬性的預設值是 Latin1_General_AS_CS，它指定使用 Latin1_General 定序，以及區分腔調字、區分大小寫的排序順序。  
  
 請注意，BIN 和 BIN2 與其他排序選項互斥，如果您想要使用 BIN 或 BIN2，請清除 [區分腔調字] 的排序選項。 同樣地，選取 BIN2 時，則無法使用區分大小寫、不區分大小寫、區分腔調字、不區分腔調字、區分假名和區分全半形等選項。  
  
 下表描述 Windows 定序排序順序選項和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]之相關聯的後置詞。  
  
|排序順序 (後置詞)|排序順序描述|  
|---------------------------|----------------------------|  
|二進位 (_BIN) 或 BIN2 (_BIN2)|SQL Server 中有兩種二進位定序：較舊的 BIN 定序和較新的 BIN2 定序。 在 BIN2 定序中，所有字元都是根據其字碼指標排序。 在 BIN 定序中，只有第一個字元是根據字碼指標排序，剩餘字元則是根據其位元組值排序。 (因為 Intel 平台是 Little Endian 架構，所以 Unicode 字碼字元一律以位元組交換的方式儲存)。<br /><br /> 如果是 Unicode 資料類型的二進位定序，在資料排序時不會考量地區設定。 例如，Latin_1_General_BIN 和 Japanese_BIN 用於 Unicode 資料時會產生相同的排序結果。<br /><br /> 二進位排序順序為區分大小寫和區分腔調字。 二進位也是最快的排序順序。|  
|區分大小寫 (_CS)|區分大寫和小寫字母。 如果選取此選項，小寫字母會排序在大寫字母的前面。 指定 _CI，就可以明確地設定不區分大小寫。 特定定序的大小寫設定不會套用至物件識別碼，例如維度、Cube 和其他物件的識別碼。 如需詳細資訊，請參閱＜ [全球化秘訣和最佳作法 &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) ＞。|  
|區分腔調字 (_AS)|區分有腔調和無腔調的字元。 例如，'a' 不等於 'ấ'。 如果未選取此選項，在排序用途上， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將有腔調和無腔調字母視為相同。 指定 _AI，就可以明確地設定不區分腔調字。|  
|區分假名 (_KS)|區分兩種類型的日文假名字元：平假名與片假名。 如果未選取此選項，在排序用途上， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 視平假名和片假名相同。 不區分假名的排序沒有排序順序後置詞。|  
|區分全半形 (_WS)|區分單一位元組字元和以雙位元組字元表示的相同字元。 如果未選取此選項，在排序用途上， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 視相同字元的單一位元組和雙位元組表示法相同。 不區分全半形的排序沒有排序順序後置詞。|  
  
##  <a name="bkmk_defaultLang"></a> 變更執行個體上的預設語言或定序  
 預設語言和定序是在安裝期間建立，但是您可以當做安裝後組態的一部分來變更。 在執行個體層級變更定序不容易，並且具有下列需求：  
  
-   服務會重新啟動。  
  
-   更新現有物件的定序設定。 建立物件之後，會繼承一次定序設定。 必須手動完成定序的後續變更。 如需詳細資訊，請參閱＜ [使用 XMLA 變更資料模型中的語言和定序](#bkmk_XMLA) 。  
  
-   更新定序之後，請重新處理資料分割和維度。  
  
 您可以在伺服器層級，使用 SQL Server Management Studio 或 AMO PowerShell 來變更預設語言或定序。 或者，您可以修改**\<語言 >**和 **\<CollationName >**在 msmdsrv.ini 檔案中，設定指定之語言的 LCID。  
  
1.  在 Management Studio 中，在伺服器名稱上按一下滑鼠右鍵 | [屬性] | [語言/定序]。  
  
2.  選擇排序選項。 若要選取 [二進位]  或 [二進位 2] ，請先清除 [區分腔調字] 的核取方塊。  
  
     請注意，定序和語言是完全無關的設定。 如果您變更其中一項，並不會篩選另一項的值以顯示常見組合。  
  
3.  更新資料模型，以使用新的定序 (請參閱下一節)。  
  
4.  重新啟動服務。  
  
##  <a name="bkmk_cube"></a> 變更 Cube 上的語言或定序  
  
1.  在 [方案總管] 中，按兩下 Cube，開啟 Cube 設計師。  
  
2.  在 [量值] 或 [維度] 窗格中，選取最上層節點。 任何一個窗格的最上層物件是 Cube。  
  
3.  在 [屬性] 中，設定 **Language** 和 **Collation**。 所有 Cube 物件 (包括 Cube 維度和量值) 會使用您選擇的值，並會影響處理和查詢作業。  
  
     在 Cube 中的物件上內嵌替代語言和定序屬性的唯一方法是透過翻譯。 如需詳細資訊，請參閱 [Analysis Services 中的翻譯支援](../analysis-services/translation-support-in-analysis-services.md) 。  
  
##  <a name="bkmk_XMLA"></a> 使用 XMLA 變更資料模型中的語言和定序  
 建立物件之後，會繼承一次語言和定序設定。 必須手動完成這些屬性的後續變更。 快速變更多個物件上之定序的其中一個方法，是在 XMLA 指令碼上使用 ALTER 命令。  
  
 根據預設，定序會在資料庫層級設定一次。 物件階層的其餘部分都會隱含這個繼承。 如果您在 Cube 中的物件上明確設定 **Collation** (個別維度屬性上允許使用)，這個屬性會出現在 XMLA 定義中。 否則只有最上層定序屬性。  
  
 使用 XMLA 修改現有的資料庫之前，請確定您沒有引入資料庫與用來建立資料庫的原始程式檔之間的差異。 例如，您可能想要使用 XMLA 來快速變更概念驗證測試的語言或定序，然後追蹤原始程式檔的變更 (請參閱 [變更 Cube 上的語言或定序](#bkmk_cube))，並使用已存在的作業程序來重新部署方案。  
  
1.  在 Management Studio 中，在資料庫上按一下滑鼠右鍵 | [編寫資料庫的指令碼為] | [ALTER 至] | [新增查詢編輯器視窗]。  
  
2.  搜尋現有的語言或定序，並以替代值取代。  
  
3.  按 F5 執行指令碼。  
  
4.  重新處理 Cube。  
  
##  <a name="bkmk_enablefast1033"></a> 透過 EnableFast1033Locale 提高英文地區設定的效能  
 如果您使用 [英文 (美國)] 語言識別碼 (0x0409 或 1033) 作為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的預設語言，則可以設定 **EnableFast1033Locale** 組態屬性來獲得更多效能的好處，這是只有該語言識別碼才可以使用的進階組態屬性。 將此屬性的值設定為 **true** ，就可以讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用更快的演算法來進行字串雜湊和比較。 如需設定組態屬性的詳細資訊，請參閱 [Analysis Services 的伺服器屬性](../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
##  <a name="bkmk_gb18030"></a> Analysis Services 中的 GB18030 支援  
 GB18030 是一種獨立標準，可供中華人民共和國進行中文字元的編碼。 在 GB18030 中，字元的長度可以是 1、2 或 4 個位元組。 在 Analysis Services 中，處理外部來源的資料時沒有任何資料轉換。 資料會以 Unicode 的簡單格式儲存。 在查詢時，當查詢結果中傳回文字資料時，系統會根據用戶端作業系統設定，透過 Analysis Services 用戶端程式庫 (也就是 MSOLAP.dll OLE DB 提供者) 來執行 GB18030 轉換。 資料庫引擎也支援 GB18030。 如需詳細資訊，請參閱＜ [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)＞。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 的全球化案例](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [全球化秘訣和最佳作法 &#40;Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)   
 [定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
