---
title: "子字串 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs: TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
caps.latest.revision: "65"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2c78c77953dc60bdcd73ec29ba542a12478783fb
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中傳回字元、二進位、文字或影像運算式的一部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是**字元**，**二進位**，**文字**， **ntext**，或**映像**[運算式](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *start*  
 是整數或**bigint**運算式，指定開始傳回的字元的位置。 （編號為 1 的基礎，代表運算式中的第一個字元是 1）。 如果*啟動*小於 1，傳回的運算式會在中指定的第一個字元開始*運算式*。 在此情況下，傳回字元的數目會最大值的總和的*啟動* + *長度*-1 或 0。 如果*啟動*數目大於值運算式中的字元，長度為零則會傳回運算式。  
  
 *長度*  
 這是一個正整數或**bigint**運算式，指定的字元數*運算式*會傳回。 如果*長度*是負數，則會產生錯誤並終止陳述式。 如果總和*啟動*和*長度*中的字元數大於*運算式*、 開始的整個值運算式*啟動*傳回。  
  
## <a name="return-types"></a>傳回類型  
 如果傳回的字元資料*運算式*是其中一個支援的字元資料類型。 傳回二進位資料，如果*運算式*是其中一個支援**二進位**資料型別。 傳回的字串與指定運算式的類型相同，但下表所顯示者例外。  
  
|指定的運算式|傳回類型|  
|--------------------------|-----------------|  
|**char**/**varchar**/**text**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binary**/**varbinary**/**image**|**varbinary**|  
  
## <a name="remarks"></a>備註  
 值*啟動*和*長度*中的字元數必須指定**ntext**， **char**，或**varchar**資料類型與位元組**文字**，**映像**，**二進位**，或**varbinary**資料型別。  
  
 *運算式*必須**varchar （max)**或**varbinary （max)**時*啟動*或*長度*包含大於 2147483647 的值。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用增補字元 (SC) 定序，同時*啟動*和*長度*中的每個 surrogate 字組計算*運算式*做為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-substring-with-a-character-string"></a>A. 使用 SUBSTRING 與字元字串  
 下列範例會顯示如何只傳回字元字串的一部分。 從`sys.databases`資料表，此查詢會傳回系統資料庫名稱中第一個資料行，第二個資料行中的資料庫和最後一個資料行中的第三個和第四個字元的第一個字母。  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |Initial |ThirdAndFourthCharacters|
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
>  若要執行下列的範例，您必須安裝**pubs**資料庫。  
  
 下列範例示範如何從每個傳回前 10 個字元**文字**和**映像**中的資料行`pub_info`資料表`pubs`資料庫。 **文字**資料以傳回**varchar**，和**映像**資料以傳回**varbinary**。  
  
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
  
 下列範例示範在兩者的 SUBSTRING 效果**文字**和**ntext**資料。 首先，這個範例會在名稱為 `pubs` 的 `npub_info` 資料庫中，建立一份新的資料表。 其次，這個範例會從 `pr_info` 資料行的前 80 個字元中，建立 `npub_info` 資料表的 `pub_info.pr_info` 資料行，再加入 `ü` 來作為第一個字元。 最後，`INNER JOIN`擷取所有簽發者識別碼和`SUBSTRING`兩者的**文字**和**ntext**發行者資訊資料行。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
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
  
 下列範例示範如何傳回第二、 第三和第四個字元的字串常數`abcdef`。  
  
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
 [權限 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


