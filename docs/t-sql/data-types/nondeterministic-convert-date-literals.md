---
description: 將常值日期字串轉換成 DATE 值的非決定性轉換
title: 日期常值的非決定性轉換 | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aeb2953d2e955a8094e17ac64040662ff3e7804f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466099"
---
# <a name="nondeterministic-conversion-of-literal-date-strings-into-date-values"></a>將常值日期字串轉換成 DATE 值的非決定性轉換

允許將您的 CHARACTER 字串轉換成 DATE 資料類型時請務必小心。 原因是這類轉換通常都是「非決定性」。

您可以透過說明 [SET LANGUAGE](../statements/set-language-transact-sql.md) 和 [SET DATEFORMAT](../statements/set-dateformat-transact-sql.md) 的設定來控制這些非決定性轉換。



## <a name="set-language-example-month-name-in-polish"></a>SET LANGUAGE 範例：波蘭文的月份名稱

- `SET LANGUAGE Polish;`

字元字串可以是月份的名稱。 但名稱是英文、波蘭文、克羅埃西亞文或其他語言？ 此外，使用者的工作階段是否會設為正確對應語言？

例如，假設一個單字 _listopad_，此為月份的名稱。 但該月份會根據 SQL 系統相信其正在使用的語言而有所不同：
- 若是波蘭文，則 _listopad_ 可翻譯成 11 月 (即英文中的 _November_)。
- 若是克羅埃西亞文，則 _listopad_ 可翻譯成 10 月 (即英文中的 _October_)。

#### <a name="code-example-of-set-language"></a>SET LANGUAGE 的程式碼範例

```sql
--SELECT alias FROM sys.syslanguages ORDER BY alias;

DECLARE @yourInputDate  NVARCHAR(32) = '28 listopad 2018';

SET LANGUAGE Polish;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Polish];

SET LANGUAGE Croatian;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Croatian];

SET LANGUAGE English;


/***  Actual output:  For the two months, note the 11 versus the 10.
SL_Polish
2018-11-28

SL_Croatian
2018-10-28
**_/
```



## <a name="set-dateformat-example"></a>SET DATEFORMAT 範例

- `SET DATEFORMAT dmy;`

上述 _ *dmy** 格式表示範例日期字串 '01-03-2018' 會解譯為「2018 年 3 月的第一天」。

若改為指定 **mdy**，則相同的 '01-03-2018' 字串就會表示「2018 年 1 月的第三天」。

若指定 **ymd**，則無法保證輸出結果為何。 '2018' 的數值對天來說太大了。
<!--
The preceding claim of "no guarantee" might be incorrect, in the minds of the SQL query engine Developer team?
-->

#### <a name="specific-countries"></a>特定國家/地區

在日本和中國，會使用 **ymd** 的 DATEFORMAT。 格式部分為由大單位至小單位的合理順序。 因此，此格式的排序狀況相當良好。 此格式被視為是「國際」格式。 其為國際格式的原因是四位數年份並不明確，且目前在地球上沒有任何國家/地區使用古老的 **ydm** 格式。

在其他國家/地區 (例如德國和法國) 中，DATEFORMAT 為 **dmy**，其表示 **'dd-mm-yyyy'**。 **dmy** 格式的排序狀況並不良好，但仍然是由小單位至大單位的合理順序。

美國和密克羅尼西亞聯邦是使用 **mdy** 的唯二國家/地區，此格式無法排序。 格式的混合順序符合語音上說明日期的模式。

#### <a name="code-example-of-set-dateformat-mdy-versus-dmy"></a>SET DATEFORMAT 的程式碼範例：*mdy* 與 *dmy*

下列 Transact-SQL 程式碼範例會使用相同日期字元字串，搭配三種不同的 DATEFORMAT 設定。 執行程式碼會產生如註解中的輸出：

```sql
DECLARE @yourDateString NVARCHAR(10) = '12-09-2018';
PRINT @yourDateString + '  = the input.';

SET DATEFORMAT dmy;
SELECT CONVERT(DATE, @yourDateString) AS [DMY-Interpretation-of-input-format];

SET DATEFORMAT mdy;
SELECT CONVERT(DATE, @yourDateString) AS [MDY-Interpretation-of-input-format];

SET DATEFORMAT ymd;
SELECT CONVERT(DATE, @yourDateString) AS [YMD-Interpretation--?--NotGuaranteed];


/***  Actual output:
12-09-2018  = the input.

DMY-Interpretation-of-input-format
2018-09-12

MDY-Interpretation-of-input-format
2018-12-09

YMD-Interpretation--?--NotGuaranteed
2018-12-09
**_/
```

在上述程式碼範例中，最後一個範例的格式 _ *ymd** 與輸入字串不符。 輸入字串之第三個節點表示對天來說太大的數值。 Microsoft 無法保證這類不相符所產生的輸出值。

#### <a name="convert-offers-explicit-codes-for-_deterministic_-control-of-date-formats"></a>CONVERT 可提供「決定性」日期格式控制的明確程式碼

我們的 CAST 和 CONVERT 文件文章會列出您可以與 CONVERT 函式「決定性地」控制日期轉換搭配使用的明確程式碼。 每個月該文章都擁有我們最高的頁面瀏覽次數。

- [CAST 與 CONVERT (Transact-SQL)：日期與時間樣式](../functions/cast-and-convert-transact-sql.md#date-and-time-styles)
- [CAST 與 CONVERT (Transact-SQL)：某些日期時間轉換不具決定性](../functions/cast-and-convert-transact-sql.md#certain-datetime-conversions-are-nondeterministic)



## <a name="compatibility-level-90-and-above"></a>相容性層級 90 及以上

在 SQL Server 2000 中，相容性層級為 80。 針對層級設定 80 或以下，隱含日期轉換具決定性。

從 SQL Server 2005 和其相容性層級 90 開始，隱含日期轉換不具決定性。 從層級 90 開始，日期轉換依存於 SET LANGUAGE 和 SET DATEFORMAT。

#### <a name="unicode"></a>Unicode

<!-- The next live sentence needs an explanatory example!  N'somethingHere?'.
-->
非 Unicode 字元資料與定序之間的轉換也被視為非決定性。



## <a name="see-also"></a>另請參閱

- [設定工作階段語言](../../relational-databases/collations/set-a-session-language.md)
- [日期和時間資料類型與函數 (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md)
- [FORMAT (Transact-SQL)](../functions/format-transact-sql.md)
- [ISDATE (Transact-SQL)](../functions/isdate-transact-sql.md)



<!--
This new article is linked-to by the following articles (at least initially on 2018/11/19).....
...
* docs/relational-databases/views/create-indexed-views.md
* docs/relational-databases/indexes/indexes-on-computed-columns.md
* docs/t-sql/functions/cast-and-convert-transact-sql.md
...
As a reaction to public PR 1279, this approach of creating a new article to link to is a better alternative than a docs/includes/ approach.
GeneMi (MightyPen), 2018/11/19
-->

