---
title: SUBSTRING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3dea4c451c82a17e29a6d47028a35e3e61bd27ec
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/15/2019
ms.locfileid: "54298965"
---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [請提供您對 SQL Docs 目錄的意見反應！](https://aka.ms/sqldocsurvey)

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中傳回字元、二進位、文字或影像運算式的一部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是 **character**、**binary**、**text**、**ntext** 或 **image** [expression](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 *start*  
 這是指定傳回之字元開始的整數或 **bigint** 運算式。 (編號是以 1 為基礎，這表示運算式中的第一個字元為 1)。 如果 *start* 小於 1，傳回的運算式將會從 *expression* 內指定的第一個字元開始。 在此情況下，傳回的字元數會是 *start* + *length* 的總和 -1 或是 0 (以最大值為準)。 如果 *start* 大於值運算式中的字元數，則會傳回長度為零的運算式。  
  
 *length*  
 這是一個正整數，或是指定將傳回之 *expression* 字元數的 **bigint** 運算式。 如果 *length* 是負數，則會產生錯誤並結束此陳述式。 如果 *start* 和 *length* 的總和大於 *expression* 中的字元數，則會傳回從 *start* 開始的整個值運算式。  
  
## <a name="return-types"></a>傳回類型  
 如果 *expression* 是其中一個支援的字元資料類型，就會傳回字元資料。 如果 *expression* 是支援的 **binary**資料類型之一，就會傳回二進位資料。 傳回的字串與指定運算式的類型相同，但下表所顯示者例外。  
  
|指定的運算式|傳回類型|  
|--------------------------|-----------------|  
|**char**/**varchar**/**text**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binary**/**varbinary**/**image**|**varbinary**|  
  
## <a name="remarks"></a>Remarks  
 *start* 和 *length* 的值必須指定為字元數 (適用於 **ntext****char**或 **varchar** 資料類型) 和位元組數 (適用於 **text**’**image**、**binary**或 **varbinary** 資料類型)。  
  
 當 *start* 或 *length* 包含大於 2147483647 的值時，*expression* 必須是 **varchar(max)** 或 **varbinary(max)**。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用增補字元 (SC) 定序時，*start* 和 *length* 會將 *expression* 中的每個代理字組算成單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-substring-with-a-character-string"></a>A. 使用 SUBSTRING 與字元字串  
 下列範例會顯示如何只傳回字元字串的一部分。 從 `sys.databases` 資料表，此查詢會傳回第一個資料行中的系統資料庫名稱、第二個資料行中的資料庫第一個字母，以及最後一個資料行中的第三和第四個字元。  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|NAME |Initial |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |st |
|tempdb  |t  |mp |
|model   |m  |de |
|msdb    |m  |db |


  
 以下是如何顯示字串常數 `abcdef` 的第二、第三和第四個字元。  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. 使用 SUBSTRING 與 text、ntext 以及 image 資料  
  
> [!NOTE]  
>  若要執行下列範例，您必須安裝 **pubs** 資料庫。  
  
 下列範例示範如何從 `pubs` 資料庫之 `pub_info`資料表的各個 **text** 和 **image**資料行傳回前 10 個字元。 **text** 資料會當成 **varchar** 傳回，且 **image** 資料會當成 **varbinary** 傳回。  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 下列範例會顯示 **text** 和 **ntext** 資料的 SUBSTRING 效果。 首先，這個範例會在名稱為 `pubs` 的 `npub_info` 資料庫中，建立一份新的資料表。 其次，這個範例會從 `pr_info` 資料行的前 80 個字元中，建立 `npub_info` 資料表的 `pub_info.pr_info` 資料行，再加入 `ü` 來作為第一個字元。 最後，`INNER JOIN` 會擷取所有簽發者識別碼，以及 **text** 和 **ntext** 發行者資訊資料行的 `SUBSTRING`。  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>C. 使用 SUBSTRING 與字元字串  
 下列範例會顯示如何只傳回字元字串的一部分。 這個查詢會從 `dbo.DimEmployee` 資料表中，傳回第一個資料行中的姓氏，而第二資料行只有第一個首字母。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 下列範例會顯示如何傳回字串常數 `abcdef` 的第二、第三和第四個字元。  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>另請參閱  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


