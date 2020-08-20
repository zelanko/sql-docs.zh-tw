---
description: 設定及管理全文檢索搜尋的同義字檔案
title: 設定及管理全文檢索搜尋的同義字檔案
ms.date: 07/01/2020
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: d713b4eb49a527f2cbbbf871cce9d01d4449443d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465060"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>設定及管理全文檢索搜尋的同義字檔案
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的全文檢索查詢可以透過使用「同義字」  ，搜尋使用者指定之詞彙的同義字。 每個同義字會針對特定語言定義一組同義字。 透過開發符合全文檢索資料的同義字，您可以有效地擴大針對該資料進行全文檢索查詢的範圍。

系統會針對所有 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 查詢以及指定 `FORMSOF THESAURUS` 子句的任何 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 查詢進行同義字比對。
  
全文檢索搜尋的同義字是一個 XML 文字檔。
  
##  <a name="whats-in-a-thesaurus"></a><a name="tasks"></a> 同義字的內容  
 您必須先以特定語言定義出同義字的對應 (亦即同義字)，然後全文檢索搜尋查詢才能尋找該語言的同義字。 您必須手動設定每個同義字，以便定義下列項目：  
  
-   展開集  
  
     展開集包含可以由全文檢索查詢彼此替代的一組同義字，例如 "writer"、"author" 和 "journalist"。 包含展開集中任何同義字之相符項目的查詢會展開成包含展開集中的其他每個同義字。  
  
     如需詳細資訊，請參閱本主題後面的[展開集的 XML 結構](#expansion)。  
  
-   取代集  
  
     取代集包含替代集所要取代的文字模式。 如需範例，請參閱本主題後面的[取代集的 XML 結構](#replacement)一節。 

-   變音符號設定  
  
     針對給定的同義字，所有搜尋模式都會區分或不區分變音符號，例如波狀符號 ( **~** )、尖重音符號 ( **&acute;** ) 或母音變化 ( **&uml;** ) (亦即，「區分腔調字」  或「不區分腔調字」  )。 例如，假設您在全文檢索查詢中，指定以其他模式取代模式 "caf&eacute;"。 如果同義字不區分腔調字，全文檢索搜尋就會取代模式 "caf&eacute;" 和 "cafe"。 如果同義字區分腔調字，全文檢索搜尋只會取代模式 "caf&eacute;"。 根據預設，同義字不會區分腔調字。  
  
##  <a name="default-thesaurus-files"></a><a name="initial_thesaurus_files"></a> 預設的同義字檔案
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一組 XML 同義字檔案 (每個支援的語言都有一個檔案)。 這些檔案基本上都是空的。 它們僅包含所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同義字通用的最上層 XML 結構以及標記為註解的範例同義字。  
  
##  <a name="location-of-thesaurus-files"></a><a name="location"></a> 同義字檔案的位置  
 同義字檔案的預設位置為：  
  
`<SQL_Server_data_files_path>\MSSQL13.MSSQLSERVER\MSSQL\FTDATA\`
  
這個預設位置包含下列檔案：  
  
-   **特定語言**同義字檔案  

    安裝程式會在上述位置安裝空的同義字檔案。 系統會針對每個支援的語言提供一個個別的檔案。 系統管理員可以自訂這些檔案。  
  
    同義字檔案的預設檔案名稱會使用下列格式：  
  
    `'ts' + <three-letter language-abbreviation> + '.xml'`
  
    特定語言的同義字檔案名稱會指定在下列登錄值中：
     
    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<instance-name>\MSSearch\<language-abbrev>`
  
-   **通用**同義字檔案  
  
    空的通用同義字檔案：tsGlobal.xml。  

### <a name="change-the-location-of-a-thesaurus-file"></a>變更同義字檔案的位置 
您可以變更同義字檔案的登錄機碼，藉以變更其位置和名稱。 針對每個語言，同義字檔案的位置會指定在下列登錄值中：  
  
`HKLM\SOFTWARE\Microsoft\Microsoft SQL Server\<instance name>\MSSearch\Language\<language-abbreviation>\TsaurusFile`
  
 通用同義字檔案會對應至 LCID 0 的中性語言。 只有管理員能夠變更這個值。  

##  <a name="how-full-text-queries-use-the-thesaurus"></a><a name="how_queries_use_tf"></a> 全文檢索查詢如何使用同義字  
同義字查詢會同時使用語言特有的同義字和通用同義字。
1.  首先，查詢會查閱語言特有的檔案並載入此檔案，以便進行處理 (除非已經載入此檔案)。 查詢會展開成包含同義字 (Thesaurus) 檔案中展開集和取代集規則所指定的語言特有同義字 (Synonym)。 
2.  然後，系統會針對通用同義字重複這些步驟。 不過，如果某個詞彙已經是語言特有同義字檔案中相符項目的一部分，該詞彙就不適用於在通用同義字中比對。  

##  <a name="structure-of-a-thesaurus-file"></a><a name="structure"></a> 同義字檔案的結構  
 每個同義字檔案都會定義識別碼為 `Microsoft Search Thesaurus` 的 XML 容器，以及包含範例同義字的 `<!--` ... `-->` 註解。 您可在包含子元素範例的 `<thesaurus>` 元素中定義同義字，而這些子元素會定義變音符號設定、展開集和取代集。

典型的空白同義字檔案包含下列 XML 文字：  
  
```xml  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```

### <a name="xml-structure-of-an-expansion-set"></a><a name="expansion"></a> XML structure of an expansion set  
  
 每個展開集都是用 `<expansion>` 元素括住。 在這個元素內，您可以使用 `<sub>` 元素來指定一或多個替代項目。 在展開集中，您可以指定一組彼此是同義字的替代項目。  
  
 例如，您可編輯展開區段，以將 "writer"、"author" 及 "journalist" 替代字視為同義字。 此時會展開包含某個替代項目之相符項目的全文檢索搜尋查詢，以併入展開集中指定的所有其他替代項目。 因此，在上個範例中，發出 FORMS OF THESAURUS 或 FREETEXT 查詢以尋找 "author" 這個字時，全文檢索搜尋也會傳回內含 "writer" 和 "journalist" 這些字的搜尋結果。  
  
這是上例之展開集區段的樣子：  
  
```xml  
<expansion>  
        <sub>writer</sub>  
        <sub>author</sub>  
        <sub>journalist</sub>  
</expansion>  
```  
  
### <a name="xml-structure-of-a-replacement-set"></a><a name="replacement"></a> XML structure of a replacement set  
  
每個取代集都是用 `<replacement>` 元素括住。 在這個元素內，您可以使用 `<pat>` 元素來指定一或多個模式，並使用 `<sub>` 元素來指定零或多個替代項目 (每個同義字指定一個)。 您也可以指定要用替代集取代的模式。 模式和替代項目都可以包含單字或一串文字。 如果沒有針對某個模式指定替代項目，其作用就是從使用者查詢中移除該模式。  
  
例如，假設您想要查詢 "Win8" (模式) 以將其取代為 "Windows Server 2012" 或 "Windows 8.0" (替代項目)。 如果您要執行全文檢索查詢以找出 "Win8"，則全文檢索搜尋只會傳回內含 "Windows Server 2012" 或 "Windows 8.0" 的搜尋結果。 它不會傳回內含 "Win8" 的結果。 這是因為 "Win8" 模式已「取代」為 "Windows Server 2012" 和 "Windows 8.0" 模式。  
  
這是上例之取代集區段的樣子：  
  
```xml  
<replacement>  
        <pat>Win8</pat>  
        <sub>Windows Server 2012</sub>  
        <sub>Windows 8.0</sub>  
</replacement>  
```  
  
如果您有兩個相似模式相符的取代集，則這兩個取代集中長度較長之取代集的優先順序較高。 例如，如果您執行 FORMS OF THESAURUS 查詢以找出 "Internet Explorer online community" 且具有下列取代集，則 "Internet Explorer" 取代集的優先順序高於 "Internet" 取代集。 因此，系統會將該查詢處理為 "IE online community" 或 "IE 9 online community"。  
  
```xml  
<replacement>  
         <pat>Internet</pat>  
         <sub>intranet</sub>  
</replacement>  
```  
  
和  
  
```xml  
<replacement>  
         <pat>Internet Explorer</pat>  
         <sub>IE</sub>  
         <sub>IE 9</sub>  
</replacement>  
```

### <a name="xml-structure-of-the-diacritics-setting"></a>變音符號設定的 XML 結構  
  
您可在單一 `<diacritics_sensitive>` 元素中指定同義字的變音符號設定。 這個元素包含可控制區分腔調字的整數值，如下所示：  
  
|變音符號設定|值|XML|  
|------------------------|-----------|---------|  
|不區分腔調字|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
|區分腔調字|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
> [!NOTE]  
>  此設定只能在檔案中套用一次，而且它會套用至檔案中的所有搜尋模式。 不能針對個別模式指定此設定。  

##  <a name="edit-a-thesaurus-file"></a><a name="editing"></a> 編輯同義字檔案  
您可以編輯特定語言的同義字檔案 (XML 檔案)，以設定同義字。 在安裝期間，系統會安裝空白的同義字檔案，其中僅包含 `<xml>` 容器和標記為註解的範例 `<thesaurus` 元素。 若要讓尋找同義字的全文檢索搜尋查詢正常運作，您必須實際建立 `<thesaurus` 元素以定義一組同義字。 您可以定義兩種同義字形式：展開集和取代集。  

### <a name="edit-a-thesaurus-file"></a>編輯同義字檔案  
  
1.  在 [記事本] 或其他文字編輯器中開啟同義字檔案。  
  
2.  如果是第一次編輯同義字檔案，則請分別移除檔案開頭及結尾處的下列註解行：  
  
    ```xml  
    <!--Commented out  
    -->  
    ```  
  
3.  新增、修改或刪除取代集或展開集。  
  
4.  儲存檔案並關閉記事本。  
  
5.  使用 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md) ，將同義字檔案的內容載入 tempdb，並指定對應至同義字檔案語言的地區設定識別碼 (LCID)。 例如，英文同義字檔案 tsenu.xml 的對應 LCID 就是 1033。  
  
    ```sql  
    USE AdventureWorks;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO
    ```

### <a name="recommendations-for-editing-thesaurus-files"></a>同義字檔案的編輯建議  
  
 我們建議同義字檔案中的項目不應該包含任何特殊字元。 這是因為斷詞工具在處理特殊字元方面具有難以察覺的行為。 如果某個同義字項目包含任何特殊字元，與該項目搭配使用的斷詞工具可能會針對全文檢索查詢產生難以察覺的行為隱含。  
  
 建議您不要在 `<sub>` 項目中包含任何停用字詞，因為全文檢索索引會省略停用字詞。 系統會展開查詢以包含來自同義字檔案的 `<sub>` 項目；如果 `<sub>` 項目包含停用字詞，就會不必要地增加查詢的大小。  

### <a name="restrictions-for-editing-thesaurus-files"></a>同義字檔案的編輯限制  
  
 當您編輯同義字檔案時，就會適用下列限制：  
  
-   只有系統管理員能夠更新、修改或刪除同義字檔案。  
  
-   當您使用文字編輯器工具編輯同義字檔案時，必須以 Unicode 格式儲存這些檔案，而且必須指定位元組順序標示 (BOM)。  
  
-   同義字項目不得為空白或斷詞為空字串。  
  
-   同義字檔案中的片語長度不得超過 512 個字元。  
  
-   在展開集的 `<sub>` 項目與取代集的 `<pat>` 元素之間，同義字不得包含任何重複的項目。  

## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)     
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)
 
