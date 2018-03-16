---
title: "CAST 和 CONVERT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 56326d7862c004ac056e329e6cc05f7bbe056aea
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="cast-and-convert-transact-sql"></a>CAST 和 CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

轉換運算式的資料類型。  
例如，下列範例會將輸入資料類型變更為具有不同有效位數層級的兩個其他資料類型。
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|原始   |ssNoversion    |Decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> 本主題最下方有提供許多[範例](#BKMK_examples)。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>引數  
*expression*  
這是任何有效的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
*data_type*  
這是目標資料類型。 這包括 **xml**、**bigint** 和 **sql_variant**。 無法使用別名資料類型。
  
*length*  
這是指定目標資料類型之長度的選擇性整數。 預設值是 30。
  
*style*  
這是指定 CONVERT 函數如何轉譯 *expression* 的整數運算式。 如果 style 是 NULL，就會傳回 NULL。 此範圍取決於 *data_type*。 
  
## <a name="return-types"></a>傳回類型
傳回轉譯為 *data_type* 的 *expression*。

## <a name="date-and-time-styles"></a>日期和時間樣式  
當 *expression* 是日期或時間資料類型時，*style* 可以是下表中所顯示的其中一個值。 其他值則當做 0 處理。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，從日期和時間類型轉換為 **datetimeoffset** 時，唯一支援的樣式為 0 或 1。 所有其他轉換樣式都會傳回錯誤 9809。
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用科威特演算法來支援阿拉伯文樣式的日期格式。
  
|不含世紀 (yy) (<sup>1</sup>)|含世紀 (yyyy)|Standard|輸入/輸出 (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** 或 **100** (<sup>1,</sup><sup>2</sup>)|datetime 和 smalldatetime 的預設值|mon dd yyyy hh:miAM (或 PM)|  
|**1**|**101**|美式英文|1 = mm/dd/yy<br /> 101 = mm/dd/yyyy|  
|**2**|**102**|ANSI|2 = yy.mm.dd<br /> 102 = yyyy.mm.dd|  
|**3**|**103**|英式英文/法文|3 = dd/mm/yy<br /> 103 = dd/mm/yyyy|  
|**4**|**104**|德文|4 = dd.mm.yy<br /> 104 = dd.mm.yyyy|  
|**5**|**105**|義大利文|5 = dd-mm-yy<br /> 105 = dd-mm-yyyy|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mon yy<br /> 106 = dd mon yyyy|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mon dd, yy<br /> 107 = Mon dd, yyyy|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** 或 **109** (<sup>1,</sup><sup>2</sup>)|預設值 + 毫秒|mon dd yyyy hh:mi:ss:mmmAM (或 PM)|  
|**10**|**110**|USA|10 = mm-dd-yy<br /> 110 = mm-dd-yyyy|  
|**11**|**111**|日本|11 = yy/mm/dd<br /> 111 = yyyy/mm/dd|  
|**12**|**112**|ISO|12 = yymmdd<br /> 112 = yyyymmdd|  
|-|**13** 或 **113** (<sup>1,</sup><sup>2</sup>)|歐洲預設值 + 毫秒|dd mon yyyy hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** 或 **120** (<sup>2</sup>)|ODBC 標準|yyyy-mm-dd hh:mi:ss(24h)|  
|-|**21** 或 **121** (<sup>2</sup>)|time、date、datetime2 和 datetimeoffset 的 ODBC 標準 (使用毫秒) 預設值|yyyy-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|yyyy-mm-ddThh:mi:ss.mmm (無空格)<br /> 注意：如果毫秒 (mmm) 的值為 0，將不會顯示毫秒值。 例如，'2012-11-07T18:26:20.000' 值會顯示為 '2012-11-07T18:26:20'。|  
|-|**127**(<sup>6, 7</sup>)|具有時區 Z 的 ISO8601。|yyyy-mm-ddThh:mi:ss.mmmZ (無空格)<br /> 注意：如果毫秒 (mmm) 的值為 0，將不會顯示毫秒值。 例如，'2012-11-07T18:26:20.000' 值會顯示為 '2012-11-07T18:26:20'。|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|回曆 (<sup>5</sup>)|dd mon yyyy hh:mi:ss:mmmAM<br /> 在此樣式中，mon 代表完整月份名稱的多 Token 回曆 unicode 表示法。 這個值無法在 SSMS 的預設美國安裝中正確呈現。|  
|-|**131** (<sup>2</sup>)|回曆 (<sup>5</sup>)|dd/mm/yyyy hh:mi:ss:mmmAM|  
  
<sup>1</sup> 這些樣式值會傳回不具決定性的結果。 其中包括所有 (yy) (不含世紀) 樣式和 (yyyy) (含世紀) 樣式的子集。
  
<sup>2</sup> 預設值 (*style** *0** 或 **100**、**9** 或 **109**、**13** 或 **113**、**20** 或 **120** 及 **21** 或 **121**) 一律會傳回世紀 (yyyy)。
  
<sup>3</sup> 當轉換成 **datetime** 時輸入；當轉換成字元資料時輸出。
  
<sup>4</sup> 專為 XML 設計。 如果是從 **datetime** 或 **smalldatetime** 轉換成字元資料，則輸出格式如上表中所述。
  
<sup>5</sup> 阿拉伯回曆是具有多種變化的日曆系統。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用科威特演算法。
  
> [!IMPORTANT]  
>  根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據截止年份 2049 來解譯兩位數的年份。 也就是說，兩位數年份 49 會解譯為 2049，而兩位數年份 50 會解譯成 1950。 許多用戶端應用程式 (例如根據 Automation 物件的應用程式) 都使用截止年份 2030 年。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的兩位數年份截止設定選項會變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的截止年份，並允許以一致方式處理日期。 我們建議您指定四位數的年份。  
  
<sup>6</sup> 只有在從字元資料轉換為 **datetime** 或 **smalldatetime** 時才支援。 當只代表日期或只代表時間元件的字元資料轉換為 **datetime** 或 **smalldatetime** 資料類型時，未指定的時間元件會設定為 00:00:00.000，而未指定的日期元件則會設定為 1900-01-01。
  
<sup>7</sup> 選擇性的時區指標 Z 可用來以較輕鬆的方式將具有時區資訊的 XML **datetime** 值對應到沒有時區的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 值。 Z 是時區 UTC - 0 的指標。 其他的時區是以 + 或 - 方向位移的 HH:MM 來代表。 例如： `2006-12-12T23:45:12-08:00`＞。
  
當您從 **smalldatetime** 轉換成字元資料時，包括秒或毫秒的樣式會在這些位置顯示零。 當您從 **datetime** 或 **smalldatetime** 值轉換時，可以利用適當的 **char** 或 **varchar** 資料類型長度來截斷不需要的日期部分。
  
當您從含有時間之樣式的字元資料轉換成 **datetimeoffset** 時，時區時差就會附加至結果。
  
## <a name="float-and-real-styles"></a>float 和 real 樣式
當 *expression* 是 **float** 或 **real** 時，*style* 可以是下表中所顯示的其中一個值。 其他值則當做 0 處理。
  
|ReplTest1|輸出|  
|---|---|
|**0** (預設)|最多 6 位數。 在適當時機，供科學記號標記法使用。|  
|**1**|一律 8 位數。 一律用在科學記號標記法中。|  
|**2**|一律 16 位數。 一律用在科學記號標記法中。|  
|**3**|一律 17 位數。 用於不失真的轉換。 透過這個樣式，可保證將每個不同的 float 或 real 值轉換成相異的字元字串。<br /> **適用對象：**[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，以及 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更新版本。|  
|**126、128、129**|因舊版因素而納入，但在未來版本中可能會被取代。|  
  
## <a name="money-and-smallmoney-styles"></a>money 和 smallmoney 樣式
當 *expression* 是 **money** 或 **smallmoney** 時，*style* 可以是下表中所顯示的其中一個值。 其他值則當做 0 處理。
  
|ReplTest1|輸出|  
|---|---|
|**0** (預設)|小數點左側並不會每隔三位數加一個逗號，小數點右側有兩個位數；如 4235.98。|  
|**1**|小數點左側每隔三位數加一個逗號，小數點右側有兩位數；如 3,510.92。|  
|**2**|小數點左側並不會每隔三位數加一個逗號，小數點右側有四個位數；如 4235.9819。|  
|**126**|轉換成 char(n) 或 varchar(n) 時，相當於樣式 2|  
  
## <a name="xml-styles"></a>xml 樣式
當 *expression* 是 **xml*** 時，style* 可以是下表中所顯示的其中一個值。 其他值則當做 0 處理。
  
|ReplTest1|輸出|  
|---|---|
|**0** (預設)|使用預設剖析行為，捨棄無意義的空格，不允許內部 DTD 子集。<br /> **注意：**當您轉換成 **xml** 資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無意義空格的處理方式會與 XML 1.0 不同。 如需詳細資訊，請參閱[建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)。|  
|**1**|保留無意義的空格。 這個樣式設定會將預設的 **xml:space** 處理行為設成如同已指定 **xml:space="preserve"**。|  
|**2**|啟用有限的內部 DTD 子集處理。<br /><br /> 如果啟用的話，伺服器可以利用內部 DTD 子集所提供的下列資訊來執行非驗證的剖析作業。<br /> - 已套用屬性的預設值。<br /> - 已解決和展開內部實體參考。<br /> - 已檢查 DTD 內容模型，以確定語法的正確性。<br /> 剖析器會忽略外部 DTD 子集。 另外，它也不會評估 XML 宣告來了解 **standalone** 屬性是設為 **yes** 還是 **no**，而是會依照獨立文件的方式來剖析 XML 執行個體。|  
|**3**|保留無意義的空格，啟用有限的內部 DTD 子集處理。|  
  
## <a name="binary-styles"></a>二進位樣式
當 *expression* 是 **binary(n)**、**varbinary(n)**、**char(n)** 或 **varchar(n)** 時，*style* 可以是下表中所顯示的其中一個值。 此表中沒有列出的樣式值會傳回錯誤。
  
|ReplTest1|輸出|  
|---|---|
|**0** (預設)|將 ASCII 字元轉譯成二進位位元組或將二位進位元組轉譯成 ASCII 字元。 每個字元或位元組都會以 1:1 的方式轉換。<br /> 如果 *data_type* 是二進位類型，就會在結果的左邊加入字元 0x。|  
|**1**、**2**|如果 *data_type* 是二進位類型，此運算式就必須是字元運算式。 *expression* 必須由偶數個十六進位數字 (0、1、2、3、4、5、6、7、8、9、A、B、C、D、E、F、a、b、c、d、e、f) 所構成。 如果 *style* 設定為 1，字元 0x 就必須是運算式中的前兩個字元。 如果此運算式含有奇數個字元，或者其中任何字元無效，就會引發錯誤。<br /> 如果已轉換之運算式的長度超過 *data_type* 的長度，結果就會自右截斷。<br /> 大於已轉換結果之固定長度的 *data_types* 會在結果的右邊加入零。<br /> 如果 data_type 是字元類型，此運算式就必須是二進位運算式。 每個二進位字元都會轉換成兩個十六進位字元。 如果已轉換之運算式的長度超過 *data_type* 的長度，就會自右截斷。<br /> 如果 *data_type* 是固定大小的字元類型，而且已轉換之結果的長度小於 *data_type* 的長度，就會在已轉換之運算式的右邊加入空格，以便維持偶數個十六進位數字。<br /> 針對 *style* 1 的已轉換結果，系統會在它的左邊加入字元 0x。|  
  
## <a name="implicit-conversions"></a>隱含的轉換
隱含的轉換是不需要指定 CAST 或 CONVERT 函數，便能夠進行的轉換。 明確的轉換是需要指定 CAST 或 CONVERT 函數，才能進行的轉換。 下圖顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統提供之資料類型所能使用的所有明確與隱含資料類型轉換。 這些包括 **xml**、**bigint** 和 **sql_variant**。 從 **sql_variant** 資料類型進行指派時，不可使用隱含轉換，但可以隱含轉換成 **sql_variant**。
  
> [!TIP]  
>  若要取得此圖表的可下載 PDF 檔案，請從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=35834) \(英文\) 取得。  
  
![資料類型轉換表](../../t-sql/data-types/media/lrdatahd.png "資料類型轉換表")
  
當您在 **datetimeoffset** 與字元類型 **char**、**varchar**、**nchar** 和 **nvarchar** 之間轉換時，轉換過之時區時差部分的 HH 和 MM 應該永遠是兩位數，例如 -08:00。
  
> [!NOTE]  
>  由於 Unicode 資料使用的位元組數目一律是偶數，因此，在 **binary** 或 **varbinary** 和 Unicode 支援的資料類型之間轉換時，要特別小心。 例如，下列轉換不會傳回 41 的十六進位值；而是傳回 4100：`SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`。  
  
## <a name="large-value-data-types"></a>大數值資料類型
大數值資料類型會表現出與小數值資料類型相同的隱含和明確轉換行為，明確地說，便是 **varchar**、**nvarchar** 和 **varbinary** 資料類型。 不過，您應該考慮下列方針：
-   從 **image** 轉換為 **varbinary(max)** (反之亦然) 是一種隱含的轉換，且 **text** 和 **varchar(max)**，以及 **ntext** 和 **nvarchar(max)** 之間的轉換亦是如此。  
-   從大數值資料類型 (如 **varchar(max)**) 轉換成較小的對應資料類型 (如 **varchar**) 是隱含的轉換，但如果大數值對於較小資料類型的指定長度而言太大，便會被截斷。  
-   從 **varchar**、**nvarchar** 或 **varbinary** 轉換成對應的大數值資料類型是透過隱含的方式執行。  
-   從 **sql_variant** 資料類型轉換為大數值資料類型為明確的轉換。  
-   大數值資料類型無法轉換成 **sql_variant** 資料類型。  
  
如需有關如何從 **xml** 資料類型轉換的詳細資訊，請參閱[建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
## <a name="xml-data-type"></a>xml 資料型別
當您將 **xml** 資料類型明確或隱含地轉換為字串或二進位資料類型時，**xml** 資料類型的內容會根據一組規則來序列化。 如需如需這些規則的相關資訊，請參閱[定義 XML 資料的序列化](../../relational-databases/xml/define-the-serialization-of-xml-data.md)。 如需有關如何從其他資料類型轉換為 **xml** 資料類型的資訊，請參閱[建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
## <a name="text-and-image-data-types"></a>text 和 image 資料類型
不支援 **text** 和 **image** 資料類型進行自動資料類型轉換。 您可以將 **text** 資料明確地轉換成字元資料，並將 **image** 資料轉換成 **binary** 或 **varbinary**，但最大長度是 8000 位元組。 如果您嘗試進行不正確的轉換，例如將包括字母的字元運算式轉換成 **int**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回一則錯誤訊息。
  
## <a name="output-collation"></a>輸出定序  
當 CAST 或 CONVERT 的輸出是字元字串，輸入也是字元字串時，輸出的定序和定序標籤與輸入相同。 如果輸入不是字元字串，輸出會使用預設的資料庫定序及強制預設的定序標籤。 如需詳細資訊，請參閱[定序優先順序 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)。
  
若要將不同的定序指派給輸出，請將 COLLATE 子句套用至 CAST 或 CONVERT 函數結果運算式上。 例如：
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>截斷和捨入結果
當您將字元或二進位運算式 (**char**、**nchar**、**nvarchar**、**varchar**、**binary** 或 **varbinary**) 轉換成不同資料類型的運算式時，資料可能會被截斷、只顯示部分資料，或因結果太短無法顯示而傳回錯誤。 除了下表所顯示的轉換之外，轉換成 **char**、**varchar**、**nchar**、**nvarchar**、 **binary** 和 **varbinary** 都會被截斷。
  
|來源資料類型|目標資料類型|結果|  
|---|---|---|
|**int**、**smallint** 或 **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**、**smallmoney**、**numeric**、**decimal**、**float** 或 **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\* = 結果太短，無法顯示。 E = 因結果太短無法顯示，而傳回錯誤。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保證只有往返轉換 (從原始資料類型轉換至其他資料類型之後再轉換回來) 才會各版本都產生相同的值。 下列範例會顯示這類往返轉換：
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  請不要嘗試建構 **binary** 值，然後將其轉換為 numeric 資料類型類別目錄的其中一種資料類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保證在不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本之間，將 **decimal** 或 **numeric** 資料類型轉換為 **binary** 的結果都會是相同的。  
  
下列範例會顯示因太小而無法顯示的結果運算式。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
當您轉換小數位數不同的資料類型時，有時會截斷結果值，有時會捨入結果值。 下表說明這個行為。
  
|來源|若要|行為|  
|---|---|---|
|**numeric**|**numeric**|捨入|  
|**numeric**|**int**|截斷|  
|**numeric**|**money**|捨入|  
|**money**|**int**|捨入|  
|**money**|**numeric**|捨入|  
|**float**|**int**|截斷|  
|**float**|**numeric**|捨入<br /><br /> 如果您將使用科學記號標記法的 **float** 值轉換成 **decimal** 或 **numeric**，就會限制為只有 17 個有效位數的值。 有效位數超過 17 的任何值都會捨入為零。|  
|**float**|**datetime**|捨入|  
|**datetime**|**int**|捨入|  
  
例如，10.6496 和-10.6496 這兩個值可能會被截斷，或在轉換成 **int** 或 **numeric** 類型期間被捨入：
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
下表將顯示該查詢的結果：
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
當您轉換資料類型，且目標資料類型的小數位數小於來源資料類型時，會將值捨入。 例如，下列轉換的結果是 `$10.3497`：
  
`SELECT CAST(10.3496847 AS money);`
  
當非數值的 **char**、**nchar**、**varchar** 或 **nvarchar** 資料被轉換成 **int**、**float**、**numeric** 或 **decimal** 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤訊息。 當空字串 (" ") 被轉換為 **numeric** 或 **decimal** 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會傳回錯誤。
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>某些日期時間轉換不具決定性
下表列出字串對日期時間轉換不具決定性的樣式。
  
|||  
|-|-|  
|100 以下的所有樣式<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> 樣式 20 和 21 除外
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (代理字組)
從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，如果您使用補充字元 (SC) 定序，從 **nchar** 或 **nvarchar** 到較小長度之 **nchar** 或 **nvarchar** 類型的 CAST 作業將不會在代理字組內截斷，而會在補充字元之前截斷。 例如，下列程式碼片段會讓 `@x` 只保留 `'ab'`。 空間不足，無法保留補充字元。
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
使用 SC 定序時，`CONVERT` 的行為類似 `CAST`。
  
## <a name="compatibility-support"></a>相容性支援
在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，除非用於計算資料行運算式，否則 **time** 和 **datetime2** 資料類型上之 CAST 和 CONVERT 作業的預設樣式為 121。 若為計算資料行，預設樣式為 0。 當您建立計算資料行、將它們用於包含自動參數化的查詢或用於條件約束定義時，這種行為就會影響計算資料行。
  
在相容性層級高於及等於 110 的情況下，**time** 和 **datetime2** 資料類型上之 CAST 和 CONVERT 作業的預設樣式一律為 121。 如果您的查詢仰賴舊的行為，請使用低於 110 的相容性層級，或在受影響的查詢中明確指定 0 樣式。
  
將資料庫升級為相容性層級高於及等於 110 並不會變更已經儲存至磁碟的使用者資料。 您必須依適當情況手動更正這項資料。 例如，如果您使用了 SELECT INTO，根據包含上述計算資料行運算式的來源建立資料表，系統就會儲存資料 (使用樣式 0) 而非計算資料行定義本身。 您必須手動將這項資料更新為符合樣式 121。
  
## <a name="BKMK_examples"></a> 範例  
  
### <a name="a-using-both-cast-and-convert"></a>A. 使用 CAST 和 CONVERT  
每個範例都會擷取定價第一位數是 `3` 的產品名稱，且會將它們的 `ListPrice` 轉換成 `int`。
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. 搭配算術運算子來使用 CAST  
下列範例會將年度目前的總銷售額 (`Computed`) 除以佣金百分比 (`SalesYTD`) 來計算單一資料行 (`CommissionPCT`)。 這個結果在進位到最近的整數之後，會轉換成 `int` 資料類型。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. 利用 CAST 來串連  
下列範例會利用 CAST 來串連非字元運算式。 使用 AdventureWorksDW。
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. 利用 CAST 來產生其他可讀取的文字  
下列範例會利用 SELECT 清單中的 CAST，將 `Name` 資料行轉換成 **char(10)** 資料行。 使用 AdventureWorksDW。
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. 搭配 LIKE 子句使用 CAST  
下列範例會將 `money` 資料行 `SalesYTD` 轉換成 `int`，再轉換成 `char(20)` 資料行，以便能夠搭配 `LIKE` 子句來使用。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. 搭配具類型的 XML 來使用 CONVERT 或 CAST  
下列幾個範例會顯示如何使用 [XML 資料類型和資料行 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)，利用 CONVERT 來轉換成 XML 類型。
  
這個範例會將含有空格、文字和標記的字串轉換成 XML 類型，且會移除所有無意義的空格 (節點之間的界限空格)：
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
這個範例會將含有空格、文字和標記的類似字串轉換成 XML 類型，且會保留所有無意義的空格 (節點之間的界限空格)：
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
這個範例會將含有空格、文字和標記的字串轉換成 XML 類型：
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
如需其他範例，請參閱[建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)。
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. 搭配 datetime 資料使用 CAST 和 CONVERT  
下列範例會顯示目前的日期和時間、使用 `CAST` 將目前的日期和時間變更成字元資料類型，然後使用 `CONVERT` 以 `ISO 8901` 格式顯示日期和時間。
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
下列範例幾乎是上一個範例的相反操作。 這個範例會將日期和時間顯示成字元資料、使用 `CAST` 將字元資料變更成 `datetime` 資料類型，然後使用 `CONVERT` 將字元資料變更成 `datetime` 資料類型。
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. 搭配二進位和字元資料使用 CONVERT  
下列範例將顯示使用不同樣式來轉換二進位和字元資料的結果。
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
下列範例示範樣式 1 如何強制截斷結果。 截斷是透過在結果中包含字元 0x 來產生。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
下列範例示範樣式 2 不會截斷結果，因為字元 0x 沒有包含在結果中。  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
將字元值 'Name' 轉換成二進位值。  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. 轉換 date 和 time 資料類型  
下列範例示範 date、time 和 datetime 資料類型的轉換。
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. 使用 CAST 和 CONVERT  
此範例會擷取標價第一位數是 `3` 的產品名稱，且會將它們的 `ListPrice` 轉換成 **int**。使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
此範例會示範相同的查詢，但使用的是 CONVERT 而非 CAST。 使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. 搭配算術運算子來使用 CAST  
下列範例會將產品單價 (`UnitPrice`) 除以折扣百分比 (`UnitPriceDiscountPct`) 來計算單一資料行。 這個結果在進位到最近的整數之後，會轉換成 `int` 資料類型。 使用 AdventureWorksDW。
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. 搭配 LIKE 子句使用 CAST  
下列範例會將 **money** 資料行 `ListPrice` 轉換成 **int** 類型，再轉換成 **char(20)** 類型，以便能夠搭配 LIKE 子句使用。 使用 AdventureWorksDW。
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. 搭配 datetime 資料使用 CAST 和 CONVERT  
下列範例會顯示目前的日期和時間，使用 CAST 將目前的日期和時間變更成字元資料類型，然後使用 CONVERT 來以 ISO 8601 格式顯示日期和時間。 使用 AdventureWorksDW。
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
下列範例幾乎是上一個範例的相反操作。 此範例會將日期和時間顯示成字元資料，使用 CAST 將字元資料變更成 **datetime** 資料類型，然後使用 CONVERT 將字元資料變更成 **datetime** 資料類型。 使用 AdventureWorksDW。
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>另請參閱
 [資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
 [撰寫國際通用的 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
