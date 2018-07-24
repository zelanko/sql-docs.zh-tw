---
title: Windows 定序名稱 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1be59e84a5b40444e6218c2b390b832516193ecf
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982277"
---
# <a name="windows-collation-name-transact-sql"></a>Windows 定序名稱 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，指定 COLLATE 子句中的 Windows 定序名稱。 Windows 定序名稱是由定序指示項和比較樣式組成。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>引數  
 *CollationDesignator*  
 指定 Windows 定序所用的基底定序規則。 基底定序規則涵蓋下列項目：  
  
-   指定字典排序時，要套用的排序規則。 排序規則根據字母或語言而定。  
  
-   儲存非 Unicode 字元資料所用的字碼頁。  
  
 部份範例如下：  
  
-   Latin1_General 或 French：兩者都使用字碼頁 1252。  
  
-   Turkish：使用字碼頁 1254。  
  
 *CaseSensitivity*  
 **CI** 指定不區分大小寫，**CS** 指定區分大小寫。  
  
 *AccentSensitivity*  
 **AI** 指定不區分腔調字，**AS** 指定區分腔調字。  
  
 *KanatypeSensitive*  
 **Omitted** 指定不區分假名，**KS** 指定區分假名。  
  
 *WidthSensitivity*  
 **Omitted** 指定不區分全半形，**WS** 指定區分全半形。  
  
 **BIN**  
 指定要用的回溯相容性二進位排序次序。  
  
 **BIN2**  
 指定使用字碼指標比較語意的二進位排序順序。  
  
## <a name="remarks"></a>Remarks  
 視定序的版本不同，某些字碼指標可能未定義。 例如比較：  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 若定序為 Latin1_General_CI_AS，則第一行會傳回大寫字元，因為此定序中未定義此字碼指標。  
  
 使用某些語言時，避免使用較舊的定序很重要。 例如，對於 Telegu 就是如此。  
  
 在某些情況下，Windows 定序與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序對相同的查詢會產生不同的查詢計劃。  
  
## <a name="examples"></a>範例  
 以下是一些 Windows 定序名稱的範例：  
  
-   **Latin1_General_100_**  
  
 定序會使用 Latin1 General 字典排序規則，即字碼頁 1252。 不會區分大小寫，但是會區分腔調字。 定序會使用 Latin1 General 字典排序規則，而且對應至字碼頁 1252。 如果是 Windows 定序，便顯示此定序的版本號碼：_90 或 _100。 它不會區分大小寫 (CI)，但是會區分腔調字 (AS)。  
  
-   **Estonian_CS_AS**  
  
     定序會使用 Estonian 字典排序規則，即字碼頁 1257。 會區分大小寫也會區分腔調字。  
  
-   **Latin1_General_BIN**  
  
     定序使用字碼頁 1252 和二進位排序規則。 Latin1 一般字典排序規則會被忽略。  
  
## <a name="windows-collations"></a>Windows 定序  
 若要列出您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體支援的 Windows 定序，請執行下列查詢。  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 下表列出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援的所有 Windows 定序。  
  
|Windows 地區設定|定序版本 100|定序版本 90|  
|--------------------|---------------------------|--------------------------|  
|亞爾薩斯語 (法國)|Latin1_General_100_|無法使用|  
|阿姆哈拉文 (衣索比亞)|Latin1_General_100_|無法使用|  
|亞美尼亞文 (亞美尼亞)|Cyrillic_General_100_|無法使用|  
|阿薩姆文 (印度)|Assamese_100_ <sup>1</sup>|無法使用|  
|巴什喀爾文 (俄羅斯)|Bashkir_100_|無法使用|  
|巴斯克文 (巴斯克)|Latin1_General_100_|無法使用|  
|孟加拉文 (孟加拉)|Bengali_100_<sup>1</sup>|無法使用|  
|孟加拉文 (印度)|Bengali_100_<sup>1</sup>|無法使用|  
|波士尼亞文 (波士尼亞赫塞哥維納，斯拉夫)|Bosnian_Cyrillic_100_|無法使用|  
|波士尼亞文 (波士尼亞赫塞哥維納，拉丁)|Bosnian_Latin_100_|無法使用|  
|布里敦文 (法國)|Breton_100_|無法使用|  
|中文 (澳門特別行政區)|Chinese_Traditional_Pinyin_100_|無法使用|  
|中文 (澳門特別行政區)|Chinese_Traditional_Stroke_Order_100_|無法使用|  
|中文 (新加坡)|Chinese_Simplified_Stroke_Order_100_|無法使用|  
|科西嘉文 (法國)|Corsican_100_|無法使用|  
|克羅埃西亞文 (波士尼亞赫塞哥維納，拉丁)|Croatian_100_|無法使用|  
|達利語 (阿富汗)|Dari_100_|無法使用|  
|英文 (印度)|Latin1_General_100_|無法使用|  
|英文 (馬來西亞)|Latin1_General_100_|無法使用|  
|英文 (新加坡)|Latin1_General_100_|無法使用|  
|菲律賓文 (菲律賓)|Latin1_General_100_|無法使用|  
|夫里斯蘭文 (荷蘭)|Frisian_100_|無法使用|  
|喬治亞文 (喬治亞)|Cyrillic_General_100_|無法使用|  
|格陵蘭文 (格陵蘭)|Danish_Greenlandic_100_|無法使用|  
|古吉拉特文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|豪撒文 (奈及利亞，拉丁)|Latin1_General_100_|無法使用|  
|印度文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|伊布文 (奈及利亞)|Latin1_General_100_|無法使用|  
|依奴提圖特文 (加拿大，拉丁)|Latin1_General_100_|無法使用|  
|依奴提圖特文 (音節) 加拿大|Latin1_General_100_|無法使用|  
|愛爾蘭文 (愛爾蘭)|Latin1_General_100_|無法使用|  
|日文 (日本 XJIS)|Japanese_XJIS_100_|Japanese_90_、Japanese_|  
|日文 (日本)|Japanese_Bushu_Kakusu_100_|無法使用|  
|坎那達文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|高棉文 (柬埔寨)|Khmer_100_<sup>1</sup>|無法使用|  
|基切語 (瓜地馬拉)|Modern_Spanish_100_|無法使用|  
|金揚萬答文 (盧安達)|Latin1_General_100_|無法使用|  
|貢根文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|寮文 (寮國人民共合國)|Lao_100_<sup>1</sup>|無法使用|  
|下索布語 (德國)|Latin1_General_100_|無法使用|  
|盧森堡文 (盧森堡)|Latin1_General_100_|無法使用|  
|馬來亞拉姆文 (印度)|Indic_General_100_<sup>1</sup>|無法使用|  
|馬爾他文 (馬爾他)|Maltese_100_|無法使用|  
|毛利文 (紐西蘭)|Maori_100_|無法使用|  
|馬普切文 (智利)|Mapudungan_100_|無法使用|  
|馬拉提文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|莫霍克文 (加拿大)|Mohawk_100_|無法使用|  
|蒙古文 (中國)|Cyrillic_General_100_|無法使用|  
|尼泊爾文 (尼泊爾)|Nepali_100_<sup>1</sup>|無法使用|  
|挪威文 (巴克摩，挪威)|Norwegian_100_|無法使用|  
|挪威文 (耐諾斯克，挪威)|Norwegian_100_|無法使用|  
|奧西坦文 (法國)|French_100_|無法使用|  
|歐利亞文 (印度)|Indic_General_100_<sup>1</sup>|無法使用|  
|普什圖文 (阿富汗)|Pashto_100_<sup>1</sup>|無法使用|  
|波斯文 (伊朗)|Persian_100_|無法使用|  
|旁遮普語 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|蓋楚瓦文 (玻利維亞)|Latin1_General_100_|無法使用|  
|蓋楚瓦文 (厄瓜多)|Latin1_General_100_|無法使用|  
|蓋楚瓦文 (秘魯)|Latin1_General_100_|無法使用|  
|羅曼斯文 (瑞士)|Romansh_100_|無法使用|  
|沙米文 (伊納立，芬蘭)|Sami_Sweden_Finland_100_|無法使用|  
|沙米文 (盧勒，挪威)|Sami_Norway_100_|無法使用|  
|沙米文 (盧勒，瑞典)|Sami_Sweden_Finland_100_|無法使用|  
|沙米文 (北，芬蘭)|Sami_Sweden_Finland_100_|無法使用|  
|沙米文 (北，挪威)|Sami_Norway_100_|無法使用|  
|沙米文 (北，瑞典)|Sami_Sweden_Finland_100_|無法使用|  
|沙米文 (斯科特，芬蘭)|Sami_Sweden_Finland_100_|無法使用|  
|沙米文 (南，挪威)|Sami_Norway_100_|無法使用|  
|沙米文 (南，瑞典)|Sami_Sweden_Finland_100_|無法使用|  
|梵文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|塞爾維亞文 (波士尼亞赫塞哥維納，斯拉夫)|Serbian_Cyrillic_100_|無法使用|  
|塞爾維亞文 (波士尼亞赫塞哥維納，拉丁)|Serbian_Latin_100_|無法使用|  
|塞爾維亞文 (塞爾維亞，斯拉夫)|Serbian_Cyrillic_100_|無法使用|  
|塞爾維亞文 (塞爾維亞，拉丁)|Serbian_Latin_100_|無法使用|  
|賴索托文/北索托文 (南非)|Latin1_General_100_|無法使用|  
|塞茲瓦納文/班圖文 (南非)|Latin1_General_100_|無法使用|  
|僧伽羅語 (斯里蘭卡)|Indic_General_100_<sup>1</sup>|無法使用|  
|斯瓦希里文 (肯亞)|Latin1_General_100_|無法使用|  
|敘利亞文 (敘利亞)|Syriac_100_<sup>1</sup>|Syriac_90_|  
|塔吉克文 (塔吉克)|Cyrillic_General_100_|無法使用|  
|塔馬塞特文 (阿爾及利亞，拉丁)|Tamazight_100_|無法使用|  
|坦米爾文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|特拉古文 (印度)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|藏文 (中國)|Tibetan_100_<sup>1</sup>|無法使用|  
|土庫曼文 (土庫曼)|Turkmen_100_|無法使用|  
|維吾爾文 (中國)|Uighur_100_|無法使用|  
|上索布語 (德國)|Upper_Sorbian_100_|無法使用|  
|烏都文 (巴基斯坦)|Urdu_100_|無法使用|  
|威爾斯文 (英國)|Welsh_100_|無法使用|  
|沃洛夫文 (塞內加爾)|French_100_|無法使用|  
|科薩文/科薩文 (南非)|Latin1_General_100_|無法使用|  
|雅庫特語 (俄羅斯)|Yakut_100_|無法使用|  
|爨文 (中國)|Latin1_General_100_|無法使用|  
|優魯巴文 (奈及利亞)|Latin1_General_100_|無法使用|  
|祖魯文/祖魯文 (南非)|Latin1_General_100_|無法使用|  
|已被取代，無法用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器層級|Hindi|Hindi|  
|已被取代，無法用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器層級|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|已被取代，無法用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器層級|Lithuanian_Classic|Lithuanian_Classic|  
|已被取代，無法用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本的伺服器層級|Macedonian|Macedonian|  
  
 <sup>1</sup>僅限 Unicode 的 Windows 定序只能套用至資料行層級或運算式層級的資料。 它們無法當做伺服器或資料庫定序使用。  
  
 <sup>2</sup>中文 (澳門) 與中文 (台灣) 定序相同之處在於兩者都使用簡體中文的規則；中文 (澳門) 與中文 (台灣) 不同之處則在於前者使用字碼頁 950。  
  
## <a name="see-also"></a>另請參閱  
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [常數 &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
