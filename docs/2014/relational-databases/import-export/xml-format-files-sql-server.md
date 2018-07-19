---
title: XML 格式檔案 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], XML format files
- bulk importing [SQL Server], format files
- XML format files [SQL Server]
ms.assetid: 69024aad-eeea-4187-8fea-b49bc2359849
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06ba4a93e79d9b2a602101b25944d251ea9c5b54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203548"
---
# <a name="xml-format-files-sql-server"></a>XML 格式檔案 (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供 XML 結構描述，以定義撰寫 *「XML 格式檔案」* (XML format file) 用於將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的語法。 XML 格式檔案必須遵守以 XML 結構描述定義語言 (XSDL) 定義的這個結構描述。 只有在同時安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 時，才能支援 XML 格式檔案。  
  
 您可以搭配使用 XML 格式檔案與 **bcp**命令、BULK INSERT 陳述式或 INSERT ...SELECT \* FROM OPENROWSET(BULK...) 陳述式。 **bcp** 命令可讓您自動產生資料表的 XML 格式檔案；如需詳細資訊，請參閱＜ [bcp Utility](../../tools/bcp-utility.md)＞。  
  
> [!NOTE]  
>  有兩種類型的格式檔案支援大量匯出和匯入：「非 XML 格式檔案」和「XML 格式檔案」。 相較於非 XML 格式檔案而言，XML 格式檔案是較彈性且功能強大的替代方案。 如需非 XML 格式檔案的相關資訊，請參閱 [非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)＞。  
  

  
##  <a name="BenefitsOfXmlFFs"></a> XML 格式檔案的優點  
  
-   XML 格式檔案具有自我描述能力，使其易於讀取、建立和擴充。 XML 格式檔案容易讀懂，以便輕鬆地了解在大量作業期間如何解譯資料。  
  
-   XML 格式檔案包含目標資料行的資料類型。  XML 編碼清楚描述資料檔的資料類型和資料元素，以及資料元素和資料表資料行之間的對應關係。  
  
     如此可將資料檔呈現資料的方式，與檔案中每一個欄位和資料類型間的關係，予以區隔開來。 例如，資料檔若包含資料的字元表示法，就會遺失對應的 SQL 資料行類型。  
  
-   XML 格式檔案允許從資料檔載入包含單一大型物件 (LOB) 資料類型的欄位。  
  
-   XML 格式檔案雖然功能增強，但仍保持與其舊版的相容性。 此外，XML 清楚的編碼方式，有利於建立所指定的資料檔的多個格式檔案。 如果您需要將資料欄位的全部或部分對應到不同資料表或檢視表中的資料行，這會很有用。  
  
-   XML 語法與作業方向無關；也就是說，大量匯出和大量匯入作業的語法相同。  
  
-   您可以使用 XML 格式檔案，大量匯入資料至資料表或非資料分割檢視中及大量匯出資料。  
  
-   針對 OPENROWSET(BULK...) 函數，指定目標資料表是選擇性的。 原因是函數依賴 XML 格式檔案，才能從資料檔讀取資料。  
  
    > [!NOTE]  
    >  使用 **bcp** 命令和 BULK INSERT 陳述式 (使用目標資料表資料行來執行類型轉換)，需要目標資料表。  
  
##  <a name="StructureOfXmlFFs"></a> XML 格式檔案的結構  
 就像非 XML 格式檔案一樣，XML 格式檔案也定義資料檔中資料欄位的格式和結構，並將那些資料欄位對應到單一目標資料表中的資料行。  
  
 XML 格式檔案擁有兩個主要元件：\<記錄> 和 \<資料列>：  
  
-   \<記錄> 描述儲存在資料檔案中的資料。  
  
     每個 \<記錄> 項目包含一或多個 \<欄位> 項目組成的集合。 這些元素對應到資料檔案中的欄位。 基本語法如下：  
  
     \<記錄>  
  
     \<欄位 .../> [ ...*n* ]  
  
     \</記錄>  
  
     每一個 \<欄位> 項目描述特定資料欄位的內容。 一個欄位只能對應到資料表的一個資料行。 並非所有欄位都需要對應到資料行。  
  
     資料檔中的欄位可以是固定/可變長度或以字元終止。 「欄位值」可以如此表示：一個字元 (使用單一位元組表示法)、一個寬字元 (使用 Unicode 雙位元組表示法)、原生資料庫格式或一個檔案名稱。 如果欄位值是以檔案名稱表示，則檔案名稱指向包含目標資料表中 BLOB 資料行的值的檔案。  
  
-   \<資料列> 描述當資料檔案中的資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的語法。  
  
     \<資料列> 項目包含一組 \<資料行> 項目。 這些元素對應到資料表資料行。 基本語法如下：  
  
     \<資料列>  
  
     \<資料行 .../> [ ...*n* ]  
  
     \</資料列>  
  
     每個 \<資料行> 項目都只能對應至資料檔案中的一個欄位。 \<ROW> 元素中的 \<COLUMN> 元素順序會定義大量作業傳回這些元素的順序。 XML 格式檔案會將本機名稱指派給每個 \<COLUMN> 元素，而此名稱與大量匯入作業之目標資料表中的資料行沒有任何關聯性。  
  
##  <a name="SchemaSyntax"></a> XML 格式檔案的結構描述語法  
 本節包含 XML 格式檔案之 XML 結構描述的元素和屬性摘要。 格式檔案的語法與作業方向無關；也就是說，不管是大量匯出還是大量匯入作業，語法都相同。 本節也探討大量匯入如何使用 \<資料列> 與 \<資料行> 項目，以及如何將項目的 xsi:type 值放入資料集中。  
  
 若要了解語法如何對應到實際 XML 格式檔案，請參閱本主題後面的 [範例 XML 格式檔案](#SampleXmlFFs)。  
  
> [!NOTE]  
>  您可以修改格式檔案，讓您從欄位數目及/或順序與資料表資料行數目及/或順序不同的資料檔案，進行大量匯入。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
  
  
###  <a name="BasicSyntax"></a> XML 結構描述的基本語法  
 此語法陳述式只會顯示項目 (\<BCP 格式>、\<錄>、\<欄位>、\<資料行> 和 \<資料行>) 及其基本屬性。  
  
 \<BCP 格式 ...>  
  
 \<記錄>  
  
 \<欄位識別碼 = "*fieldID*" xsi:type = "*fieldType*" [...]  
  
 />  
  
 \</記錄>  
  
 \<資料列>  
  
 \<資料行來源 = "*fieldID*" NAME = "*columnName*" xsi:type = "*columnType*" [...]  
  
 />  
  
 \</資料列>  
  
 \</BCP 格式>  
  
> [!NOTE]  
>  本主題稍後將會描述與 \<欄位> 或 \<> 項目中的 xsi:type 值相關聯的其他屬性。  
  

  
####  <a name="SchemaElements"></a> Schema 元素  
 本節摘要說明 XML 結構描述為 XML 格式檔案定義之每個元素的目的。 稍後會在此主題另一節說明屬性。  
  
 \<BCP 格式>  
 格式檔案元素，它定義所指定資料檔的記錄結構，以及它和資料表中資料表資料列的資料行之對應關係。  
  
 \<記錄 .../>  
 定義包含一或多個 \<欄位> 項目的複雜項目。 格式檔案中欄位的宣告順序是欄位出現在資料檔中的順序。  
  
 \<欄位 .../>  
 定義資料檔中包含資料的欄位。  
  
 這個項目的屬性將在本主題稍後的 [\<欄位> 項目的屬性](#AttrOfFieldElement)中加以討論。  
  
 \<資料列 .../>  
 定義包含一或多個 \<資料行> 項目的複雜項目。 \<資料行> 項目的順序與 RECORD 定義中的 \<欄位> 項目順序無關。 相反的，格式檔案中的 \<資料行> 項目順序會決定結果資料列集中的資料行順序。 資料欄位會以對應的 \<資料行> 項目在 \<資料行> 項目中宣告的順序載入。  
  
 如需詳細資訊，請參閱本主題稍後的[大量匯入如何使用 \<資料列> 項目](#HowUsesROW)。  
  
 \<資料行>  
 定義資料行作為項目 (\<資料行>)。 每個 \<COLUMN> 元素都會對應到 \<FIELD> 元素 (其識別碼是在 \<COLUMN> 元素的 SOURCE 屬性中指定)。  
  
 這個項目的屬性將在本主題稍後的 [\<資料行> 項目的屬性](#AttrOfColumnElement)中加以討論。 另請參閱本主題稍後的[大量匯入如何使用 \<資料行> 項目](#HowUsesColumn)。  
  
 \</BCP 格式>  
 結束格式檔案時需要用到。  
  
####  <a name="AttrOfFieldElement"></a> \<欄位> 項目的屬性  
 本節描述 \<欄位> 項目的屬性，這些屬性會摘要在下列的結構描述語法中：  
  
 <FIELD  
  
 ID **="*`fieldID`*"**  
  
 xsi **:** 型別 **="*`fieldType`*"**  
  
 [ LENGTH **="*`n`*"** ]  
  
 [PREFIX_LENGTH **="*`p`*"** ]  
  
 [MAX_LENGTH **="*`m`*"** ]  
  
 [定序 **="*`collationName`*"** ]  
  
 [結束字元 **="*`terminator`*"** ]  
  
 />  
  
 每個 \<欄位> 項目都與其他項目無關。 以下透過屬性來說明欄位：  
  
|FIELD 屬性|說明|選擇性 /<br /><br /> 必要項|  
|---------------------|-----------------|------------------------------|  
|ID **="*`fieldID`*"**|指定資料檔中欄位的邏輯名稱。 欄位識別碼是用來參考該欄位的索引鍵。<br /><br /> < 欄位 ID **="*`fieldID`*」**/ > 對應至 < 資料行來源 **="*`fieldID`*"**/>|必要項|  
|xsi: type **="*`fieldType`*"**|這是識別元素執行個體之類型的 XML 建構 (如同屬性般使用)。 *fieldType* 的值會決定在指定執行個體中需要哪些選用屬性 (如下)。|必要 (視資料類型而定)|  
|LENGTH **="*`n`*"**|此屬性定義固定長度資料類型的執行個體之長度。<br /><br /> *n* 的值必須為正整數。|除非 xsi:type 值有要求，否則是選擇性的|  
|PREFIX_LENGTH **="*`p`*"**|此屬性定義二進位資料代表的前置長度。 PREFIX_LENGTH 值 *p*必須是下列其中一個：1、2、4 或 8。|除非 xsi:type 值有要求，否則是選擇性的|  
|MAX_LENGTH **="*`m`*"**|此屬性是可儲存在給定欄位中的最大位元組數。 若沒有目標資料表，則無法取得資料行最大長度。 MAX_LENGTH 屬性會限制輸出字元資料行的最大長度，因而限制為資料行值配置的儲存區。 在 ELECT FROM 子句中使用 OPENROWSET 函數的 BULK 選項時，這樣做特別方便。<br /><br /> *m* 的值必須為正整數。 根據預設， **char** 資料行的最大長度是 8000 個字元，而 **nchar** 資料行的最大長度是 4000 個字元。|選擇性|  
|定序 **="*`collationName`*"**|COLLATION 只能用於字元欄位。 如需 SQL 定序名稱的清單，請參閱 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)。|選擇性|  
|結束字元 **="*`terminator`*"**|此屬性會指定資料欄位的結束字元。 結束字元可以是任何字元。 結束字元必須是不包含於資料之任何部分的唯一字元。<br /><br /> 根據預設，欄位結束字元是定位字元 (以 \t 表示)。 若要表示段落標記，請使用 \r\n。|只能搭配字元資料的 xsi:type 使用，字元資料需要此屬性。|  
  
#####  <a name="XsiTypeValuesOfFIELD"></a> \<欄位> 項目的 xsi:type 值  
 xsi:type 值是識別元素執行個體之資料類型的 XML 建構 (如同屬性般使用)。 如需有關使用「將 xsi:type 值放入資料集」的資訊，請參閱本節稍後的部分。  
  
 \<欄位> 項目的 xsi:type 值支援下列資料類型。  
  
|\<欄位> xsi:type 值|必要的 XML 屬性<br /><br /> 適用於資料類型|選擇性 XML 屬性<br /><br /> 適用於資料類型|  
|-------------------------------|---------------------------------------------------|---------------------------------------------------|  
|**NativeFixed**|`LENGTH`|無。|  
|**NativePrefix**|`PREFIX_LENGTH`|MAX_LENGTH|  
|**CharFixed**|`LENGTH`|COLLATION|  
|**NCharFixed**|`LENGTH`|COLLATION|  
|**CharPrefix**|`PREFIX_LENGTH`|MAX_LENGTH、COLLATION|  
|**NCharPrefix**|`PREFIX_LENGTH`|MAX_LENGTH、COLLATION|  
|**CharTerm**|`TERMINATOR`|MAX_LENGTH、COLLATION|  
|**NCharTerm**|`TERMINATOR`|MAX_LENGTH、COLLATION|  
  
 如需 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)＞。  
  
####  <a name="AttrOfColumnElement"></a> \<資料行> 項目的屬性  
 本節描述 \<資料行> 項目的屬性，這些屬性會摘要在下列的結構描述語法中：  
  
 \<元素的 xsi:type 值  
  
 SOURCE = "*fieldID*"  
  
 NAME = "*columnName*"  
  
 xsi:type = "*columnType*"  
  
 [ LENGTH = "*n*" ]  
  
 [ PRECISION = "*n*" ]  
  
 [ SCALE = "*value*" ]  
  
 [ NULLABLE = { "YES"  
  
 "NO" } ]  
  
 />  
  
 欄位會使用下列屬性對應到目標資料表的資料行：  
  
|COLUMN 屬性|描述|選擇性 /<br /><br /> 必要項|  
|----------------------|-----------------|------------------------------|  
|來源 **="*`fieldID`*"**|指定對應到資料行的欄位識別碼。<br /><br /> < 資料行來源 **="*`fieldID`*」**/ > 對應至 < 欄位 ID **="*`fieldID`*"**/>|必要項|  
|NAME = "*columnName*"|指定資料列集中由格式檔案代表的資料行名稱。 此資料行名稱會用來識別結果集中的資料行，而且它不需要對應到用於目標資料表中的資料行名稱。|必要項|  
|xsi **:** 型別 **="*`ColumnType`*"**|這是識別元素執行個體之資料類型的 XML 建構 (如同屬性般使用)。 *ColumnType* 的值會決定在指定執行個體中需要哪些選用屬性 (如下)。<br /><br /> 注意： 可能的值*ColumnType*和其相關聯的屬性詳列於下一個表格。|選擇性|  
|LENGTH **="*`n`*"**|定義固定長度資料類型的長度。 只有當 xsi:type 是字串資料類型時，才會使用 LENGTH。<br /><br /> *n* 的值必須為正整數。|選用 (只在 xsi:type 是字串資料類型時才可使用)|  
|PRECISION **="*`n`*"**|指定數字中的位數。 例如，數字 123.45 的精確度是 5。<br /><br /> 其值必須為正整數。|選擇性 (唯有 xsi:type 是變數數字 (variable-number) 資料類型時才能使用)|  
|縮放比例 **="*`int`*"**|指定數字中小數點右方的位數。 例如，數字 123.45 的小數位數是 2。<br /><br /> 值必須是整數。|選擇性 (唯有 xsi:type 是變數數字 (variable-number) 資料類型時才能使用)|  
|NULLABLE **=** { **"** YES **"**<br /><br /> **"** NO **"** }|指定資料行是否可指定 NULL 值。 此屬性完全與 FIELDS 無關。 然而，若資料行並非 NULLABLE 且欄位指定 NULL (未指定任何值)，則會導致執行階段錯誤。<br /><br /> 只有當您執行一般的 SELECT FROM OPENROWSET(BULK...) 陳述式時，才會使用 NULLABLE 屬性。|選用 (可用於任何資料類型)|  
  
#####  <a name="XsiTypeValuesOfCOLUMN"></a> \<資料行> 項目的 xsi:type 值  
 xsi:type 值是識別元素執行個體之資料類型的 XML 建構 (如同屬性般使用)。 如需有關使用「將 xsi:type 值放入資料集」的資訊，請參閱本節稍後的部分。  
  
 \<資料行> 項目支援原生 SQL 資料類型，如下所示：  
  
|類型類別目錄|\<資料行> 資料類型|必要的 XML 屬性<br /><br /> 適用於資料類型|選擇性 XML 屬性<br /><br /> 適用於資料類型|  
|-------------------|---------------------------|---------------------------------------------------|---------------------------------------------------|  
|固定|`SQLBIT``SQLTINYINT`， `SQLSMALLINT`， `SQLINT`， `SQLBIGINT`， `SQLFLT4`， `SQLFLT8`， `SQLDATETIME`， `SQLDATETIM4`， `SQLDATETIM8`， `SQLMONEY`， `SQLMONEY4`， `SQLVARIANT`，及 `SQLUNIQUEID`|無。|NULLABLE|  
|變數數字|`SQLDECIMAL` 和 `SQLNUMERIC`|無。|NULLABLE、PRECISION、SCALE|  
|LOB|`SQLIMAGE`、`CharLOB`、`SQLTEXT` 和 `SQLUDT`|無。|NULLABLE|  
|字元 LOB|`SQLNTEXT`|無。|NULLABLE|  
|二進位字串|`SQLBINARY` 和 `SQLVARYBIN`|無。|NULLABLE、LENGTH|  
|字元字串|`SQLCHAR`、`SQLVARYCHAR`、`SQLNCHAR` 和 `SQLNVARCHAR`|無。|NULLABLE、LENGTH|  
  
> [!IMPORTANT]  
>  若要大量匯出或匯入 SQLXML 資料，請在格式檔案中使用下列資料類型：SQLCHAR 或 SQLVARYCHAR (資料會以用戶端字碼頁或定序所隱含的字碼頁傳送)、SQLNCHAR、SQLNVARCHAR (資料會以 Unicode 傳送)、SQLBINARY 或 SQLVARYBIN (資料不經轉換即傳送)。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)＞。  
  
###  <a name="HowUsesROW"></a> 大量匯入如何使用 \<資料列> 項目  
 某些內容會略過 \<資料列> 項目。 \<資料列> 項目是否會影響大量匯入作業，視作業執行方式而定：  
  
-   **bcp** 命令  
  
     將資料載入目標資料表時，**P** 會略過 \<資料列> 元件。 相反地， **bcp** 會根據目標資料表的資料行類型來載入資料。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式 (BULK INSERT 和 OPENROWSET 的 Bulk 資料列集提供者)  
  
     大量匯入資料到資料表時，[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會使用 \<資料列> 元件來產生輸入資料列集。 此外，[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會根據在目標資料表中 \<資料列> 與對應資料行中指定的資料行類型，執行適當的類型轉換。 若格式檔案中指定的資料行類型與目標資料表不同，會發生額外的類型轉換。 此額外類型轉換可能會導致 BULK INSERT 或 OPENROWSET 的 Bulk 資料列集提供者發生某些不一致 (亦即，遺失精確度) 的行為 (與 **bcp**相較)。  
  
     \<資料列> 項目中的資訊可讓您建構資料列，而不需要任何額外資訊。 因此，您可以使用 SELECT 陳述式 (SELECT \* FROM OPENROWSET(BULK *datafile* FORMATFILE=*xmlformatfile*) 來產生資料列集。  
  
    > [!NOTE]  
    >  OPENROWSET BULK 子句需要格式檔案 (請注意，要有 XML 格式檔案才能將欄位的資料類型轉換為資料行的資料類型)。  
  
###  <a name="HowUsesColumn"></a> 大量匯入如何使用 \<資料行> 項目  
 若要大量匯入資料至資料表中，格式檔案中的 \<資料行> 項目會藉由指定下列各項，將資料檔案欄位對應到資料表資料行：  
  
-   資料檔的資料列中每一個欄位的位置。  
  
-   資料行類型，用來將欄位資料類型轉換成所要的資料行資料類型。  
  
 若沒有任何資料行對應到欄位，則該欄位不會被複製到產生的資料列。 此行為可讓資料檔產生具有不同資料行的資料列 (在不同的資料表中)。  
  
 同樣地，從資料表大量匯出資料時，格式檔案中的每一個 \<資料行> 會將輸入資料表資料列中的資料行對應到輸出資料檔案中的對應欄位。  
  
###  <a name="PutXsiTypeValueIntoDataSet"></a> 將 xsi:type 值放到資料集中  
 當您使用 XML Schema Definition (XSD) 語言來驗證 XML 文件時，xsi:type 值不會放到資料集中。 然而，您可以透過將 XML 格式檔案載入到 XML 文件 (例如： `myDoc`)，來將 xsi:type 資訊放到資料集中，如以下程式碼片段所示：  
  
```  
...;  
myDoc.LoadXml(xmlFormat);  
XmlNodeList ColumnList = myDoc.GetElementsByTagName("COLUMN");  
for(int i=0;i<ColumnList.Count;i++)  
{  
   Console.Write("COLUMN: xsi:type=" +ColumnList[i].Attributes["type",  
      "http://www.w3.org/2001/XMLSchema-instance"].Value+"\n");  
}  
```  
  
##  <a name="SampleXmlFFs"></a> 範例 XML 格式檔案  
 本節包含有關在各種情況下使用 XML 格式檔案的詳細資訊，包括 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 範例。  
  
> [!NOTE]  
>  在下列範例顯示的資料檔中， `<tab>` 表示資料檔中的定位字元， `<return>` 則表示歸位字元。  
  

  
> [!NOTE]  
>  如需如何建立格式檔案的相關資訊，請參閱 [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)＞。  
  
###  <a name="OrderCharFieldsSameAsCols"></a> A. 以與資料表資料行相同的方式排序字元資料欄位  
 下列範例顯示 XML 格式檔案，其中描述包含三個字元資料欄位的資料檔。 格式檔案將資料檔對應到包含三個資料行的資料表。 資料欄位是以一對一的方式，來對應資料表的資料行。  
  
 **Table (row):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **Data file (record):** Age\<tab>Firstname\<tab>Lastname\<return>  
  
 下列 XML 格式檔案會將資料檔中的資料讀入資料表。  
  
 在 `<RECORD>` 元素中，格式檔案是以字元資料來表示這三個欄位內的資料值。 每一個欄位的 `TERMINATOR` 屬性，都會指出跟在資料值後面的結束字元。  
  
 資料欄位是以一對一的方式，來對應資料表的資料行。 在 `<ROW>` 元素中，格式檔案會將資料行 `Age` 對應到第一個欄位、資料行 `FirstName` 對應到第二個欄位，以及資料行 `LastName` 對應到第三個欄位。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>   
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="2" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="3" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  如需參考相等的 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 範例，請參閱 [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)＞。  
  
###  <a name="OrderFieldsAndColsDifferently"></a> B. 以不同的方式排序資料欄位與資料表資料行  
 下列範例顯示 XML 格式檔案，其中描述包含三個字元資料欄位的資料檔。 格式檔案會將資料檔對應到包含三個資料行 (排序方式與資料檔的欄位不同) 的資料表。  
  
 **Table (row):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **Data file** (record): Age\<tab>Lastname\<tab>Firstname\<return>  
  
 在 `<RECORD>` 元素中，格式檔案是以字元資料來表示這三個欄位內的資料值。  
  
 在 `<ROW>` 元素中，格式檔案會將資料行 `Age` 對應到第一個欄位、資料行 `FirstName` 對應到第三個欄位，以及資料行 `LastName` 對應到第二個欄位。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="2" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  如需參考相等的 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 範例，請參閱[使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)。  
  
### <a name="c-omitting-a-data-field"></a>C. 省略資料欄位  
 下列範例顯示 XML 格式檔案，其中描述包含四個字元資料欄位的資料檔。 格式檔案將資料檔對應到包含三個資料行的資料表。 第二個資料欄位不對應到任何資料表資料行。  
  
 **Table (row):** Person (Age int, FirstName Varchar(20), LastName Varchar(30))  
  
 **Data file (record):** Age\<tab>employeeID\<tab>Firstname\<tab>Lastname\<return>  
  
 在 `<RECORD>` 元素中，格式檔案是以字元資料來表示這四個欄位內的資料值。 每一個欄位的 TERMINATOR 屬性，都會指出跟在資料值後面的結束字元。  
  
 在 `<ROW>` 元素中，格式檔案會將資料行 `Age` 對應到第一個欄位、資料行 `FirstName` 對應到第三個欄位，以及資料行 `LastName` 對應到第四個欄位。  
  
```  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="10"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="4" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  如需參考相等的 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 範例，請參閱 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)＞。  
  
###  <a name="MapXSItype"></a> D. 將 \<欄位> xsi:type 對應到 \<資料行> xsi:type  
 下列範例顯示不同類型的欄位，以及它們與資料行的對應關係。  
  
```  
<?xml version = "1.0"?>  
<BCPFORMAT  
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <RECORD>  
      <FIELD xsi:type="CharTerm" ID="C1" TERMINATOR="\t"   
            MAX_LENGTH="4"/>  
      <FIELD xsi:type="CharFixed" ID="C2" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="CharPrefix" ID="C3" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharTerm" ID="C4" TERMINATOR="\t"   
         MAX_LENGTH="4"/>  
      <FIELD xsi:type="NCharFixed" ID="C5" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharPrefix" ID="C6" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NativeFixed" ID="C7" LENGTH="4"/>  
   </RECORD>  
   <ROW>  
      <COLUMN SOURCE="C1" NAME="Age" xsi:type="SQLTINYINT"/>  
      <COLUMN SOURCE="C2" NAME="FirstName" xsi:type="SQLVARYCHAR"   
      LENGTH="16" NULLABLE="NO"/>  
      <COLUMN SOURCE="C3" NAME="LastName" />  
      <COLUMN SOURCE="C4" NAME="Salary" xsi:type="SQLMONEY"/>  
      <COLUMN SOURCE="C5" NAME="Picture" xsi:type="SQLIMAGE"/>  
      <COLUMN SOURCE="C6" NAME="Bio" xsi:type="SQLTEXT"/>  
      <COLUMN SOURCE="C7" NAME="Interest"xsi:type="SQLDECIMAL"   
      PRECISION="5" SCALE="3"/>  
   </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="MapXMLDataToTbl"></a> E. 將 XML 資料對應到資料表  
 下列範例建立包含兩個資料行的空資料表 (`t_xml`)，其中第一個資料行對應到 `int` 資料類型，而第二個資料行則對應到 `xml` 資料類型。  
  
```  
CREATE TABLE t_xml (c1 int, c2 xml)  
```  
  
 下列 XML 格式檔案將會在資料表 `t_xml`中載入資料檔。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" PREFIX_LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLINT"/>  
  <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLNCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="ImportFixedFields"></a> F. 匯入固定長度或固定寬度的欄位  
 下列範例描述各有 `10` 個或 `6` 個字元的固定欄位。 格式檔案分別以 `LENGTH="10"` 和 `LENGTH="6"`來表示這些欄位長度/寬度。 資料檔案的每一列都是以歸位字元和換行字元的組合 {CR}{LF} 作為結束，這在格式檔案中是以 `TERMINATOR="\r\n"`來表示。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT  
       xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharFixed" LENGTH="10"/>  
    <FIELD ID="2" xsi:type="CharFixed" LENGTH="6"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="C1" xsi:type="SQLINT" />  
    <COLUMN SOURCE="2" NAME="C2" xsi:type="SQLINT" />  
  </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="AdditionalExamples"></a> 其他範例  
 如需非 XML 格式檔案及 XML 格式檔案的其他範例，請參閱下列主題：  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
