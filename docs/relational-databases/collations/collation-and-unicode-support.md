---
title: 定序與 Unicode 支援 | Microsoft 文件
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
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
- UTF-8
- UTF-16
- UTF8
- UTF16
- UCS2
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: pmasl
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 862147cfb7620999bf3e56a90fae0e90fbb1be45
ms.sourcegitcommit: 0d34b654f0b3031041959e87f5b4d4f0a1af6a29
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2019
ms.locfileid: "74901947"
---
# <a name="collation-and-unicode-support"></a>定序與 Unicode 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的定序會提供資料的排序規則、大小寫和區分腔調字屬性。 與字元資料類型 (例如 **char** 和 **varchar**) 搭配使用的定序會指示字碼頁，以及可針對該資料類型表示的對應字元。 

不論您是安裝新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體、還原資料庫備份，還是將伺服器連線至用戶端資料庫，都請務必了解您要使用之資料的地區設定需求、排序次序和區分大小寫與腔調字。 若要列出您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所提供的定序，請參閱 [sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)。    
    
當您針對伺服器、資料庫、資料行或運算式選取定序時，就是將某些特性指派給資料。 這些特性會影響資料庫中許多作業的結果。 例如，當您使用 `ORDER BY` 來建構查詢時，結果集排序次序可能會相依於套用至資料庫的定序，或在查詢運算式層級指定於 `COLLATE` 子句中的定序。    
    
為了有效運用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的定序支援，您應了解本主題中定義的字詞，以及它們與資料特性的關聯。    
    
##  <a name="Terms"></a> 定序字詞    
    
-   [定序](#Collation_Defn) 
    - [定序集](#Collation_sets)
    - [定序層級](#Collation_levels)
-   [地區設定](#Locale_Defn)    
-   [字碼頁](#Code_Page_Defn)    
-   [排序次序](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> 定序    
定序指定位元模式，代表資料集中的每一個字元。 定序也可以決定排序和比較資料的規則。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援在單一資料庫中儲存具備不同定序的物件。 對於非 Unicode 資料行，定序設定則指定資料的字碼頁以及可代表的字元。 在非 Unicode 資料行之間移動的資料必須從來源字碼頁轉換成目的地字碼頁。    
    
當[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在各有不同定序設定的不同資料庫內容中執行時，陳述式的結果可能不同。 如果可能的話，請針對組織使用標準化定序。 這樣您就不需要在每一個字元或 Unicode 運算式中指定定序。 如果您必須使用有不同定序和字碼頁設定的物件，則在編寫查詢程式碼時，必須考量定序優先順序的規則。 如需詳細資訊，請參閱 [定序優先順序 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)。    
    
與定序建立關聯的選項會區分大小寫、區分腔調字、區分假名、區分全半形和區分變化選取器。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 引進一個適用於 [UTF-8](https://www.wikipedia.org/wiki/UTF-8) 編碼的額外選項。 

您可以將它們附加至定序名稱來指定這些選項。 例如，此定序 **Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8** 區分大小寫、區分腔調字、區分假名、區分全半形並以 UTF-8 編碼。 例如，此定序 **Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS** 不區分大小寫、不區分腔調字、區分假名、區分全半形和區分變化選取器，並使用非 Unicode 編碼。 

下表描述與這些不同選項建立關聯的行為：    
    
|選項|描述|    
|------------|-----------------|    
|區分大小寫 (\_CS)|區分大寫和小寫字母。 如果選取此選項，小寫字母會排序在大寫字母的前面。 如果未選取此選項，定序就不會區分大小寫。 亦即，在排序用途上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將大寫和小寫字母視為相同。 指定 \_CI，就可以明確地選取不區分大小寫。|   
|區分腔調字 (\_AS)|區分有腔調和無腔調的字元。 例如，"a" 不等於 "ấ"。 如果未選取此選項，定序就不會區分腔調。 亦即，在排序用途上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將有腔調和無腔調字母視為相同。 指定 \_AI，就可以明確地選取不區分腔調字。|    
|區分假名 (\_KS)|區分兩種類型的日文假名字元：平假名與片假名。 如果未選取此選項，定序就不會區分假名。 亦即，在排序用途上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將平假名和片假名視為相同。 省略此選項是指定不區分假名的唯一方法。|   
|區分全半形 (\_WS)|區分全形與半形字元。 如果未選取此選項，則針對排序用途上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將相同字元的全形和半形表示法視為相同。 省略此選項，是指定不區分全形與半形的唯一方法。|  
|區分變化選取器 (\_VSS)|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中首次引進如何區分日文定序 **Japanese_Bushu_Kakusu_140** 和 **Japanese_XJIS_140** 中的各種不同表意字元變化選取器。 變化序列是由基底字元加上額外的變化選取器所組成。 如果未選取此 \_VSS 選項，則定序不區分變化選取器，且比較時不會考慮變化選取器。 亦即，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基於排序目的，會將建置在相同基底字元但使用不同變化選取器的字元視為相同。 如需詳細資訊，請參閱 [Unicode Ideographic Variation Database](https://www.unicode.org/reports/tr37/) (Unicode 表意字元變化資料庫)。<br/><br/> 全文檢索搜尋索引不支援區分變化選取器 (\_VSS) 定序。 全文檢索搜尋索引支援只區分腔調字 (\_AS)、區分假名 (\_KS) 和區分全半形 (\_WS) 選項。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 和 CLR 引擎不支援 (\_VSS) 變化選取器。|      
|二進位 (\_BIN)<sup>1</sup>|依據對每一個字元定義的位元模式來排序和比較 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中資料。 二進位排序次序為區分大小寫且區分腔調字。 二進位也是最快的排序順序。 如需詳細資訊，請參閱本文的[＜二進位定序＞](#Binary-collations)一節。|      
|二進位字碼指標 (\_BIN2)<sup>1</sup> | 依據 Unicode 資料的 Unicode 字碼指標來排序和比較 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中資料。 針對非 Unicode 資料，二進位字碼指標將使用與二進位排序相同的比較。<br/><br/> 使用二進位字碼指標排序次序的好處，就是在比較已排序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的應用程式中不需要對資料進行重新排序。 因此，二進位字碼指標排序次序可簡化應用程式的開發並提升效能。 如需詳細資訊，請參閱本文的[＜二進位定序＞](#Binary-collations)一節。|
|UTF-8 (\_UTF8)|讓 UTF-8 編碼資料儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果未選取此選項，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用適用資料類型的預設非 Unicode 編碼格式。 如需詳細資訊，請參閱本文的[＜UTF-8 支援＞](#utf8)一節。| 

<sup>1</sup> 如果選取二進位或二進位字碼指標，則無法使用區分大小寫 (\_CS)、區分腔調字 (\_AS)、區分假名 (\_KS) 和區分全半形 (\_WS) 選項。      

#### <a name="examples-of-collation-options"></a>定序選項的範例
每一個定序都會結合成一系列後置詞，以定義大小寫、腔調字、全半形或假名的區分。 下列範例描述不同後置詞結合的排序次序行為。

|Windows 定序後置詞|排序順序描述|
|------------|-----------------| 
|\_BIN<sup>1</sup>|二進位排序|
|\_BIN2<sup>1, 2</sup>|二進位字碼指標排序次序|
|\_CI_AI<sup>2</sup>|不區分大小寫、不區分腔調字、不區分假名、不區分全半形|
|\_CI_AI_KS<sup>2</sup>|不區分大小寫、不區分腔調字、區分假名、不區分全半形|
|\_CI_AI_KS_WS<sup>2</sup>|不區分大小寫、不區分腔調字、區分假名、區分全半形|
|\_CI_AI_WS<sup>2</sup>|不區分大小寫、不區分腔調字、不區分假名、區分全半形|
|\_CI_AS<sup>2</sup>|不區分大小寫、區分腔調字、不區分假名、不區分全半形|
|\_CI_AS_KS<sup>2</sup>|不區分大小寫、區分腔調字、區分假名、不區分全半形|
|\_CI_AS_KS_WS<sup>2</sup>|不區分大小寫、區分腔調字、區分假名、區分全半形|
|\_CI_AS_WS<sup>2</sup>|不區分大小寫、區分腔調字、不區分假名、區分全半形|
|\_CS_AI<sup>2</sup>|區分大小寫、不區分腔調字、不區分假名、不區分全半形|
|\_CS_AI_KS<sup>2</sup>|區分大小寫、不區分腔調字、區分假名、不區分全半形|
|\_CS_AI_KS_WS<sup>2</sup>|區分大小寫、不區分腔調字、區分假名、區分全半形|
|\_CS_AI_WS<sup>2</sup>|區分大小寫、不區分腔調字、不區分假名、區分全半形|
|\_CS_AS<sup>2</sup>|區分大小寫、區分腔調字、不區分假名、不區分全半形|
|\_CS_AS_KS<sup>2</sup>|區分大小寫、區分腔調字、區分假名、不區分全半形|
|\_CS_AS_KS_WS<sup>2</sup>|區分大小寫、區分腔調字、區分假名、區分全半形|
|\_CS_AS_WS<sup>2</sup>|區分大小寫、區分腔調字、不區分假名、區分全半形|

<sup>1</sup> 如果選取二進位或二進位字碼指標，則無法使用區分大小寫 (\_CS)、區分腔調字 (\_AS)、區分假名 (\_KS) 和區分全半形 (\_WS) 選項。    

<sup>2</sup> 新增 UTF-8 選項 (\_UTF8) 會啟用使用 UTF-8 來編碼 Unicode 資料。 如需詳細資訊，請參閱本文的[＜UTF-8 支援＞](#utf8)一節。 

### <a name="Collation_sets"></a> 定序集

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援下列定序集：    

-  [Windows 定序](#Windows-collations)
-  [二進位定序](#Binary-collations)
-  [SQL Server 定序](#SQL-collations)
    
#### <a name="Windows-collations"></a> Windows 定序    
Windows 定序會定義規則，以便依據相關聯的 Windows 系統地區設定來儲存字元資料。 針對 Windows 定序，您可以使用與 Unicode 資料相同的演算法，來執行非 Unicode 資料的比較。 基本 Windows 定序規則會指定套用字典排序時使用的字母或語言。 這些規則也會指定用來儲存非 Unicode 字元資料的字碼頁。 Unicode 和非 Unicode 排序都與特定 Windows 版本中的字串比較相容。 如此可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的各種資料類型取得一致性，同時讓開發人員能夠使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相同的規則在應用程式中排序字串。 如需詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)。    
    
#### <a name="Binary-collations"></a> 二進位定序    
二進位定序依據地區設定和資料類型所定義的字碼值順序來排序資料。 它們區分大小寫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中二進位定序會定義所使用的地區設定和 ANSI 字碼頁。 這會強制使用二進位排序次序。 因為它們相對而言較為簡單，所以二進位定序可提升應用程式效能。 如果是非 Unicode 資料類型，資料比較是依據 ANSI 字碼頁中所定義的字碼指標。 如果是 Unicode 資料類型，資料比較則是依據 Unicode 字碼指標。 如果是 Unicode 資料類型的二進位定序，在資料排序時不會考量地區設定。 例如，**Latin_1_General_BIN** 和 **Japanese_BIN** 用於 Unicode 資料時會產生相同的排序結果。 如需詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)。   
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中有兩種二進位定序類型：

-  舊版 **BIN** 定序，對 Unicode 資料執行未完成的字碼指標對字碼指標比較。 這些舊版二進位定序會將第一個字元作為 WCHAR 進行比較，之後再以逐位元組的方式進行比較。 在 BIN 定序中，只有第一個字元是根據字碼指標排序，剩餘字元則是根據其位元組值排序。

-  較新的 **BIN2** 定序會實作純字碼指標比較。 在 BIN2 定序中，所有字元都是根據其字碼指標排序。 因為 Intel 平台是 Little Endian 架構，所以 Unicode 字碼字元一律以位元組交換的方式儲存。     
    
#### <a name="SQL-collations"></a> SQL Server 定序    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序 (SQL_\*) 會提供與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 舊版的排序次序相容性。 非 Unicode 資料的字典排序規則與 Windows 作業系統所提供任何排序常式不相容。 不過，Unicode 資料的排序與 Windows 排序規則的特定版本相容。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序對非 Unicode 和 Unicode 資料使用不同的比較規則，所以您會看到相同資料的比較有不同的結果，這取決於基礎資料類型而定。 如需詳細資訊，請參閱 [SQL Server 定序名稱 (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)。 

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定期間，預設安裝定序設定會由作業系統 (OS) 地區設定決定。 您可以在安裝期間變更伺服器層級的定序，也可以在安裝之前變更 OS 地區設定。 基於回溯相容性的原因，預設定序會設定為與每個特定地區設定建立關聯的最舊可用版本。 因此，此定序不一定是建議的定序。 若要完全利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的功能，請變更預設安裝設定以使用 Windows 定序。 例如，針對 OS 地區設定 [英文 (美國)] (字碼頁 1252)，安裝期間的預設定序是 **SQL_Latin1_General_CP1_CI_AS**，且可以變更為與其最接近的 Windows 定序對應項目 **Latin1_General_100_CI_AS_SC**。
    
> [!NOTE]    
> 當您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的英文執行個體時，您可以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序 (SQL_\*)，以與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的現有執行個體相容。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序是在安裝期間定義，所以當下列條件成立時，請務必小心指定定序設定：    
>     
> -   應用程式的程式碼視先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序行為而定。    
> -   您必須儲存反映多國語言的字元資料。    
    
### <a name="Collation_levels"></a> 定序層級
您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的下列層級設定定序：    

-  [伺服器層級定序](#Server-level-collations)
-  [資料庫層級定序](#Database-level-collations)
-  [資料行層級定序](#Column-level-collations)
-  [運算式層級定序](#Expression-level-collations)

#### <a name="Server-level-collations"></a> 伺服器層級定序   
預設伺服器定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定期間決定，因此會成為系統資料庫和所有使用者資料庫的預設定序。 

下表顯示由作業系統 (OS) 地區設定決定的預設定序指定，包括其 Windows 和 SQL 語言代碼識別碼 (LCID)：

|Windows 地區設定|Windows LCID|SQL LCID|預設定序|
|---------------|---------|---------|---------------|
|南非荷蘭文 (南非)|0x0436|0x0409|Latin1_General_CI_AS|
|阿爾巴尼亞文 (阿爾巴尼亞)|0x041c|0x041c|Albanian_CI_AS|
|亞爾薩斯語 (法國)|0x0484|0x0409|Latin1_General_CI_AS|
|阿姆哈拉文 (衣索比亞)|0x045e|0x0409|Latin1_General_CI_AS|
|阿拉伯文 (阿爾及利亞)|0x1401|0x0401|Arabic_CI_AS|
|阿拉伯文 (巴林)|0x3c01|0x0401|Arabic_CI_AS|
|阿拉伯文 (埃及)|0x0c01|0x0401|Arabic_CI_AS|
|阿拉伯文 (伊拉克)|0x0801|0x0401|Arabic_CI_AS|
|阿拉伯文 (約旦)|0x2c01|0x0401|Arabic_CI_AS|
|阿拉伯文 (科威特)|0x3401|0x0401|Arabic_CI_AS|
|阿拉伯文 (黎巴嫩)|0x3001|0x0401|Arabic_CI_AS|
|阿拉伯文 (利比亞)|0x1001|0x0401|Arabic_CI_AS|
|阿拉伯文 (摩洛哥)|0x1801|0x0401|Arabic_CI_AS|
|阿拉伯文 (阿曼)|0x2001|0x0401|Arabic_CI_AS|
|阿拉伯文 (卡達)|0x4001|0x0401|Arabic_CI_AS|
|阿拉伯文 (沙烏地阿拉伯)|0x0401|0x0401|Arabic_CI_AS|
|阿拉伯文 (敘利亞)|0x2801|0x0401|Arabic_CI_AS|
|阿拉伯文 (突尼西亞)|0x1c01|0x0401|Arabic_CI_AS|
|阿拉伯文 (阿拉伯聯合大公國)|0x3801|0x0401|Arabic_CI_AS|
|阿拉伯文 (葉門)|0x2401|0x0401|Arabic_CI_AS|
|亞美尼亞文 (亞美尼亞)|0x042b|0x0419|Latin1_General_CI_AS|
|阿薩姆文 (印度)|0x044d|0x044d|伺服器層級無法使用|
|阿澤里文 (亞塞拜然，斯拉夫)|0x082c|0x082c|已淘汰，伺服器層級無法使用|
|阿澤里文 (亞塞拜然，拉丁)|0x042c|0x042c|已淘汰，伺服器層級無法使用|
|巴什喀爾文 (俄羅斯)|0x046d|0x046d|Latin1_General_CI_AI|
|巴斯克文 (巴斯克)|0x042d|0x0409|Latin1_General_CI_AS|
|白俄羅斯文 (白俄羅斯)|0x0423|0x0419|Cyrillic_General_CI_AS|
|孟加拉文 (孟加拉)|0x0845|0x0445|伺服器層級無法使用|
|孟加拉文 (印度)|0x0445|0x0439|伺服器層級無法使用|
|波士尼亞文 (波士尼亞赫塞哥維納，斯拉夫)|0x201a|0x201a|Latin1_General_CI_AI|
|波士尼亞文 (波士尼亞赫塞哥維納，拉丁)|0x141a|0x141a|Latin1_General_CI_AI|
|布里敦文 (法國)|0x047e|0x047e|Latin1_General_CI_AI|
|保加利亞文 (保加利亞)|0x0402|0x0419|Cyrillic_General_CI_AS|
|加泰蘭文 (加泰蘭)|0x0403|0x0409|Latin1_General_CI_AS|
|中文 (香港特別行政區、中國)|0x0c04|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|中文 (澳門特別行政區)|0x1404|0x1404|Latin1_General_CI_AI|
|中文 (澳門)|0x21404|0x21404|Latin1_General_CI_AI|
|中文 (中國)|0x0804|0x0804|Chinese_PRC_CI_AS|
|中文 (中國)|0x20804|0x20804|Chinese_PRC_Stroke_CI_AS|
|中文 (新加坡)|0x1004|0x0804|Chinese_PRC_CI_AS|
|中文 (新加坡)|0x21004|0x20804|Chinese_PRC_Stroke_CI_AS|
|中文 (台灣)|0x30404|0x30404|Chinese_Taiwan_Bopomofo_CI_AS|
|中文 (台灣)|0x0404|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|科西嘉文 (法國)|0x0483|0x0483|Latin1_General_CI_AI|
|克羅埃西亞文 (波士尼亞赫塞哥維納，拉丁)|0x101a|0x041a|Croatian_CI_AS|
|克羅埃西亞文 (克羅埃西亞)|0x041a|0x041a|Croatian_CI_AS|
|捷克文 (捷克共和國)|0x0405|0x0405|Czech_CI_AS|
|丹麥文 (丹麥)|0x0406|0x0406|Danish_Norwegian_CI_AS|
|達利語 (阿富汗)|0x048c|0x048c|Latin1_General_CI_AI|
|迪維西文 (馬爾地夫)|0x0465|0x0465|伺服器層級無法使用|
|荷蘭文 (比利時)|0x0813|0x0409|Latin1_General_CI_AS|
|荷蘭文 (荷蘭)|0x0413|0x0409|Latin1_General_CI_AS|
|英文 (澳大利亞)|0x0c09|0x0409|Latin1_General_CI_AS|
|英文 (貝里斯)|0x2809|0x0409|Latin1_General_CI_AS|
|英文 (加拿大)|0x1009|0x0409|Latin1_General_CI_AS|
|英文 (加勒比海)|0x2409|0x0409|Latin1_General_CI_AS|
|英文 (印度)|0x4009|0x0409|Latin1_General_CI_AS|
|英文 (愛爾蘭)|0x1809|0x0409|Latin1_General_CI_AS|
|英文 (牙買加)|0x2009|0x0409|Latin1_General_CI_AS|
|英文 (馬來西亞)|0x4409|0x0409|Latin1_General_CI_AS|
|英文 (紐西蘭)|0x1409|0x0409|Latin1_General_CI_AS|
|英文 (菲律賓)|0x3409|0x0409|Latin1_General_CI_AS|
|英文 (新加坡)|0x4809|0x0409|Latin1_General_CI_AS|
|英文 (南非)|0x1c09|0x0409|Latin1_General_CI_AS|
|英文 (千里達及托巴哥)|0x2c09|0x0409|Latin1_General_CI_AS|
|英文 (英國)|0x0809|0x0409|Latin1_General_CI_AS|
|英文 (美國)|0x0409|0x0409|SQL_Latin1_General_CP1_CI_AS|
|英文 (辛巴威)|0x3009|0x0409|Latin1_General_CI_AS|
|愛沙尼亞文 (愛沙尼亞)|0x0425|0x0425|Estonian_CI_AS|
|法羅文 (法羅群島)|0x0438|0x0409|Latin1_General_CI_AS|
|菲律賓文 (菲律賓)|0x0464|0x0409|Latin1_General_CI_AS|
|芬蘭文 (芬蘭)|0x040b|0x040b|Finnish_Swedish_CI_AS|
|法文 (比利時)|0x080c|0x040c|French_CI_AS|
|法文 (加拿大)|0x0c0c|0x040c|French_CI_AS|
|法文 (法國)|0x040c|0x040c|French_CI_AS|
|法文 (盧森堡)|0x140c|0x040c|French_CI_AS|
|法文 (摩納哥)|0x180c|0x040c|French_CI_AS|
|法文 (瑞士)|0x100c|0x040c|French_CI_AS|
|夫里斯蘭文 (荷蘭)|0x0462|0x0462|Latin1_General_CI_AI|
|加利西亞文 (西班牙)|0x0456|0x0409|Latin1_General_CI_AS|
|喬治亞文 (喬治亞)|0x10437|0x10437|Georgian_Modern_Sort_CI_AS|
|喬治亞文 (喬治亞)|0x0437|0x0419|Latin1_General_CI_AS|
|德文 - 電話簿排序 (DIN)|0x10407|0x10407|German_PhoneBook_CI_AS|
|德文 (奧地利)|0x0c07|0x0409|Latin1_General_CI_AS|
|德文 (德國)|0x0407|0x0409|Latin1_General_CI_AS|
|德文 (列支敦斯登)|0x1407|0x0409|Latin1_General_CI_AS|
|德文 (盧森堡)|0x1007|0x0409|Latin1_General_CI_AS|
|德文 (瑞士)|0x0807|0x0409|Latin1_General_CI_AS|
|希臘文 (希臘)|0x0408|0x0408|Greek_CI_AS|
|格陵蘭文 (格陵蘭)|0x046f|0x0406|Danish_Norwegian_CI_AS|
|古吉拉特文 (印度)|0x0447|0x0439|伺服器層級無法使用|
|豪撒文 (奈及利亞，拉丁)|0x0468|0x0409|Latin1_General_CI_AS|
|希伯來文 (以色列)|0x040d|0x040d|Hebrew_CI_AS|
|印度文 (印度)|0x0439|0x0439|伺服器層級無法使用|
|匈牙利文 (匈牙利)|0x040e|0x040e|Hungarian_CI_AS|
|匈牙利文技術排序|0x1040e|0x1040e|Hungarian_Technical_CI_AS|
|冰島文 (冰島)|0x040f|0x040f|Icelandic_CI_AS|
|伊布文 (奈及利亞)|0x0470|0x0409|Latin1_General_CI_AS|
|印尼文 (印尼)|0x0421|0x0409|Latin1_General_CI_AS|
|因紐特文 (加拿大，拉丁)|0x085d|0x0409|Latin1_General_CI_AS|
|因紐特文 (語音節) 加拿大|0x045d|0x045d|Latin1_General_CI_AI|
|愛爾蘭文 (愛爾蘭)|0x083c|0x0409|Latin1_General_CI_AS|
|義大利文 (義大利)|0x0410|0x0409|Latin1_General_CI_AS|
|義大利文 (瑞士)|0x0810|0x0409|Latin1_General_CI_AS|
|日文 (日本 XJIS)|0x0411|0x0411|Japanese_CI_AS|
|日文 (日本)|0x040411|0x40411|Latin1_General_CI_AI|
|坎那達文 (印度)|0x044b|0x0439|伺服器層級無法使用|
|哈薩克文 (哈薩克)|0x043f|0x043f|Kazakh_90_CI_AS|
|高棉文 (柬埔寨)|0x0453|0x0453|伺服器層級無法使用|
|基切語 (瓜地馬拉)|0x0486|0x0c0a|Modern_Spanish_CI_AS|
|金揚萬答文 (盧安達)|0x0487|0x0409|Latin1_General_CI_AS|
|貢根文 (印度)|0x0457|0x0439|伺服器層級無法使用|
|韓文 (韓國字典排序)|0x0412|0x0412|Korean_Wansung_CI_AS|
|吉爾吉斯文 (吉爾吉斯)|0x0440|0x0419|Cyrillic_General_CI_AS|
|寮文 (寮國人民共合國)|0x0454|0x0454|伺服器層級無法使用|
|拉脫維亞文 (拉脫維亞)|0x0426|0x0426|Latvian_CI_AS|
|立陶宛文 (立陶宛)|0x0427|0x0427|Lithuanian_CI_AS|
|下索布語 (德國)|0x082e|0x0409|Latin1_General_CI_AS|
|盧森堡文 (盧森堡)|0x046e|0x0409|Latin1_General_CI_AS|
|馬其頓文 (馬其頓，馬其頓共和國)|0x042f|0x042f|Macedonian_FYROM_90_CI_AS|
|馬來文 (汶萊達魯薩蘭)|0x083e|0x0409|Latin1_General_CI_AS|
|馬來文 (馬來西亞)|0x043e|0x0409|Latin1_General_CI_AS|
|馬來亞拉姆文 (印度)|0x044c|0x0439|伺服器層級無法使用|
|馬爾他文 (馬爾他)|0x043a|0x043a|Latin1_General_CI_AI|
|毛利文 (紐西蘭)|0x0481|0x0481|Latin1_General_CI_AI|
|馬普切文 (智利)|0x047a|0x047a|Latin1_General_CI_AI|
|馬拉提文 (印度)|0x044e|0x0439|伺服器層級無法使用|
|莫霍克文 (加拿大)|0x047a|0x047a|Latin1_General_CI_AI|
|蒙古文 (蒙古)|0x0450|0x0419|Cyrillic_General_CI_AS|
|蒙古文 (中國)|0x0850|0x0419|Cyrillic_General_CI_AS|
|尼泊爾文 (尼泊爾)|0x0461|0x0461|伺服器層級無法使用|
|挪威文 (巴克摩，挪威)|0x0414|0x0414|Latin1_General_CI_AI|
|挪威文 (耐諾斯克，挪威)|0x0814|0x0414|Latin1_General_CI_AI|
|奧西坦文 (法國)|0x0482|0x040c|French_CI_AS|
|歐利亞文 (印度)|0x0448|0x0439|伺服器層級無法使用|
|普什圖文 (阿富汗)|0x0463|0x0463|伺服器層級無法使用|
|波斯文 (伊朗)|0x0429|0x0429|Latin1_General_CI_AI|
|波蘭文 (波蘭)|0x0415|0x0415|Polish_CI_AS|
|葡萄牙文 (巴西)|0x0416|0x0409|Latin1_General_CI_AS|
|葡萄牙文 (葡萄牙)|0x0816|0x0409|Latin1_General_CI_AS|
|旁遮普語 (印度)|0x0446|0x0439|伺服器層級無法使用|
|蓋楚瓦文 (玻利維亞)|0x046b|0x0409|Latin1_General_CI_AS|
|蓋楚瓦文 (厄瓜多)|0x086b|0x0409|Latin1_General_CI_AS|
|蓋楚瓦文 (秘魯)|0x0c6b|0x0409|Latin1_General_CI_AS|
|羅馬尼亞文 (羅馬尼亞)|0x0418|0x0418|Romanian_CI_AS|
|羅曼斯文 (瑞士)|0x0417|0x0417|Latin1_General_CI_AI|
|俄文 (俄羅斯)|0x0419|0x0419|Cyrillic_General_CI_AS|
|沙米文 (伊納立，芬蘭)|0x243b|0x083b|Latin1_General_CI_AI|
|沙米文 (盧勒，挪威)|0x103b|0x043b|Latin1_General_CI_AI|
|沙米文 (盧勒，瑞典)|0x143b|0x083b|Latin1_General_CI_AI|
|沙米文 (北，芬蘭)|0x0c3b|0x083b|Latin1_General_CI_AI|
|沙米文 (北，挪威)|0x043b|0x043b|Latin1_General_CI_AI|
|沙米文 (北，瑞典)|0x083b|0x083b|Latin1_General_CI_AI|
|沙米文 (斯科特，芬蘭)|0x203b|0x083b|Latin1_General_CI_AI|
|沙米文 (南，挪威)|0x183b|0x043b|Latin1_General_CI_AI|
|沙米文 (南，瑞典)|0x1c3b|0x083b|Latin1_General_CI_AI|
|梵文 (印度)|0x044f|0x0439|伺服器層級無法使用|
|塞爾維亞文 (波士尼亞赫塞哥維納，斯拉夫)|0x1c1a|0x0c1a|Latin1_General_CI_AI|
|塞爾維亞文 (波士尼亞赫塞哥維納，拉丁)|0x181a|0x081a|Latin1_General_CI_AI|
|塞爾維亞文 (塞爾維亞，斯拉夫)|0x0c1a|0x0c1a|Latin1_General_CI_AI|
|塞爾維亞文 (塞爾維亞，拉丁)|0x081a|0x081a|Latin1_General_CI_AI|
|賴索托文/北索托文 (南非)|0x046c|0x0409|Latin1_General_CI_AS|
|塞茲瓦納文/班圖文 (南非)|0x0432|0x0409|Latin1_General_CI_AS|
|僧伽羅語 (斯里蘭卡)|0x045b|0x0439|伺服器層級無法使用|
|斯洛伐克文 (斯洛伐克)|0x041b|0x041b|Slovak_CI_AS|
|斯洛維尼亞文 (斯洛維尼亞)|0x0424|0x0424|Slovenian_CI_AS|
|西班牙文 (阿根廷)|0x2c0a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (玻利維亞)|0x400a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (智利)|0x340a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (哥倫比亞)|0x240a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (哥斯大黎加)|0x140a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (多明尼加)|0x1c0a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (厄瓜多)|0x300a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (薩爾瓦多)|0x440a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (瓜地馬拉)|0x100a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (宏都拉斯)|0x480a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (墨西哥)|0x080a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (尼加拉瓜)|0x4c0a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (巴拿馬)|0x180a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (巴拉圭)|0x3c0a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (秘魯)|0x280a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (波多黎各)|0x500a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (西班牙)|0x0c0a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (西班牙，傳統排序)|0x040a|0x040a|Traditional_Spanish_CI_AS|
|西班牙文 (美國)|0x540a|0x0409|Latin1_General_CI_AS|
|西班牙文 (烏拉圭)|0x380a|0x0c0a|Modern_Spanish_CI_AS|
|西班牙文 (委內瑞拉)|0x200a|0x0c0a|Modern_Spanish_CI_AS|
|斯瓦希里文 (肯亞)|0x0441|0x0409|Latin1_General_CI_AS|
|瑞典文 (芬蘭)|0x081d|0x040b|Finnish_Swedish_CI_AS|
|瑞典文 (瑞典)|0x041d|0x040b|Finnish_Swedish_CI_AS|
|敘利亞文 (敘利亞)|0x045a|0x045a|伺服器層級無法使用|
|塔吉克文 (塔吉克)|0x0428|0x0419|Cyrillic_General_CI_AS|
|塔馬塞特文 (阿爾及利亞，拉丁)|0x085f|0x085f|Latin1_General_CI_AI|
|坦米爾文 (印度)|0x0449|0x0439|伺服器層級無法使用|
|韃靼文 (俄羅斯)|0x0444|0x0444|Cyrillic_General_CI_AS|
|特拉古文 (印度)|0x044a|0x0439|伺服器層級無法使用|
|泰文 (泰國)|0x041e|0x041e|Thai_CI_AS|
|藏文 (中國)|0x0451|0x0451|伺服器層級無法使用|
|土耳其文 (土耳其)|0x041f|0x041f|Turkish_CI_AS|
|土庫曼文 (土庫曼)|0x0442|0x0442|Latin1_General_CI_AI|
|維吾爾文 (中國)|0x0480|0x0480|Latin1_General_CI_AI|
|烏克蘭文 (烏克蘭)|0x0422|0x0422|Ukrainian_CI_AS|
|上索布語 (德國)|0x042e|0x042e|Latin1_General_CI_AI|
|烏都文 (巴基斯坦)|0x0420|0x0420|Latin1_General_CI_AI|
|烏茲別克文 (烏茲別克，斯拉夫)|0x0843|0x0419|Cyrillic_General_CI_AS|
|烏茲別克文 (烏茲別克，拉丁)|0x0443|0x0443|Uzbek_Latin_90_CI_AS|
|越南文 (越南)|0x042a|0x042a|Vietnamese_CI_AS|
|威爾斯文 (英國)|0x0452|0x0452|Latin1_General_CI_AI|
|沃洛夫文 (塞內加爾)|0x0488|0x040c|French_CI_AS|
|科薩文/科薩文 (南非)|0x0434|0x0409|Latin1_General_CI_AS|
|雅庫特語 (俄羅斯)|0x0485|0x0485|Latin1_General_CI_AI|
|爨文 (中國)|0x0478|0x0409|Latin1_General_CI_AS|
|優魯巴文 (奈及利亞)|0x046a|0x0409|Latin1_General_CI_AS|
|祖魯文/祖魯文 (南非)|0x0435|0x0409|Latin1_General_CI_AS|

> [!NOTE]
> 您無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定期間選取僅限 Unicode 定序，因為系統不支援將它們當作伺服器層級定序。    
    
將定序指派給伺服器之後，除非匯出所有資料庫物件和資料，並重建 *master* 資料庫，然後匯入所有資料庫物件和資料，否則無法變更此定序。 若不變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序，您可以在建立新資料庫或資料庫資料行時，指定想要的定序。    

若要查詢 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的伺服器定序，請使用 `SERVERPROPERTY` 函式：

```sql
SELECT CONVERT(varchar, SERVERPROPERTY('collation'));
```

若要查詢伺服器的所有可用定序，請使用下列 `fn_helpcollations()` 內建函式：

```sql
SELECT * FROM sys.fn_helpcollations();
```
    
#### <a name="Database-level-collations"></a> 資料庫層級定序    
當建立資料庫時，您可以使用 `CREATE DATABASE` 的 `COLLATE` 子句或 `ALTER DATABASE` 陳述式來指定預設資料庫定序。 如果未指定定序，則會將伺服器定序指派給資料庫。    
    
除非變更伺服器的定序，否則無法變更系統資料庫的定序。
    
資料庫定序是用於資料庫中的所有中繼資料，且是資料庫中所使用全部字串資料行、暫存物件、變數名稱和任何其他字串的預設值。 請注意，如果變更使用者資料庫的定序，則在資料庫中的查詢存取暫存資料表時，可能會發生定序衝突。 暫存資料表一律儲存在 *tempdb* 系統資料庫中，以使用執行個體的定序。 如果定序導致評估字元資料發生衝突，則比較使用者資料庫與 *tempdb* 之間字元資料的查詢可能會失敗。 您可以在查詢中指定 `COLLATE` 子句以解決此問題。 如需詳細資訊，請參閱 [COLLATE (Transact-SQL)](~/t-sql/statements/collations.md)。    

> [!NOTE]
> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 上資料庫建立後，您就無法變更資料庫定序。

您可以使用類似下列 `ALTER DATABASE` 陳述式來變更使用者資料庫的定序：

```sql
ALTER DATABASE myDB COLLATE Greek_CS_AI;
```

> [!IMPORTANT]
> 改變資料庫層級定序不會影響資料行層級或運算式層級的定序。

您可以使用類似下列陳述式來擷取資料庫的目前定序：

```sql
SELECT CONVERT (VARCHAR(50), DATABASEPROPERTYEX('database_name','collation'));
```

#### <a name="Column-level-collations"></a> 資料行層級定序    
建立或改變資料表時，可以使用 `COLLATE` 子句來指定每個字元字串資料行的定序。 如果您沒有指定定序，就會將資料庫的預設定序指派給資料行。    

您可以使用類似下列 `ALTER TABLE` 陳述式來變更資料行的定序：

```sql
ALTER TABLE myTable ALTER COLUMN mycol NVARCHAR(10) COLLATE Greek_CS_AI;
```
    
#### <a name="Expression-level-collations"></a> 運算式層級定序    
運算式層級定序是在執行陳述式時設定的，而且它們會影響傳回結果集的方式。 這樣可讓 `ORDER BY` 將結果排序為地區設定特定。 若要執行運算式層級定序，請使用 `COLLATE` 子句，如下所示：    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> 地區設定    
地區設定是一組與某個地點或文化特性建立關聯的資訊。 這項資訊包括口語的名稱和識別碼、用來撰寫該語言的指令碼及文化習慣。 定序可與一個或多個地區設定產生關聯。 如需詳細資訊，請參閱 [Microsoft 指派的地區設定識別碼](https://msdn.microsoft.com/goglobal/bb964664.aspx)。    
    
###  <a name="Code_Page_Defn"></a> 字碼頁    
字碼頁是給定的指令碼的已排序字元集，其中每一個字元與數字索引或字碼指標值相關聯。 Windows 字碼頁一般稱為「字元集」  或 *charset*。 字碼頁是用來提供不同 Windows 系統地區設定所使用的字元集和鍵盤配置的支援。     
 
###  <a name="Sort_Order_Defn"></a> 排序次序    
排序次序會指定如何排序資料值。 次序會影響資料比較的結果。 資料是使用定序來排序，而且可以使用索引來最佳化。    
    
##  <a name="Unicode_Defn"></a> Unicode 支援    
Unicode 是將字碼指標對應到字元的標準用法。 由於 Unicode 主要設計為涵蓋世界上所有語言的字元，因此您不需要使用不同字碼頁來處理不同的字元集。

### <a name="unicode-basics"></a>Unicode 基本概念
若某個資料庫中以多種語言儲存資料，則當您只使用字元資料和字碼頁時會使得管理更加困難。 同時，也不容易針對可以儲存所有需要語言特定字元的資料庫尋找某個字碼頁。 此外，當以執行各種字碼頁的不同用戶端來讀取或更新特殊字元時，很難保證這些特殊字元能有正確的轉譯。 支援國際用戶端的資料庫應該一律使用 Unicode 資料類型，而不使用非 Unicode 資料類型。

例如，考慮必須處理三種主要語言的北美地區客戶資料庫：

-  墨西哥的西班牙文姓名與地址
-  魁北克的法文姓名與地址
-  加拿大其他地區與美國的英文姓名與地址

當只使用字元資料行與字碼頁時，您必須小心確定安裝資料庫時使用了可以處理這三種語言字元的字碼頁。 當執行另一種語言之字碼頁的用戶端讀取字元時，您也必須小心確保任何語言的字元都正確轉譯。
   
> [!NOTE]
> 用戶端所使用的字碼頁是由作業系統 (OS) 設定決定。 若要在 Windows XP 作業系統上設定用戶端字碼頁，請使用 [控制台] 中的 **[地區設定]** 。    

要對支援全球用戶需要的所有字元，選取字元資料類型的字碼頁則相當困難。 在國際資料庫中管理字元資料最簡單的方式，就是一律使用支援 Unicode 的資料類型。 

### <a name="unicode-data-types"></a>Unicode 資料類型
如果您將可反映多種語言的字元資料儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本)，則請使用 Unicode 資料類型 (**nchar**、**nvarchar** 和 **ntext**)，而非 Unicode 資料類型 (**char**、**varchar** 和 **text**)。 

> [!NOTE]
> 針對 Unicode 資料類型，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以使用 UCS-2 表示最多 65,535 個字元，或是在使用增補字元的情況下，使用完整的 Unicode 範圍 (1,114,111 個字元)。 如需啟用增補字元的詳細資訊，請參閱[增補字元](#Supplementary_Characters)。

或者，從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始，如果使用支援 UTF-8 的定序 (\_UTF8)，則先前非 Unicode 資料類型 (**char** 和 **varchar**) 會變成使用 UTF-8 編碼的 Unicode 資料類型。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 不會變更先前現有 Unicode 資料類型 (**Nchar**、**Nvarchar** 和 **Ntext**) 的行為，它們會繼續使用 UCS-2 或 UTF-16 編碼。 如需詳細資訊，請參閱 [UTF-8 和 UTF-16 間的儲存差異](#storage_differences)。

### <a name="unicode-considerations"></a>Unicode 考量事項
重要限制會與非 Unicode 資料類型相關聯。 這是因為非 Unicode 電腦受限於使用單一字碼頁。 透過使用 Unicode，您可能會發現效能獲得明顯改善，因為所需要的字碼頁轉換減少。 您必須在資料庫、資料行或運算式層級個別選取 Unicode 定序，因為伺服器層級不支援這些定序。    

當您將資料從伺服器移至用戶端時，舊版用戶端驅動程式可能無法辨識您的伺服器定序。 這種問題可能會發生在您將資料從 Unicode 伺服器移至非 Unicode 用戶端時。 此時，最佳選項可能就是升級用戶端作業系統，以便更新基礎系統定序。 如果用戶端已經安裝資料庫用戶端軟體，就可以考慮將服務更新套用至資料庫用戶端軟體。    
    
> [!TIP]
> 此外，您也可以嘗試針對伺服器上的資料使用不同的定序。 您可以選擇將對應至用戶端字碼頁的定序。    
>
> 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本) 中所提供 UTF-16 定序來改善部分 Unicode 字元的搜尋和排序 (僅限 Windows 定序)，您可以選取其中一個增補字元 (\_SC) 定序或其中一個版本 140 定序。    
 
若要使用 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 中提供的 UTF-8 定序，以及改善一些 Unicode 字元的排序和搜尋 (僅限 Windows 定序)，您必須選取啟用 UTF-8 編碼的定序 (\_UTF8)。
 
-   UTF8 旗標可套用至：    
    -   版本 90 定序 
        > [!NOTE]
        > 只有在增補字元 (\_SC) 或區分變化選取器 (\_VSS) 感知定序已存在於此版本時。
    -   版本 100 定序    
    -   版本 140 定序   
    -   BIN2<sup>1</sup> 二進位定序
    
-   UTF8 旗標無法套用至：    
    -   不支援增補字元 (\_SC) 或區分變化選取器 (\_VSS) 的 90 版定序    
    -   BIN 或 BIN2<sup>2</sup> 二進位定序    
    -   SQL\_* 定序  
    
<sup>1</sup> 從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 開始。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0 已將定序 **UTF8_BIN2** 替換成 **Latin1_General_100_BIN2_UTF8**。        
<sup>2</sup> 最高使用 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3。    
    
若要評估與使用 Unicode 或非 Unicode 資料類型有關的議題，請測試自己的狀況，在您的環境中衡量效能差異。 建議您將組織內系統上使用的定序標準化，並盡量部署 Unicode 伺服器和用戶端。    
    
在許多情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會與其他伺服器或用戶端互動，且您的組織可能會在應用程式與伺服器執行個體之間使用多重資料存取標準。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端是兩種主要類型中的其中一種：    
    
-   **Unicode 用戶端**，其使用 OLE DB 和開放式資料庫連接 (ODBC) 3.7 版或更新版本。    
-   **非 Unicode 用戶端**，其使用 DB-Library 和 ODBC 3.6 版或較舊版本。    
    
下表將提供搭配 Unicode 和非 Unicode 伺服器之不同組合來使用多國語言資料的相關資訊：    
    
|伺服器|Client|優點或限制|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|因為 Unicode 資料會在整個系統中使用，所以這個狀況可提供最佳效能，並防止所擷取的資料遭到損毀。 這是 ActiveX Data Objects (ADO)、OLE DB 和 ODBC 3.7 版或更新版本的情況。|    
|Unicode|非 Unicode|在此狀況中，特別是執行新版作業系統的伺服器與執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或在舊版作業系統上執行的用戶端之間存在連線，當您將資料移至用戶端電腦時，可能會有一些限制或錯誤。 伺服器上的 Unicode 資料會嘗試對應至非 Unicode 用戶端上的對應字碼頁，以便轉換資料。|    
|非 Unicode|Unicode|這不是使用多國語言資料的理想設定。 您無法將 Unicode 資料寫入非 Unicode 伺服器。 當資料傳送到在此伺服器的字碼頁以外的伺服器時，就可能發生問題。|    
|非 Unicode|非 Unicode|這是多國語言資料的限制狀況。 您只能使用單一字碼頁。|    
    
##  <a name="Supplementary_Characters"></a> 增補字元    
Unicode Consortium 會為每個字元配置唯一的字碼指碼，其值介於 000000 到 10FFFF 的範圍。 最常用的字元會具備介於 000000 到 00FFFF 範圍 (65,535 個字元) 內的字碼指碼值，其在記憶體和硬碟上可容於 8 位元或 16 位元的字組中。 此範圍通常會指定為基本多語系平面 (BMP)。 

但 Unicode Consortium 已建立其它 16 個字元「平面」，每個平面的大小都與 BMP 相同。 此定義可讓 Unicode 具備表示 1,114,112 個字元的潛力 (即 2<sup>16</sup> * 17 個字元)，介於字碼指碼範圍 000000 到 10FFFF 中。 字碼元素值大於 00FFFF 的字元需要二至四個連續的 8 位元字組 (UTF-8) 或兩個連續的 16 位元字組 (UTF-16)。 這些字元位於 BMP 範圍之外，稱為「增補字元」  的範圍內，並且額外的連續 8 位元或 16 位元字組稱為「代理字組」  。 如需增補字元、代理及代理字組的詳細資訊，請參閱 [Unicode Standard](http://www.unicode.org/standard/standard.html) (Unicode 標準)。    

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 **nchar** 和 **nvarchar** 等資料類型，用來儲存 BMP 範圍 (000000 到 00FFFF) 中的 Unicode 資料，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會使用 UCS-2 來進行編碼。 

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引進的全新系列增補字元 (\_SC) 定序可以與 **nchar**、**nvarchar** 和 **sql_variant** 資料類型搭配使用，以代表完整的 Unicode 字元範圍 (000000 到 10FFFF)。 例如：**Latin1_General_100_CI_AS_SC** 或 **Japanese_Bushu_Kakusu_100_CI_AS_SC** (如果使用日文定序的話)。 
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 會將增補字元支援延伸到具有新啟用 UTF-8 定序 ([\_UTF8](#utf8)) 的 **char** 和 **varchar** 資料類型。 這些資料類型也能夠代表完整的 Unicode 字元範圍。   

> [!NOTE]
> 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始，所有新的 \_140 定序都會自動支援增補字元。

如果您使用增補字元：    
    
-   增補字元可用於 90 (含) 以上定序版本的排序及比較作業。    
-   所有版本 100 定序都支援含有增補字元的語言排序。    
-   不支援在中繼資料內使用增補字元，例如資料庫物件的名稱。    
-   無法啟用搭配使用定序與增補字元 (\_SC) 的資料庫來進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。 這是因為針對複寫所建立的某些系統資料表和預存程序使用舊版 **ntext** 資料類型，其不支援增補字元。  

-   SC 旗標可套用至：    
    -   版本 90 定序    
    -   版本 100 定序    
    
-   SC 旗標無法套用至：    
    -   80 版本的非版本控制 Windows 定序    
    -   BIN 或 BIN2 二進位定序    
    -   SQL\* 定序    
    -   版本 140 定序 (這些定序已支援增補字元，因此不需要 SC 旗標)    
    
下表將比較當某些字串函式和字串運算子使用增補字元搭配或不搭配增補字元感知 (SCA) 定序時，這些函式和運算子的行為：    
    
|字串函數或運算子|搭配 SCA 定序|不搭配 SCA 定序|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|將 UTF-16 代理字組視為單一字碼指標。|將 UTF-16 代理字組視為兩個字碼指標。|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|這些函數會將每個 代理字組視為單一字碼指標，且如預期方式運作。|這些函數可能會將代理字組拆開並造成無法預期的結果。|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|傳回對應至所指定 Unicode 字碼指標值 (在範圍 0 到 0x10FFFF 中) 的字元。 如果所指定值位於 0 到 0xFFFF 的範圍內，即會傳回單一字元。 若為更高的值，則傳回對應的 Surrogate。|高於 0xFFFF 的值會傳回 NULL 而非對應的 Surrogate。|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|傳回 UTF-16 字碼指標 在範圍 0 到 0x10FFFF 中)。|傳回 UCS-2 字碼指標 (在範圍 0 到 0x10FFFF 中)。|    
|[符合單一萬用字元](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [萬用字元 - 不相符的字元](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|增補字元支援所有萬用字元作業。|增補字元不支援這些萬用字元作業。 但支援其他萬用字元運算子。|    
    
## <a name="GB18030"></a> GB18030 支援    
GB18030 是一種獨立標準，可供中華人民共和國進行中文字元的編碼。 在 GB18030 中，字元的長度可以是 1、2 或 4 個位元組。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可在 GB18030 編碼的字元從用戶端應用程式進入伺服器時加以辨識，並在轉換後以原生模式將其儲存為 Unicode 字元，藉以支援這種編碼的字元。 當 GB18030 編碼的字元儲存在伺服器後，任何後續作業都會將其視為 Unicode 字元。 

您可以使用任何中文定序，最好是使用最新的 100 版本。 所有 \_100 層級定序都支援含有 GB18030 字元的語言排序。 如果資料包含增補字元 (代理字組)，您就可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供的 SC 定序來改善搜尋和排序。    

> [!NOTE]
> 確認您的用戶端工具 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 使用 Dengxian 字型，以正確顯示包含 GB18030 編碼字元的字串。
    
## <a name="Complex_script"></a> 複雜字集支援    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以支援輸入、儲存、變更和顯示複雜字集。 複雜字集包括下列類型：    
    
-   包括由右至左和由左至右兩種文字之組合的字集，如阿拉伯文和英文文字的組合。    
-   字元的形狀會隨著位置或是否結合其他字元而不同的字集，例如，阿拉伯文、印度文和泰文字元。    
-   泰文之類的語言，因為單字之間不中斷，所以需要用內部字典來辨識單字。    
    
與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 互動的資料庫應用程式必須使用支援複雜字集的控制項。 受控碼中所建立標準 Windows Form 控制項具有複雜字集的功能。    

## <a name="Japanese_Collations"></a> 在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中新增的日文定序
 
從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，支援新的日文定序系列，可使用不同選項 (\_CS、\_AS、\_KS、\_WS 和 \_VSS) 的排列。 

若要列出這些定序，您可以查詢 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]：      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

所有新定序都內建增補字元支援，因此新的 **\_140** 定序都沒有 (都不需要) SC 旗標。

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 索引、記憶體最佳化資料表、資料行存放區索引和原生編譯的模組都支援這些定序。

<a name="ctp23"></a>

## <a name="utf8"></a> UTF-8 支援
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始完整支援將廣泛使用的 UTF-8 字元編碼作為匯入或匯出編碼，和作為字串資料的資料庫層級或資料行層級定序。 UTF-8 允許用於 **char** 和 **varchar** 資料類型，且會在您建立物件定序或將其變更為具有 *UTF8* 尾碼的定序時啟用。 例如，**LATIN1_GENERAL_100_CI_AS_SC**至 **LATIN1_GENERAL_100_CI_AS_SC_UTF8**。 

UTF-8 僅適用於支援增補字元的 Windows 定序，已於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中推出。 **nchar** 和 **nvarchar** 資料類型只允許 UCS-2 或 UTF-16 編碼，沒有產生任何變更。

### <a name="storage_differences"></a> UTF-8 和 UTF-16 間的儲存差異
Unicode Consortium 會為每個字元配置唯一的字碼指碼，其值介於 000000 到 10FFFF 的範圍。 透過 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]，UTF-8 和 UTF-16 編碼都能夠表示完整範圍：    
-  透過 UTF-8 編碼，ASCII 範圍 (000000–00007F) 中的字元需要 1 個位元組，字碼指碼 000080–0007FF 需要 2 個位元組，字碼指碼 000800–00FFFF 需要 3 個位元組，字碼指碼 0010000–0010FFFF 需要 4 個位元組。 
-  透過 UTF-16 編碼，字碼指碼 000000–00FFFF 需要 2 個位元組，字碼指碼 0010000–0010FFFF 需要 4 個位元組。 

下表列出每個字元範圍和編碼類型的編碼儲存體位元組：

|字碼範圍 (十六進位)|字碼範圍 (十進位)|使用 UTF-8 的儲存體位元組<sup>1</sup>|使用 UTF-16 的儲存體位元組<sup>1</sup>|    
|---------------------------------|---------------------------------|--------------------------|-----------------------------|   
|000000–00007F|0–127|1|2|
|000080–00009F<br />0000A0–0003FF<br />000400–0007FF|128–159<br />160–1,023<br />1,024–2,047|2|2|
|000800–003FFF<br />004000–00FFFF|2,048–16,383<br />16,384–65,535|3|2|
|010000–03FFFF<sup>2</sup><br /><br />040000–10FFFF<sup>2</sup>|65,536–262,143<sup>2</sup><br /><br />262,144–1,114,111<sup>2</sup>|4|4|

<sup>1</sup>「儲存體位元組」  意指編碼的位元組長度，而非資料類型在磁碟上的儲存大小。 如需磁碟上儲存大小的詳細資訊，請參閱 [nchar 與 nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 和 [char 與 varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)。

<sup>2</sup>[增補字元](#Supplementary_Characters)的字碼指碼範圍。

> [!TIP]   
> 一般認為在 [CHAR(*n*) 和 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) 中，或在 [NCHAR(*n*) 和 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 中，*n* 會定義字元數。 這是因為在 CHAR(10) 資料行的範例中，可以使用定序 (例如 **Latin1_General_100_CI_AI**) 來儲存範圍 0-127 中的 10 個 ASCII 字元，因為此範圍內的每個字元只會使用 1 個位元組。
>    
> 不過，在 [CHAR(*n*) 和 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) 中，*n* 會以「位元組」  為單位 (0-8,000) 來定義字串大小，且在 [NCHAR(*n*) 和 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 中，*n* 會以「位元組配對」  為單位 (0-4,000) 來定義字串大小。 *n* 一律不會定義可儲存的字元數。

如以上所見，取決於使用的字元集，選擇適當 Unicode 編碼和資料類型可能會節省大量儲存體或增加目前體存體使用量。 例如，使用啟用 UTF-8 的拉丁定序 (例如 **Latin1_General_100_CI_AI_SC_UTF8**) 時，`CHAR(10)` 資料行會儲存 10 個位元組，且可以保留範圍 0-127 內的 10 個 ASCII 字元。 但在範圍為 128-2047 時只能保留 5 個字元，而在範圍為 2048-65535 時只能保留 3 個字元。 相較之下，由於 `NCHAR(10)` 資料行會儲存 10 個位元組配對 (20 個位元組)，因此可以保留範圍 0-65535 內的 10 個字元。  

在您為資料庫或資料行選擇使用 UTF-8 或 UTF-16 編碼前，請考慮 要儲存之字串資料的分佈：
-  若大部分都在 ASCII 範圍 0-127 內 (例如英文)，則使用 UTF-8 時每個字元將需要 1 個位元組，UTF-16 則需要 2 個位元組。 使用 UTF-8 可提供儲存空間上的優勢。 將具有 ASCII 字元 (範圍 0-127) 的現有資料行資料類型從 `NCHAR(10)` 變更為 `CHAR(10)`，並使用啟用 UTF-8 的定序，會使儲存體需求減少 50%。 這項減少的原因是 `NCHAR(10)` 需要 20 個位元組作為儲存體，相較於 `CHAR(10)` 針對相同的 Unicode 字串表示只需要 10 個位元組。    
-  在 ASCII 的範圍之上，幾乎所有的拉丁語系字集，以及希臘文、斯拉夫、科普特文、亞美尼亞文、希伯來文、阿拉伯文、敘利亞文、它拿文和西非書面文字在 UTF-8 和 UTF-16 中每個字元都需要 2 個位元組。 在這些案例中，可比較的資料類型 (例如使用 **char** 或 **nchar**) 沒有明顯的儲存差異。
-  若其內容大部分是東亞字集 (例如韓文、中文和日文)，則在 UTF-8 中每個字元都需要 3 個位元組，UTF-16 中則為 2 個位元組。 使用 UTF-16 可提供儲存空間上的優勢。 
-  範圍 010000 至 10FFFF 的字元在 UTF-8 和 UTF-16 中都需要 4 個位元組。 在這些案例中，可比較的資料類型 (例如使用 **char** 或 **nchar**) 沒有儲存體差異。

針對其它考量事項，請參閱[撰寫國際 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)。

### <a name="converting"></a> 正在轉換為 UTF-8
因為在 [CHAR(*n*) 和 VARCHAR(*n*) 中](../../t-sql/data-types/char-and-varchar-transact-sql.md)，或在 [NCHAR(*n*) 和 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 中，*n* 定義的是儲存體位元組大小，而不是可儲存的字元數，因此請務必判斷您必須轉換成的資料類型大小，以避免資料截斷。 

例如，假設有一個資料行定義為 **NVARCHAR(100)** ，其中儲存 180 個位元組的日文字元。 在此範例中，資料行資料目前是使用 UCS-2 或 UTF-16 編碼，每個字元是使用 2 個位元組。 將資料行類型轉換成 **VARCHAR(200)** 不足以防止資料截斷，因為新的資料類型只能儲存 200 個位元組，但日文字元以 UTF-8 編碼時需要 3 個位元組。 因此，必須將資料行定義為 **VARCHAR(270)** 以避免資料因資料截斷而遺失。

因此，在將現有資料轉換為 UTF-8 之前，必須事先知道資料行定義的預估位元組大小，並據此調整新資料類型大小。 請參閱[資料範例 GitHub](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/unicode) \(英文\) 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼或 SQL Notebook，該範例使用 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 函數和 [COLLATE](../../t-sql/statements/collations.md) 陳述式，來判斷現有資料庫中 UTF-8 轉換作業的正確資料長度需求。

若要變更現有資料表中的資料行定序和資料類型，請使用[設定或變更資料行定序](../../relational-databases/collations/set-or-change-the-column-collation.md)中所述的其中一個方法。

若要變更資料庫定序，讓新物件根據預設繼承資料庫定序，或變更伺服器定序，讓新資料庫根據預設繼承系統定序，請參閱此文章的[相關工作](#Related_Tasks)一節。 

##  <a name="Related_Tasks"></a> Related tasks    
    
|Task|主題|    
|----------|-----------|    
|描述如何設定或變更 SQL Server 執行個體的定序。 請注意，變更伺服器定序並不會變更現有資料庫的定序。|[設定或變更伺服器定序](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|描述如何設定或變更使用者資料庫的定序。 請注意，變更資料庫定序並不會變更現有資料表資料行的定序。|[設定或變更資料庫定序](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|描述如何設定或變更資料庫中資料行的定序|[設定或變更資料行定序](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|描述如何傳回伺服器、資料庫或資料行層級的定序資訊|[檢視定序資訊](../../relational-databases/collations/view-collation-information.md)|    
|描述如何撰寫 Transact-SQL 陳述式，讓它們可以從某種語言攜至另一種語言，或更輕鬆地支援多種語言|[撰寫國際通用的 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|描述如何變更錯誤訊息的語言，以及日期、時間和貨幣資料的使用和顯示方式喜好設定|[設定工作階段語言](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Related content    
如需詳細資訊，請參閱下列相關內容：
* [SQL Server 最佳作法定序變更](https://go.microsoft.com/fwlink/?LinkId=113891)  
* [使用 Unicode 字元格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
* [撰寫國際通用的 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)  
* [SQL Server 最佳做法：移轉至 Unicode](https://go.microsoft.com/fwlink/?LinkId=113890) (不再維護)   
* [Unicode Consortium](https://go.microsoft.com/fwlink/?LinkId=48619)  
* [Unicode Standard](http://www.unicode.org/standard/standard.html) (Unicode 標準)  
* [OLE DB Driver for SQL Server 中的 UTF-8 支援](../../connect/oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
* [SQL Server 定序名稱 (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)  
* [Windows 定序名稱 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)  
* [介紹 SQL Server UTF-8 支援](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-UTF-8-support-for-SQL-Server/ba-p/734928)       
    
## <a name="see-also"></a>另請參閱    
[自主資料庫定序](../../relational-databases/databases/contained-database-collations.md)     
[選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)       
[單位元組和多位元組字元集](https://docs.microsoft.com/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)      
 
