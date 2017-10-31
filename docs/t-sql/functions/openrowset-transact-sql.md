---
title: "OPENROWSET (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
caps.latest.revision: 130
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c23ec85299af595305a5f6d5141dbbf3ffab96d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含所有從 OLE DB 資料來源存取遠端資料所需的連接資訊。 這個方法是存取連結伺服器資料表的另一個方法，而且是使用 OLE DB 來連接和存取遠端資料的單次特定方法。 對於更常用到的 OLE DB 資料來源參考，請改用連結的伺服器。 如需詳細資訊，請參閱 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)。 `OPENROWSET`可以查詢的 FROM 子句中參考函數，如同一般資料表名稱。 `OPENROWSET`函式可以參考的目標資料表為`INSERT`， `UPDATE`，或`DELETE`陳述式中的，OLE DB 提供者功能而定。 雖然查詢可以傳回多個結果集，`OPENROWSET`傳回只有第一個。  
  
 `OPENROWSET`也支援透過內建的 BULK 提供者，可讓資料從檔案讀取並傳回一個資料列集的大量作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>引數  
 '*provider_name*'  
 這是一個字元字串，代表在登錄中指定之 OLE DB 提供者的易記名稱 (或 PROGID)。 *provider_name*沒有預設值。  
  
 '*datasource*'  
 這是一個對應至特定 OLE DB 資料來源的字串常數。 *資料來源*是要傳遞到 IDBProperties 介面來初始化提供者的提供者的 DBPROP_INIT_DATASOURCE 屬性。 這個字串通常都包含資料庫檔案的名稱、資料庫伺服器的名稱，或是提供者尋找資料庫所用的名稱。  
  
 '*user_id*'  
 這是一個字串常數，代表傳遞到指定之 OLE DB 提供者的使用者名稱。 *user_id*指定連接的安全性內容，並傳入當做 DBPROP_AUTH_USERID 屬性傳入來初始化提供者。 *user_id*不可以是 Microsoft Windows 登入名稱。  
  
 '*密碼*'  
 這是一個字串常數，代表傳遞到 OLE DB 提供者的使用者密碼。 *密碼*時，會傳遞會當做 DBPROP_AUTH_PASSWORD 屬性初始化提供者。 *密碼*不可以是 Microsoft Windows 密碼。  
  
 '*provider_string*'  
 這是一個提供者特定的連接字串，會當做 DBPROP_INIT_PROVIDERSTRING 屬性傳入來初始化 OLE DB 提供者。 *provider_string*通常會封裝將提供者初始化所需的所有連接資訊。 如需可辨識的關鍵字的清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，請參閱[初始化和授權屬性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
 *類別目錄*  
 這是指定之物件所在的目錄或資料庫名稱。  
  
 *結構描述*  
 這是指定之物件的結構描述或物件擁有者名稱。  
  
 *物件*  
 這是唯一識別所處理之物件的物件名稱。  
  
 '*查詢*'  
 這是傳給提供者，並且由提供者執行的字串常數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體不會處理這項查詢，但會處理提供者傳回的查詢結果，亦即通過查詢。 如果提供者不是透過資料表名稱，而只透過命令語言使用其資料表資料，通過查詢將會很實用。 在遠端伺服器上，就支援通過查詢，只要查詢提供者支援 OLE DB 命令物件，而且它的強制介面。 如需詳細資訊，請參閱[SQL Server Native Client &#40; OLE DB &#41;參考](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)。  
  
 BULK  
 使用 BULK 資料列集提供者，讓 OPENROWSET 讀取檔案資料。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，OPENROWSET 可以從資料檔讀取，而不必將資料載入到目標資料表中。 此舉可讓您搭配簡單的 SELECT 陳述式來使用 OPENROWSET。  
  
 BULK 選項的引數可讓您全力控制在哪裡開始和結束資料讀取、如何處理錯誤以及如何解譯資料。 例如，您可以指定資料檔會讀取成單一資料列、 單一資料行資料列集的類型**varbinary**， **varchar**，或**nvarchar**。 預設行為將在接下來的引數描述中加以描述。  
  
 如需有關如何使用 BULK 選項的詳細資訊，請參閱本主題稍後的＜備註＞。 如需有關 BULK 選項所需權限的詳細資訊，請參閱本主題稍後的「權限」。  
  
> [!NOTE]  
>  當它以完整復原模式匯入資料時，OPENROWSET (BULK ...) 不會最佳化記錄。  
  
 如需有關準備資料進行大量匯入資訊，請參閱[準備的資料大量匯出或匯入 &#40;SQL Server &#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 這是要將資料複製到目標資料表之資料檔的完整路徑。   
 **適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
開頭為[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1 data_file 可保留在 Azure blob 儲存體中。 如需範例，請參閱[範例的大量資料的存取 Azure Blob 儲存體](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。
  
 \<bulk_options >  
 為 BULK 選項指定一個或多個引數。  
  
 字碼頁 = {'ACP' |'OEM' |「 原始 」 |*字碼頁*'}  
 指定資料檔案中之資料的字碼頁。 字碼頁才會相關的資料包含**char**， **varchar**，或**文字**字元值大於 127 或小於 32 的資料行。  
  
> [!NOTE]  
>  我們建議您除了指定在格式檔案中，每個資料行的定序名稱，當您希望 65001 選項的優先順序高於定序/字碼頁規格。  
  
|CODEPAGE 值|Description|  
|--------------------|-----------------|  
|ACP|將轉換的資料行**char**， **varchar**，或**文字**資料型別，從 ANSI /[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 字碼頁 (ISO 1252)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字碼頁。|  
|OEM (預設值)|將轉換的資料行**char**， **varchar**，或**文字**從系統 OEM 字碼頁的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字碼頁。|  
|RAW|不進行字碼頁之間的轉換。 這是最快的選項。|  
|*code_page*|指出在哪一個來源字碼頁，將資料檔中的字元資料加以編碼；例如 850。<br /><br /> **\*\*重要\* \*** 之前的版本[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]不支援字碼頁 65001 （utf-8 編碼）。|  
  
 ERRORFILE ='*file_name*'  
 指定用來收集格式錯誤且無法轉換成 OLE DB 資料列集之資料列的檔案。 這些資料列會「依照原狀」，從資料檔複製到這個錯誤檔中。  
  
 錯誤檔是在開始執行命令時建立。 如果檔案已經存在，就會引發錯誤。 另外，還會建立一個副檔名為 .ERROR.txt 的控制檔。 這個檔案會參考錯誤檔中的每個資料列，且會提供錯誤診斷。 錯誤更正之後，就能夠載入資料。  
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。
開頭為[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]、`error_file_path`可保留在 Azure blob 儲存體中。 

' errorfile_data_source_name'   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。
具名的外部資料來源會指向 Azure Blob 儲存體的位置將包含匯入期間發現錯誤的檔案時發生錯誤。 必須建立外部資料來源，使用`TYPE = BLOB_STORAGE`選項加入[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1。 如需詳細資訊，請參閱[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)。
  
 FIRSTROW =*first_row*  
 指定要載入之第一個資料列的號碼。 預設值是 1。 這表示指定之資料檔中的第一個資料列。 資料列號碼是由計算資料列結束字元所決定。 FIRSTROW 是以 1 為基底。  
  
 LASTROW =*last_row*  
 指定要載入之最後一個資料列的號碼。 預設值是 0。 這表示指定的資料檔中的最後一個資料列。  
  
 MAXERRORS =*maximum_errors*  
 指定最多出現幾個語法錯誤或不符合的資料列 (如格式檔所定義) 之後，OPENROWSET 便會擲出例外狀況。 只要尚未到達 MAXERRORS，OPENROWSET 會忽略所有不正確的資料列，也不載入它，並將這個不正確的資料列計為一個錯誤。  
  
 預設值為*maximum_errors*為 10。  
  
> [!NOTE]  
>  MAX_ERRORS 不適用於 CHECK 條件約束，或轉換**money**和**bigint**資料型別。  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 指定資料檔中大約有多少資料列。 這個值應該與實際的資料列數差不多。  
  
 OPENROWSET 一律將資料檔當做單一批次加以匯入。 不過，如果您指定*rows_per_batch*值 > 0，表示查詢處理器會使用的值*rows_per_batch*做為查詢計畫中配置資源的提示。  
  
 根據預設，ROWS_PER_BATCH 是未知的。 指定 ROWS_PER_BATCH = 0 相當於省略 ROWS_PER_BATCH。  
  
 順序 ({*資料行*[ASC |DESC]} [，... *n*  ] [UNIQUE])  
 指定要如何排序資料檔中資料的選擇性提示。 依預設，大量作業會假設資料檔沒有排序。 如果查詢最佳化工具可以利用指定的順序來產生更有效率的查詢計畫，效能就可能會提升。 指定排序可能很有用處的範例包括以下情況：  
  
-   將資料列插入具有叢集索引的資料表中，其中的資料列集資料會根據叢集索引鍵來排序。  
  
-   將資料列集與另一個資料表聯結，其中的排序資料行和聯結資料行會相符。  
  
-   依據排序資料行彙總資料列集資料。  
  
-   在查詢的 FROM 子句中使用資料列集當做來源資料表，其中的排序資料行和聯結資料行會相符。  
  
 UNIQUE 會指定沒有重複項目的資料檔。  
  
 如果資料檔中的實際資料列並未根據指定的順序來排序，或是指定了 UNIQUE 提示而且有重複的索引鍵存在，則會傳回錯誤。  
  
 當使用 ORDER 時，需要資料行別名。 資料行別名清單必須參考由 BULK 子句所存取的衍生資料表。 ORDER 子句中所指定的資料行名稱會參考這個資料行別名清單。 大型值型別 (**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，和**xml**) 及大型物件 (LOB) 類型 (**文字**， **ntext**，和**映像**) 不能指定資料行。  
  
 SINGLE_BLOB  
 傳回的內容*data_file*當做類型的單一資料列、 單一資料行資料列集**varbinary （max)**。  
  
> [!IMPORTANT]  
>  建議您只使用 SINGLE_BLOB 選項匯入 XML 資料，而不要使用 SINGLE_CLOB 和 SINGLE_NCLOB，因為只有 SINGLE_BLOB 支援所有的 Windows 編碼轉換。  
  
 SINGLE_CLOB  
 藉由讀取*data_file*以 ascii 模式，傳回內容類型的單一資料列、 單一資料行資料列集當做**varchar （max)**，使用目前資料庫的定序。  
  
 SINGLE_NCLOB  
 藉由讀取*data_file*為 UNICODE，傳回內容類型的單一資料列、 單一資料行資料列集當做**nvarchar （max)**，使用目前資料庫的定序。  

### <a name="input-file-format-options"></a>輸入的檔案格式選項
  
格式 **=**  'CSV'   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
指定逗號分隔的值檔案符合[遵循 RFC 4180](https://tools.ietf.org/html/rfc4180)標準。

 FORMATFILE ='*f*'  
 指定格式檔的完整路徑。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援兩種類型的格式檔案：XML 和非 XML。  
  
 您必須使用格式檔，才能定義結果集中的資料行類型。 不過，當指定 SINGLE_CLOB、SINGLE_BLOB 或 SINGLE_NCLOB 時，就不需要格式檔，這是唯一的例外狀況。  
  
 格式檔案的相關資訊，請參閱[使用格式檔案大量匯入資料 &#40;SQL Server &#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
開頭為[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1 f 可保留在 Azure blob 儲存體中。 如需範例，請參閱[範例的大量資料的存取 Azure Blob 儲存體](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。

FIELDQUOTE  **=**  'field_quote'   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
指定將用於做為 CSV 檔案中的引號字元的字元。 如果未指定，引號字元 （"） 會用作引號字元如中所定義[遵循 RFC 4180](https://tools.ietf.org/html/rfc4180)標準。

  
## <a name="remarks"></a>備註  
 `OPENROWSET`可以用來存取遠端資料從 OLE DB 資料來源時，才**DisallowAdhocAccess**登錄選項明確設為 0 指定之提供者，而且特定分散式查詢 進階組態選項啟用。 若未設定這些選項，預設行為便不允許特定存取。  
  
 存取遠端 OLE DB 資料來源時，用戶端連接到將進行查詢之伺服器所在的伺服器上，不會自動委派信任連接的登入識別。 此時必須設定驗證委派。  
  
 如果 OLE DB 提供者支援指定之資料來源中的多個目錄和結構描述，則需要用到目錄和結構描述名稱。 值*目錄*和*結構描述*OLE DB 提供者不支援它們時，可以省略。 如果提供者只支援結構描述名稱，表單的兩段式名稱*結構描述***。***物件*必須指定。 如果提供者只支援類別目錄名稱，格式的三部分名稱*目錄***。***結構描述***。***物件*必須指定。 通過查詢必須指定三部分名稱使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 如需詳細資訊，請參閱[TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`不接受其引數的變數。  
  
 呼叫`OPENDATASOURCE`， `OPENQUERY`，或`OPENROWSET`中`FROM`子句個別且獨立從評估做為目標的更新，這些函式的任何呼叫即使完全相同的引數會提供給兩個呼叫。 尤其，針對其中一個呼叫結果所套用的篩選或聯結條件對於另一個呼叫的結果沒有作用。  
  
## <a name="using-openrowset-with-the-bulk-option"></a>搭配 BULK 選項使用 OPENROWSET  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 增強功能支援 OPENROWSET(BULK...) 函數：  
  
-   搭配使用的 FROM 子句`SELECT`可以呼叫`OPENROWSET(BULK...)`而不是資料表名稱，與完整`SELECT`功能。  
  
     `OPENROWSET`與`BULK`選項需要相互關聯名稱，也稱為範圍變數或別名中`FROM`子句。 您可以指定資料行別名。 如果未指定資料行別名清單，格式檔就必須有資料行名稱。 指定資料行別名會覆寫格式檔中的資料行名稱，例如：  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    若要加入的失敗`AS <table_alias>`就會產生錯誤：    
>    訊息 491，層級 16，狀態 1，行 20    
>    必須為 FROM 子句中的大量資料列集指定相互關聯名稱。    
  
-   A`SELECT...FROM OPENROWSET(BULK...)`陳述式的檔案中的資料會直接查詢，而不將資料匯入資料表。 `SELECT…FROM OPENROWSET(BULK...)`陳述式也可以使用格式檔案來指定資料行名稱和資料類型列出大量資料行別名。  
  
-   使用`OPENROWSET(BULK...)`當做來源資料表`INSERT`或`MERGE`陳述式大量匯入資料，從資料檔將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 如需詳細資訊，請參閱[使用 BULK INSERT 或 OPENROWSET &#40; 匯入大量資料BULK_ &#41;&#40;SQL Server &#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   當`OPENROWSET BULK`選項搭配`INSERT`陳述式，BULK 子句支援資料表提示。 除了一般資料表提示，例如`TABLOCK`、`BULK`子句也接受下列特定的資料表提示： `IGNORE_CONSTRAINTS` (僅忽略`CHECK`和`FOREIGN KEY`條件約束)， `IGNORE_TRIGGERS`， `KEEPDEFAULTS`，和`KEEPIDENTITY`。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 如需有關如何使用資訊`INSERT...SELECT * FROM OPENROWSET(BULK...)`陳述式，請參閱[大量匯入和匯出資料 &#40;SQL Server &#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). 如需大量匯入所執行的資料列插入作業於何時記錄到交易記錄的資訊，請參閱[大量匯入採用最低限度記錄的必要條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
> [!NOTE]  
>  當您使用`OPENROWSET`，請務必了解如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]處理模擬。 安全性考量的相關資訊，請參閱[使用 BULK INSERT 或 OPENROWSET &#40; 匯入大量資料BULK_ &#41;&#40;SQL Server &#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>大量匯入 SQLCHAR、SQLNCHAR 或 SQLBINARY 資料  
 OPENROWSET(BULK...) 會假設，如果未指定，則 SQLCHAR、SQLNCHAR 或 SQLBINARY 資料的最大長度不會超過 8000 個位元組。 正在匯入的資料是否包含任何的 LOB 資料欄位在**varchar （max)**， **nvarchar （max)**，或**varbinary （max)**超過 8000 個位元組的物件，您必須使用XML 格式檔案來定義資料欄位的最大長度。 若要指定最大長度，請編輯格式檔案，並宣告 MAX_LENGTH 屬性。  
  
> [!NOTE]  
>  自動產生的格式檔案不會指定 LOB 欄位的長度或最大長度。 但是，您可以編輯格式檔案，並手動指定長度或最大長度。  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>大量匯出或匯入 SQLXML 文件  
 若要大量匯出或匯入 SQLXML 資料，請在格式檔案中使用下列其中一種資料類型。  
  
|資料類型|效果|  
|---------------|------------|  
|SQLCHAR 或 SQLVARYCHAR|資料是使用用戶端字碼頁或定序所隱含的字碼頁所傳送。|  
|SQLNCHAR 或 SQLNVARCHAR|以 Unicode 格式傳送這份資料。|  
|SQLBINARY 或 SQLVARYBIN|未經任何轉換即傳送這份資料。|  
  
## <a name="permissions"></a>Permissions  
 `OPENROWSET`權限，取決於傳遞給 OLE DB 提供者的使用者名稱的權限。 若要使用`BULK`選項需要`ADMINISTER BULK OPERATIONS`權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. 搭配 SELECT 和 SQL Server Native Client OLE DB 提供者來使用 OPENROWSET  
 下列範例會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者來存取`HumanResources.Department`資料表中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]遠端伺服器上的資料庫`Seattle1`。 (使用 SQLNCLI 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會重新導向至最新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者)。`SELECT` 陳述式是用來定義傳回的資料列集。 提供者字串包含 `Server` 和 `Trusted_Connection` 關鍵字。 這些關鍵字可辨識[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。  
  
```tsql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. 使用 Microsoft OLE DB Provider for Jet  
 下列範例是透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet，存取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access `Customers` 資料庫中的 `Northwind` 資料表。  
  
> [!NOTE]  
>  這個範例假設您已經安裝了 Access。 若要執行這個範例，您必須安裝 Northwind 資料庫。  
  
```tsql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. 使用 OPENROWSET 和 INNER JOIN 中的另一份資料表  
 下列範例會選取所有資料從`Customers`的本機執行個體中的資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`Northwind`資料庫以及從`Orders`資料表存取`Northwind`儲存在同一部電腦上的資料庫。  
  
> [!NOTE]  
>  這個範例假設您已經安裝了 Access。 若要執行這個範例，您必須安裝 Northwind 資料庫。  
  
```tsql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. 使用 OPENROWSET 將檔案資料大量插入到 varbinary(max) 資料行中  
 下列範例會建立一份小型資料表做為示範之用，並且從 `Text1.txt` 根目錄下的 `C:` 檔，將檔案資料插入到 `varbinary(max)` 資料行中。  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. 搭配一個格式檔來使用 OPENROWSET BULK 提供者，從文字檔擷取資料列  
 下列範例會利用一個格式檔，從 Tab 鍵分隔的文字檔 `values.txt` 擷取資料列，該檔含有下列資料：  
  
```tsql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 格式檔 `values.fmt` 會描述 `values.txt` 中的資料行：  
  
```tsql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 這是擷取該資料的查詢：  
  
```tsql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. 指定格式檔案和程式碼 頁面  
 下列範例顯示如何同時使用這兩種格式檔案和程式碼頁面選項。  
  
```tsql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. 從 CSV 檔案，使用格式檔案的存取資料  
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
```tsql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. 從 CSV 檔案，不使用格式檔案的存取資料

```tsql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. 資料檔案儲存在 Azure Blob 儲存體的存取   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。   
下列範例會使用外部資料來源指向 Azure 儲存體帳戶，並建立共用的存取簽章使用資料庫範圍認證中的容器。     

```tsql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
對於完成`OPENROWSET`範例包括設定認證和外部資料來源，請參閱[範例的大量資料的存取 Azure Blob 儲存體](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。
 
### <a name="additional-examples"></a>其他範例  
 如需其他範例會示範如何使用`INSERT...SELECT * FROM OPENROWSET(BULK...)`，請參閱下列主題：  
  
-   [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [資料列集函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

