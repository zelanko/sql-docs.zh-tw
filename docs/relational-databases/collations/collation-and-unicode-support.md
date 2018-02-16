---
title: "定序與 Unicode 支援 | Microsoft 文件"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Active
ms.openlocfilehash: d1fd84b774ee2ea2a7af3db4f1cd015dfbd3176d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的定序會提供資料的排序規則、大小寫和區分腔調字屬性。 與字元資料類型 (例如 **char** 和 **varchar** ) 搭配使用的定序會指示字碼頁，以及可針對該資料類型表示的對應字元。 不論您是安裝新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體、還原資料庫備份，還是將伺服器連接至用戶端資料庫，都請務必了解您要使用之資料的地區設定需求、排序次序和區分大小寫與腔調字。 若要列出您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所提供的定序，請參閱 [sys。fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)。    
    
 當您針對伺服器、資料庫、資料行或運算式選取定序時，就是將某些特性指派給資料，而這些特性會影響資料庫中許多作業的結果。 例如，當您使用 ORDER BY 來建構查詢時，結果集的排序次序可能會相依於套用至資料庫的定序或在查詢運算式層級指定於 COLLATE 子句中的定序。    
    
 為了有效運用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的定序支援，您必須了解本主題中定義的詞彙，以及它們與資料特性的關聯。    
    
##  <a name="Terms"></a> 定序詞彙    
    
-   [定序](#Collation_Defn)    
    
-   [地區設定](#Locale_Defn)    
    
-   [字碼頁](#Code_Page_Defn)    
    
-   [排序次序](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> 定序    
 定序指定位元模式，代表資料集的每一個字元。 定序也可以決定排序和比較資料的規則。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援在單一資料庫中儲存具備不同定序的物件。 對於非 Unicode 資料行，定序設定則指定資料的字碼頁以及可代表的字元。 在非 Unicode 資料行之間移動的資料必須從來源字碼頁轉換成目的地字碼頁。    
    
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在各有不同定序設定的不同資料庫內容中執行時，陳述式的結果可能不同。 如果可能的話，請針對組織使用標準化定序。 這樣您就不需要在每一個字元或 Unicode 運算式中明確指定定序。 如果您必須使用有不同定序和字碼頁設定的物件，則在編寫查詢程式碼時，必須考量定序優先順序的規則。 如需詳細資訊，請參閱 [定序優先順序 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)。    
    
 與定序相關聯的選項是區分大小寫、區分腔調字、區分假名、區分全半形和區分變化選取器 (Variation Selector)。 這些選項的指定方式是將它們附加至定序名稱。 例如，此定序 `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` 區分大小寫、區分腔調字、區分假名和區分全半形。 例如，此定序 `Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS` 不區分大小寫、不區分腔調字、區分假名、區分全半形和區分變化選取器。  下表描述與這些不同選項相關聯的行為。    
    
|選項|描述|    
|------------|-----------------|    
|區分大小寫 (_CS)|區分大寫和小寫字母。 如果選取此選項，小寫字母會排序在大寫字母的前面。 如果未選取此選項，定序就不會區分大小寫。 也就是說，在排序用途上，SQL Server 會將大寫和小寫字母視為相同。 指定 _CI，就可以明確地選取不區分大小寫。|    
|區分腔調字 (_AS)|區分有腔調和無腔調的字元。 例如，'a' 不等於 'ấ'。 如果未選取此選項，定序就不會區分腔調。 也就是說，在排序用途上，SQL Server 會將有腔調和無腔調字母視為相同。 指定 _AI，就可以明確地選取不區分腔調字。|    
|區分假名 (_KS)|區分兩種類型的日文假名字元：平假名和片假名。 如果未選取此選項，定序就不會區分假名。 也就是說，在排序用途上，SQL Server 會將平假名和片假名視為相同。 省略此選項，是指定不區分假名的唯一方法。|    
|區分全半形 (_WS)|區分全形與半形字元。 如果未選取此選項，在排序用途上，SQL Server 會將相同字元的全形和半形表示法視為相同。 省略此選項，是指定不區分全形與半形的唯一方法。|    
|區分變化選取器 (_VSS) | [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]中首次引進如何區分日文定序 Japanese_Bushu_Kakusu_140 和 Japanese_XJIS_140 中的各種不同表意字元變化選取器。 變化序列是由基底字元加上額外的變化選取器所組成。 如果未選取此 _VSS 選項，則定序不區分變化選取器，而且比較時不會考慮變化選取器。 換句話說，SQL Server 基於排序目的，會將建置在相同基底字元但使用不同變化選取器的字元視為相同。 另請參閱  [Unicode Ideographic Variation Database](http://www.unicode.org/reports/tr37/)。 <br/><br/> 全文檢索搜尋索引不支援區分 Variation Selector (_VSS) 定序。 全文檢索搜尋索引支援只區分腔調字 (_AS)、區分假名 (_KS) 和區分全半形 (_WS) 選項。 SQL Server XML 和 CLR 引擎不支援 (_VSS) Variation Selector。
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援下列定序集：    
    
 Windows 定序    
 Windows 定序會定義規則，以便依據相關聯的 Windows 系統地區設定儲存字元資料。 如果是 Windows 定序，非 Unicode 資料的比較是使用與 Unicode 資料相同的演算法來實作。 基本 Windows 定序規則會指定套用字典排序時使用的字母或語言，以及用來儲存非 Unicode 字元資料的字碼頁。 Unicode 和非 Unicode 排序都與特定 Windows 版本中的字串比較相容。 如此可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的各種資料類型取得一致性，同時讓開發人員能夠使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相同的規則，在應用程式中排序字串。 如需詳細資訊，請參閱 [Windows 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)。    
    
 二進位定序    
 二進位定序依據地區設定和資料類型所定義的字碼值順序來排序資料。 它們會區分大小寫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的二進位定序會定義所使用的地區設定和 ANSI 字碼頁。 這會強制使用二進位排序次序。 因為它們相對而言較為簡單，所以二進位定序可提升應用程式效能。 如果是非 Unicode 資料類型，資料比較是依據 ANSI 字碼頁中所定義的字碼元素。 如果是 Unicode 資料類型，資料比較則是依據 Unicode 字碼指標。 如果是 Unicode 資料類型的二進位定序，在資料排序時不會考量地區設定。 例如，Latin_1_General_BIN 和 Japanese_BIN 用於 Unicode 資料時會產生相同的排序結果。    
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中有兩種二進位定序：較舊的 **BIN** 定序和較新的 **BIN2** 定序。 在 **BIN2** 定序中，所有字元都是根據其字碼指標排序。 在 **BIN** 定序中，只有第一個字元是根據字碼指標排序，剩餘字元則是根據其位元組值排序。 (因為 Intel 平台是 Little Endian 架構，所以 Unicode 字碼字元一律以位元組交換的方式儲存)。    
    
 SQL Server 定序    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序 (SQL_*) 會提供與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]舊版之間的排序次序相容性。 非 Unicode 資料的字典排序規則與 Windows 作業系統提供的任何排序常式不相容。 不過，Unicode 資料的排序與 Windows 排序規則的特定版本相容。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序對非 Unicode 和 Unicode 資料使用不同的比較規則，所以您會看到相同資料的比較有不同的結果，這取決於基礎資料類型而定。 如需詳細資訊，請參閱 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)。    
    
> [!NOTE]    
>  當您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的英文執行個體時，可基於與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 現有的執行個體相容而指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序 (SQL_*)。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序是在安裝期間定義，所以當下列條件成立時，請一定要小心指定定序設定：    
>     
>  -   應用程式的程式碼視先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序行為而定。    
> -   您必須儲存反映多國語言的字元資料。    
    
 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的下列層級設定定序：    
    
 伺服器層級定序    
 預設伺服器定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定，因此也會成為系統資料庫和所有使用者資料庫的預設定序。 請注意，您無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間選取僅限 Unicode 定序，因為系統不支援將它們當做伺服器層級定序。    
    
 將定序指派給伺服器之後，除非匯出所有資料庫物件和資料，並重建 **master** 資料庫，然後匯入所有資料庫物件和資料，否則無法變更此定序。 若不變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的預設定序，您可以在建立新資料庫或資料庫資料行時，指定想要的定序。    
    
 資料庫層級定序    
 建立或修改資料庫時，您可以使用 CREATE DATABASE 或 ALTER DATABASE 陳述式的 COLLATE 子句來指定預設資料庫定序。 如果未指定定序，則會將伺服器定序指派給資料庫。    
    
 除非變更伺服器的定序，否則無法變更系統資料庫的定序。    
    
 資料庫定序是用於資料庫中的所有中繼資料，而且是資料庫中使用之所有字串資料行、暫存物件、變數名稱和任何其他字串的預設值。 請注意，如果變更使用者資料庫的定序，則在資料庫中的查詢存取暫存資料表時，可能會發生定序衝突。 暫存資料表一律儲存在 **tempdb** 系統資料庫中，以使用執行個體的定序。 如果定序導致評估字元資料發生衝突，則比較使用者資料庫與 **tempdb** 間之字元資料的查詢可能會失敗。 您可以在查詢中指定 COLLATE 子句以解決此問題。 如需詳細資訊，請參閱 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)。    
    
 資料行層級定序    
 建立或改變資料表時，可以使用 COLLATE 子句來指定每個字元字串資料行的定序。 若未指定任何定序，就會將資料庫的預設定序指派給此資料行。    
    
 運算式層級定序    
 運算式層級定序是在執行陳述式時設定的，而且它們會影響傳回結果集的方式。 這樣可讓 ORDER BY 將結果排序成地區設定特定的結果。 使用類似下面的 COLLATE 子句來實作運算式層級定序：    
    
```    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> 地區設定    
 地區設定是一組與某個地點或文化特性相關聯的資訊。 這項資訊包括口語的名稱和識別碼、用來撰寫該語言的指令碼及文化習慣。 定序可與一個或多個地區設定產生關聯。 如需詳細資訊，請參閱 [Microsoft 指派的地區設定識別碼](http://msdn.microsoft.com/goglobal/bb964664.aspx)。    
    
###  <a name="Code_Page_Defn"></a> Code Page    
 字碼頁是給定的指令碼的已排序字元集，其中每一個字元與數字索引或字碼指標值相關聯。 Windows 字碼頁一般稱為 *「字元集」* (Character set) 或 *charset*。 字碼頁是用來提供不同 Windows 系統地區設定所使用的字元集和鍵盤配置的支援。     
###  <a name="Sort_Order_Defn"></a> Sort Order    
 排序次序會指定如何排序資料值。 這會影響資料比較的結果。 資料是使用定序來排序，而且可以使用索引來最佳化。    
    
##  <a name="Unicode_Defn"></a> Unicode 支援    
 Unicode 是將字碼指標對應到字元的標準用法。 由於 Unicode 主要設計為涵蓋世界上所有語言的字元，因此不需要使用不同的字碼頁來處理不同的字元集。 如果您儲存能夠反映多種語言的字元資料，一定要使用 Unicode 資料類型 (**nchar**、 **nvarchar**及 **ntext**) 而不要使用非 Unicode 資料類型 (**char**、 **varchar**及 **text**)。    
    
 重要限制會與非 Unicode 資料類型相關聯。 這是因為非 Unicode 電腦受限於使用單一字碼頁。 透過使用 Unicode，您可能會發現效能獲得明顯改善，因為所需要的字碼頁轉換減少。 您必須在資料庫、資料行或運算式層級個別選取 Unicode 定序，因為伺服器層級不支援這些定序。    
    
 用戶端所使用的字碼頁是由作業系統設定決定。 若要在 Windows XP 作業系統上設定用戶端字碼頁，請使用 [控制台] 中的 **[地區設定]** 。    
    
 當您將資料從伺服器移至用戶端時，舊版用戶端驅動程式可能無法辨識您的伺服器定序。 這種問題可能會發生在您將資料從 Unicode 伺服器移至非 Unicode 用戶端時。 此時，最佳選項可能就是升級用戶端作業系統，以便更新基礎系統定序。 如果用戶端已經安裝資料庫用戶端軟體，就可以考慮將服務更新套用至資料庫用戶端軟體。    
    
 此外，您也可以嘗試針對伺服器上的資料使用不同的定序。 您可以選擇將對應至用戶端字碼頁的定序。    
    
 若要使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中提供的 UTF-16 定序來改善部分 Unicode 字元的搜尋和排序 (僅限 Windows 定序)，您可以選取其中一個增補字元 characters (_SC) 定序或其中一個版本 140 定序。    
    
 若要評估與使用 Unicode 或非 Unicode 資料類型有關的議題，請測試自己的狀況，在您的環境中衡量效能差異。 建議您將組織內系統上使用的定序標準化，並盡量部署 Unicode 伺服器和用戶端。    
    
 在許多情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會與其他伺服器或用戶端互動，而且您的組織可能會在應用程式與伺服器執行個體之間使用多重資料存取標準。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端是兩種主要類型中的其中一種：    
    
-   **Unicode 用戶端** ，使用 OLE DB 和開放式資料庫連接 (ODBC) 3.7 版或更新版本。    
    
-   **非 Unicode 用戶端** ，使用 DB-Library 和 ODBC 3.6 版或更早版本。    
    
 下表將提供搭配 Unicode 和非 Unicode 伺服器的各種組合來使用多國語言資料的相關資訊。    
    
|[伺服器]|用戶端|好處或限制|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|因為 Unicode 資料會在整個系統中使用，所以這個狀況可提供最佳效能，並防止所擷取的資料遭到損毀。 這是 ActiveX Data Objects (ADO)、OLE DB 和 ODBC 3.7 版或更新版本的情況。|    
|Unicode|非 Unicode|在此狀況中，特別是執行新版作業系統的伺服器與執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或在舊版作業系統上執行的用戶端之間存在連接，當您將資料移至用戶端電腦時，可能會有一些限制或錯誤。 伺服器上的 Unicode 資料會嘗試對應至非 Unicode 用戶端上的對應字碼頁，以便轉換資料。|    
|非 Unicode|Unicode|這不是使用多國語言資料的理想組態。 您無法將 Unicode 資料寫入非 Unicode 伺服器。 當資料傳送到在此伺服器的字碼頁以外的伺服器時，就可能發生問題。|    
|非 Unicode|非 Unicode|這是多國語言資料的限制狀況。 您只能使用單一字碼頁。|    
    
##  <a name="Supplementary_Characters"></a> 增補字元    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供資料類型 (例如 **nchar** 和 **nvarchar** ) 來儲存 Unicode 資料。 這些資料類型會使用稱為 *UTF-16*的格式來編碼文字。 Unicode Consortium 會為每個字元配置唯一的字碼指標，其值介於 0x0000 到 0x10FFFF 的範圍。 最常用的字元具有可在記憶體和磁碟上納入 16 位元單字的字碼指標值，但是字碼指標值大於 0xFFFF 的字元則需要兩個連續的 16 位元單字。 這些字元稱為 *「增補字元」*(Supplementary Character)，而這兩個連續的 16 位元單字則稱為 *「Surrogate 字組」*(Surrogate Pair)。    
    
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中引進之全新系列的增補字元 (_SC) 定序可以搭配 **nchar**、**nvarchar** 和 **sql_variant** 資料類型使用。 例如： `Latin1_General_100_CI_AS_SC`或 `Japanese_Bushu_Kakusu_100_CI_AS_SC`(如果使用日文定序的話)。    

 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始，所有新定序都會自動支援增補字元。

 如果您使用增補字元：    
    
-   增補字元可用於 90 (含) 以上定序版本的排序及比較作業。    
    
-   所有版本 100 定序都支援含有增補字元的語言排序。    
    
-   不支援在中繼資料內使用增補字元，例如資料庫物件的名稱。    
    
-   無法啟用搭配使用定序與增補字元 (\_SC) 的資料庫，進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。 這是因為針對複寫所建立的某些系統資料表和預存程序使用舊版 **ntext** 資料類型，其不支援增補字元。  
    
-   SC 旗標可套用至：    
    
    -   版本 90 定序    
    
    -   版本 100 定序    
    
-   SC 旗標無法套用至：    
    
    -   80 版本的非版本控制 Windows 定序    
    
    -   BIN 或 BIN2 二進位定序    
    
    -   SQL\* 定序    
    
    -   版本 140 定序 (這些定序已支援增補字元，因此不需要 SC 旗標)    
    
 下表將比較當某些字串函式和字串運算子使用增補字元搭配或不搭配增補字元感知 (SCA) 定序時，這些函式和運算子的行為：    
    
|字串函數或運算子|搭配增補字元感知 (SCA) 定序|不搭配 SCA 定序|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|將 UTF-16 Surrogate 字組視為單一字碼指標。|將 UTF-16 Surrogate 字組視為兩個字碼指標。|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|這些函數會將每個 Surrogate 字組視為單一字碼指標，並且如預期方式運作。|這些函數可能會將 Surrogate 字組拆開，造成無法預期的結果。|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|傳回對應至指定之 Unicode 字碼指標值 (在 0 到 0x10FFFF 的範圍內) 的字元。 如果指定的值位於 0 到 0xFFFF 的範圍內，就會傳回單一字元。 若為更高的值，則傳回對應的 Surrogate。|高於 0xFFFF 的值會傳回 NULL 而非對應的 Surrogate。|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|傳回 UTF-16 字碼指標 (在 0 到 0x10FFFF 的範圍內)。|傳回 UCS-2 字碼指標 (在 0 到 0xFFFF 的範圍內)。|    
|[符合單一萬用字元](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [萬用字元 - 不相符的字元](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|增補字元支援所有萬用字元作業。|增補字元不支援這些萬用字元作業， 但支援其他萬用字元運算子。|    
    
##  <a name="GB18030"></a> GB18030 支援    
 GB18030 是一種獨立標準，可供中華人民共和國進行中文字元的編碼。 在 GB18030 中，字元的長度可以是 1、2 或 4 個位元組。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可在 GB18030 編碼的字元從用戶端應用程式進入伺服器時加以辨識，並在轉換後以原生模式將其儲存為 Unicode 字元，藉以支援這種編碼的字元。 當 GB18030 編碼的字元儲存在伺服器中後，任何後續作業都會將其視為 Unicode 字元。 您可以使用任何中文定序，最好是使用最新的 100 版本。 所有 _100 層級定序都支援含有 GB18030 字元的語言排序。 如果資料包含增補字元 (Surrogate 字組)，您就可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供的 SC 定序來改善搜尋和排序。    
    
##  <a name="Complex_script"></a> 複雜字集支援    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以支援輸入、儲存、變更和顯示複雜字集。 複雜字集包括下列類型：    
    
-   包括由右至左和由左至右兩種文字之組合的字集，如阿拉伯文和英文文字的組合。    
-   字元的形狀會隨著位置或是否結合其他字元而不同的字集，例如，阿拉伯文、印度文和泰文字元。    
-   泰文之類的語言，因為單字之間不中斷，所以需要用內部字典來辨識單字。    
    
與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 互動的資料庫應用程式必須使用支援複雜字集的控制項。 Managed 程式碼中所建立的標準 Windows Form 控制項具有複雜字集的功能。    

##  <a name="Japanese_Collations"></a> 在  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，支援兩種新的日文定序系列，可使用不同選項 (\_CS、\_AS、\_KS、\_WS、\_VSS) 排列。 

您可查詢 SQL Server 資料庫引擎列出這些定序：
``` 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

所有新定序都內建增補字元支援，因此沒有且不需要 SC 旗標。

資料庫引擎索引、記憶體最佳化資料表、資料行存放區索引和原生編譯的模組都支援這些定序。
    
##  <a name="Related_Tasks"></a> 相關工作    
    
|工作|主題|    
|----------|-----------|    
|描述如何設定或變更 SQL Server 執行個體的定序。|[設定或變更伺服器定序](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|描述如何設定或變更使用者資料庫的定序。|[設定或變更資料庫定序](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|描述如何設定或變更資料庫中資料行的定序。|[設定或變更資料行定序](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|描述如何傳回伺服器、資料庫或資料行層級的定序資訊。|[檢視定序資訊](../../relational-databases/collations/view-collation-information.md)|    
|描述如何撰寫 Transact-SQL 陳述式，讓它們可以從某種語言移植至另一種語言，或更輕鬆地支援多種語言。|[撰寫國際通用的 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|描述如何變更錯誤訊息的語言，以及日期、時間和貨幣資料之使用和顯示方式的喜好設定。|[設定工作階段語言](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> 相關內容    
 [SQL Server 最佳作法定序變更](http://go.microsoft.com/fwlink/?LinkId=113891)    
    
 [＜SQL Server 最佳作法：移轉至 Unicode＞](http://go.microsoft.com/fwlink/?LinkId=113890)    
    
 [Unicode Consortium 網站](http://go.microsoft.com/fwlink/?LinkId=48619)    
    
## <a name="see-also"></a>另請參閱    
 [自主資料庫定序](../../relational-databases/databases/contained-database-collations.md)     
 [選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)    
    
  

