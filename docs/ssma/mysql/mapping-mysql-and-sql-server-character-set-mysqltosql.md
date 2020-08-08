---
title: 將 MySQL 和 SQL Server 字元集對應 (MySQLToSQL) |Microsoft Docs
description: 瞭解如何在 SSMA for MySQL 中指定要在字元資料類型轉換期間使用的 MySQL 字元資料類型、運算式和常值的字元集。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7782a8853e1b17ecba0950e647d1335758b998af
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935277"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>對應 MySQL 和 SQL Server 字元集 (MySQLToSQL)
字元集 (字元集) 可以針對 MySQL 字元資料類型、運算式和常值指定。  
  
## <a name="charset-mapping"></a>字元集對應  
字元集對應會針對每個 MySQL 字元集定義，並在字元資料類型轉換期間使用。 它會指定如何轉換特定字元集的字元字串資料類型：  
  
-    (NCHAR/NVARCHAR) 的國家 SQL Server 字元類型，或  
  
-   若為一般 SQL Server 字元類型 (CHAR/VARCHAR)   
  
1.  **國家**目標資料庫字元資料類型如下：  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **一般**目標資料庫字元資料類型為：  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  類型對應只允許對應至**國家**字元資料類型。 當 MySQL 字元資料類型根據類型對應進行轉換之後，就會套用字元集對應。  
  
> [!NOTE]  
> 字元集對應可以在中繼資料物件瀏覽器的每個節點層級上定義，並代表從 MySQL 讀取的所有字元集。  
  
## <a name="charset-mapping-on-different-node-levels"></a>不同節點層級上的字元集對應  
字元集對應會在不同的節點層級上有所不同，亦即：  
  
1.  在根中繼資料節點層級上  
  
2.  在資料庫、類別和物件節點層級上  
  
> [!NOTE]  
> 選取來編輯字元集對應的索引標籤包含三個按鈕，而不論不同節點層級上的對應。  
>   
> 其中包括：  
>   
> 1.  **適用：** 套用使用者所做的變更，只有在已編輯和尚未儲存字元集對應時才會啟用。  
> 2.  **取消：** 取消使用者所做的變更。 編輯字元集對應但未儲存時，會啟用此按鈕。  
> 3.  **重設為預設值：** 將所有對應重設為預設值。  
  
1.  **在根中繼資料節點層級上：** [字元集對應] 方格包含 [字元集] 方格，其中每個字元集都有個別的資料行。 方格的資料行為：  
  
    1.  方格的第一個資料行名為 [**字元集名稱**]，其中包含字元集名稱。  
  
    2.  第二個命名**字元集描述**包含字元集描述。  
  
    3.  第三個標題為 [**目標字元集類型**] 的資料行包含特定字元集的對應設定。 此資料行的值為：  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定字元集的預設值在 CHAR/VARCHAR 或 NCHAR/NVARCHAR 之後具有前置詞 ' (預設) '。  
  
    以下提供 MySQL 資料庫和根中繼資料節點層級上的目標資料庫之間的字元集對應：  
  
    |字元集名稱|字元集描述| (預設) 的目標字元集類型|  
    |-|-|-|  
    |big5|繁體中文的 Big5|NCHAR/NVARCHAR (預設) |  
    |dec8|DEC 西歐|CHAR/VARCHAR (預設值) |  
    |cp850|DOS 西歐|CHAR/VARCHAR (預設值) |  
    |hp8|HP 西歐|CHAR/VARCHAR (預設值) |  
    |koi8r|KOI8-R-R Relcom 俄文|CHAR/VARCHAR (預設值) |  
    |拉丁1|cp1252 西歐|CHAR/VARCHAR (預設值) |  
    |latin2|ISO 8859-2 中部歐洲|CHAR/VARCHAR (預設值) |  
    |swe7|7位瑞典文|CHAR/VARCHAR (預設值) |  
    |ascii|US ASCII|CHAR/VARCHAR (預設值) |  
    |ujis|EUC-JP 日文|NCHAR/NVARCHAR (預設) |  
    |sjis|Shift-jis 日文|NCHAR/NVARCHAR (預設) |  
    |希伯來文|ISO 8859-8 希伯來文|CHAR/VARCHAR (預設值) |  
    |tis620|TIS620 泰文|CHAR/VARCHAR (預設值) |  
    |euckr|EUC-韓國韓文|NCHAR/NVARCHAR (預設) |  
    |koi8u|KOI8-R-U 烏克蘭|CHAR/VARCHAR (預設值) |  
    |gb2312|GB2312 簡體中文|NCHAR/NVARCHAR (預設) |  
    |希臘文|ISO 8859-7 希臘文|CHAR/VARCHAR (預設值) |  
    |cp 1250|Windows Central 歐洲|CHAR/VARCHAR (預設值) |  
    |gbk|簡體中文 GBK|NCHAR/NVARCHAR (預設) |  
    |latin5|ISO 8859-9 土耳其文|CHAR/VARCHAR (預設值) |  
    |armscii8|ARMSCII-8 亞美尼亞文|CHAR/VARCHAR (預設值) |  
    |utf8|UTF-8 Unicode|NCHAR/NVARCHAR (預設) |  
    |ucs2|UCS-2 Unicode|NCHAR/NVARCHAR (預設) |  
    |cp866|DOS 俄文|CHAR/VARCHAR (預設值) |  
    |keybcs2|DOS Kamenicky 捷克文-斯洛伐克文|CHAR/VARCHAR (預設值) |  
    |macce|Mac 中部歐洲|CHAR/VARCHAR (預設值) |  
    |macroman|Mac 西歐|CHAR/VARCHAR (預設值) |  
    |cp852|DOS 中部歐洲|CHAR/VARCHAR (預設值) |  
    |latin7|ISO 8859-13 波羅的海文|CHAR/VARCHAR (預設值) |  
    |cp 1251|Windows 斯拉夫文|CHAR/VARCHAR (預設值) |  
    |cp 1256|Windows 阿拉伯文|CHAR/VARCHAR (預設值) |  
    |cp 1257|Windows 波羅的海文|CHAR/VARCHAR (預設值) |  
    |BINARY|二進位虛擬字元集|CHAR/VARCHAR (預設值) |  
    |geostd8|GEOSTD8 的格魯吉亞文|CHAR/VARCHAR (預設值) |  
    |cp932|適用于 Windows 日文的 SJIS|NCHAR/NVARCHAR (預設) |  
    |eucjpms|適用于 Windows 日文的 UJIS|NCHAR/NVARCHAR (預設) |  
  
2.  **在 [資料庫]、[類別] 或 [物件] 節點層級上：** 在 [資料庫]、[類別目錄] 或 [物件節點層級] 的 [字元集對應] 方格中，包含與根中繼資料節點層級（視覺效果）相同的資料列。  
  
    1.  標題為之方格的第一個資料行，[**字元集名稱**] 包含字元集名稱。  
  
    2.  第二個數據行標題為 [**字元集描述**]，其中包含 [字元集描述]。  
  
    3.  唯一的差異在於方格第三個數據行中的值。 第三個標題為 [**目標資料類型**] 的欄位包含特定字元集的對應設定。 資料行的值為：  
  
        -   繼承 (CHAR/VARCHAR 或 NCHAR/NVARCHAR)   
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   在資料庫、類別和物件節點層級上的 MySQL 資料庫與目標資料庫之間的字元集對應中，**資料行目標資料類型**之根以外的每個層級上，特定字元集的預設值都應該是「繼承」。  
> -   在方格中，**繼承**的值會以 ' (CHAR/VARCHAR) ' 或 ' (NCHAR/NVARCHAR) ' 作為尾碼，視此特定字元集繼承自父系的值而定。  
  
