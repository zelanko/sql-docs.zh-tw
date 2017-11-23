---
title: "常數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aae955a177f637e3c359eabf02679025cbecdb3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="constants-transact-sql"></a>常數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

常數也稱為常值或純量值，是一個代表特定資料值的符號。 常數的格式會隨著所代表之值的資料類型而不同。
  
## <a name="character-string-constants"></a>字元字串常數
字元字串常數含括在單引號中，其中包括英數字元 (a-z、A-Z 和 0-9) 以及特殊字元，如驚歎號 (!)、@ 記號 (@) 和數字符號 (#)。 除非利用 COLLATE 子句來指定定序，否則，字元字串常值會被指派目前資料庫的預設定序。 使用者所輸入的字元字串是透過電腦的字碼頁來評估的，必要的話，它們會轉換成資料庫預設字碼頁。
  
如果連接的 QUOTED_IDENTIFIER 選項已設為 OFF，就可以將字元字串括在雙引號內，但 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者和 ODBC 驅動程式會自動使用 SET QUOTED_IDENTIFIER ON。 我們建議您使用單引號。
  
如果括在單引號中的字元字串包含內嵌雙引號，請用兩個單引號來表示內嵌的單引號。 內嵌在雙引號內的字串，不需要如此。
  
以下是字元字串的範例：
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
空字串用不含任何東西的兩個單引號來表示。 在 6.x 相容性模式中用單一空格來表示空字串。
  
字元字串常數支援增強型定序。
  
> [!NOTE]  
>  字元常數大於 8000 個位元組的型別為**varchar （max)**資料。  
  
## <a name="unicode-strings"></a>Unicode 字串
Unicode 字串的格式類似於字元字串，但前面附加了 N 識別碼 (N 代表 SQL-92 標準中的國家 (地區) 語言)。 N 前置詞必須是大寫。 例如，'Michél' 是一個字元常數，N'MICHÉL ' 則是 Unicode 常數時。 Unicode 常數會解譯成 Unicode 資料，並不會用字碼頁來評估。 Unicode 常數有定序。 這個定序主要用來控制比較和區分大小寫。 除非利用 COLLATE 子句來指定定序，否則，Unicode 常數會被指派目前資料庫的預設定序。 Unicode 資料是利用每個字元 2 位元組來儲存的，而不是字元資料的每個字元 1 個位元組。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
Unicode 字串常數支援增強型定序。
  
> [!NOTE]  
>  大於 8000 個位元組的型別為 Unicode 常數**nvarchar （max)**資料。  
  
## <a name="binary-constants"></a>二進位常數
二進位常數的前置詞是 `0x`，它是一個十六進位數字字串。 它們不需加上引號。
  
以下是二進位字串的範例：
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  大於 8000 個位元組的型別為二進位常數**varbinary （max)**資料。  
  
## <a name="bit-constants"></a>位元常數
**位元**常數由數字 0 或 1，並不會以引號括住。 如果使用大於 1 的數字，它會轉換成 1。
  
## <a name="datetime-constants"></a>datetime 常數
**datetime**常數利用特定的格式，括在單引號中的字元日期值來表示。
  
以下是範例的**datetime**常數：
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
日期時間常數的範例如下：
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>整數常數
**整數**常數由未以引號括住，而且不包含小數點的數字的字串。 **整數**常數必須是整數; 不能包含小數點。
  
以下是範例的**整數**常數：
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>十進位常數
**十進位**常數用沒有加上引號且包含小數點的數字的字串來表示。
  
以下是範例的**十進位**常數：
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>float 和 real 常數
**float**和**真實**常數利用科學記號標記法來表示。
  
以下是範例的**float**或**真實**值：
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>money 常數
**money**常數會以貨幣符號做為前置詞與可選擇小數點的數字的字串表示。 **money**常數不加引號。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會強制執行任何一種分組規則，如在代表貨幣的字串中，每三位數插入一個逗號 (,)。
  
> [!NOTE]  
>  在指定的 「 逗號都會被忽略任何地方**money**常值。  
  
以下是範例的**money**常數：
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>uniqueidentifier 常數
**uniqueidentifier**常數是代表 GUID 的字串。 您可以依照字元或二進位字串格式來指定它們。
  
下列範例指定相同的 GUID：
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>指定負數和正數  
若要指示數字為正數或負數，套用 **+** 或 **-** 數值常數的一元運算子。 這會建立一個代表帶正負號的數值之數值運算式。 數值常數時，用正數 **+** 或 **-** 一元運算子不會套用。
  
簽署**整數**運算式：  
  
```sql
+145345234
-2147483648
```
簽署**十進位**運算式：  
  
```sql
+145345234.2234
-2147483648.10
```
  
簽署**float**運算式：  
  
```sql
+123E-3
-12E5
```
  
簽署**money**運算式：  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>增強型定序  
SQL Server 支援字元及支援增強型定序的 Unicode 字串常數。 如需詳細資訊，請參閱[COLLATE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)子句。
  
## <a name="see-also"></a>另請參閱
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  
