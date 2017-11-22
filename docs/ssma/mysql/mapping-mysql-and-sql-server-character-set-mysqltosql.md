---
title: "MySQL 及 SQL Server 字元對應設定 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6953025addea83b247e8f1c03fef4bdd24d27147
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>MySQL 及 SQL Server 字元對應設定 (MySQLToSQL)
字元集 (Charset) 可以指定之 MySQL 字元資料類型、 運算式和常值。  
  
## <a name="charset-mapping"></a>字元集對應  
字元集對應會定義每個 MySQL 字元集和字元資料類型轉換期間使用。 它會指定如何將轉換的特定字元集的字元字串資料類型：  
  
-   為國家 （地區） 的 SQL Server 字元類型 (NCHAR/NVARCHAR)，或  
  
-   與一般 SQL Server 字元類型 (CHAR/VARCHAR)  
  
1.  **國家 （地區)**目標資料庫字元資料類型為：  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **一般**目標資料庫字元資料類型為：  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  型別對應只可對應至**national**字元資料類型。 MySQL 字元資料類型根據型別對應轉換之後，會套用字元集對應。  
  
> [!NOTE]  
> 字元集對應定義的中繼資料物件總管 中的每個節點層級上，而且代表從 MySQL 閱讀關於所有字元集。  
  
## <a name="charset-mapping-on-different-node-levels"></a>字元集對應上不同節點層級  
字元集對應會有所不同在不同節點層級，也就是：  
  
1.  在根中繼資料節點層級  
  
2.  在資料庫、 類別和物件節點層級  
  
> [!NOTE]  
> 選取要編輯字元集對應，這個索引標籤包含三個按鈕，不論是在不同節點層級上的對應。  
>   
> 其中包括：  
>   
> 1.  **適用於：**適用於由使用者啟用只有在字元集對應是編輯而尚未儲存所做的變更。  
> 2.  **取消：**取消使用者所做的變更。 字元集對應編輯，但不是會儲存時，取得啟用按鈕。  
> 3.  **重設預設值：**重設為預設值的所有對應。  
  
1.  **在根層級中繼資料節點：**字元集對應格線包含具有個別的資料行的每個字元集的字集方格。 方格的資料行如下：  
  
    1.  名為方格的第一個資料行**字元集名稱**包含字元集的名稱。  
  
    2.  第二個名為**Charset 描述**包含字元集的描述。  
  
    3.  第三個資料行標題，**目標字元集類型**包含的特定字元集的對應設定。 此資料行的值如下：  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 預設值的特定字元集 CHAR/VARCHAR 或 NCHAR/NVARCHAR 之後的前置詞 '(default)'。  
  
    字元集之間的對應的 MySQL 資料庫和目標資料庫上根中繼資料節點層級如下所示：  
  
    ||||  
    |-|-|-|  
    |**字元集名稱**|**Charset 描述**|**目標字元集類型 （預設值）**|  
    |big5|Big5 繁體中文|NCHAR/NVARCHAR （預設值）|  
    |dec8|DEC 西方語系|CHAR/VARCHAR （預設值）|  
    |cp850|DOS 西方語系|CHAR/VARCHAR （預設值）|  
    |hp8|HP 西方語系|CHAR/VARCHAR （預設值）|  
    |koi8r|KOI8 R Relcom 俄文|CHAR/VARCHAR （預設值）|  
    |拉丁文 1|cp1252 西方語系|CHAR/VARCHAR （預設值）|  
    |latin2|ISO 8859-2 中歐語系|CHAR/VARCHAR （預設值）|  
    |swe7|7 位元瑞典文|CHAR/VARCHAR （預設值）|  
    |ascii|US ASCII|CHAR/VARCHAR （預設值）|  
    |ujis|EUC-JP 日文|NCHAR/NVARCHAR （預設值）|  
    |sjis|日文 shift JIS|NCHAR/NVARCHAR （預設值）|  
    |希伯來文|ISO 8859-8 希伯來文|CHAR/VARCHAR （預設值）|  
    |tis620|TIS620 泰文|CHAR/VARCHAR （預設值）|  
    |euckr|EUC-KR 韓文|NCHAR/NVARCHAR （預設值）|  
    |koi8u|KOI8 U 烏克蘭文|CHAR/VARCHAR （預設值）|  
    |gb2312|GB2312 簡體中文|NCHAR/NVARCHAR （預設值）|  
    |希臘文|ISO 8859-7 希臘文|CHAR/VARCHAR （預設值）|  
    |cp 1250|Windows 中歐語系|CHAR/VARCHAR （預設值）|  
    |（gbk)|GBK 簡體中文|NCHAR/NVARCHAR （預設值）|  
    |latin5|ISO 8859-9 土耳其文|CHAR/VARCHAR （預設值）|  
    |armscii8|ARMSCII 8 亞美尼亞文|CHAR/VARCHAR （預設值）|  
    |utf8|Utf-8 Unicode|NCHAR/NVARCHAR （預設值）|  
    |ucs2|Ucs-2 Unicode|NCHAR/NVARCHAR （預設值）|  
    |cp866|DOS 俄文|CHAR/VARCHAR （預設值）|  
    |keybcs2|DOS Kamenicky 捷克文-斯洛伐克文|CHAR/VARCHAR （預設值）|  
    |macce|Mac 中歐語系|CHAR/VARCHAR （預設值）|  
    |macroman|Mac 西方語系|CHAR/VARCHAR （預設值）|  
    |cp852|DOS 中央歐語系|CHAR/VARCHAR （預設值）|  
    |latin7|ISO 8859-13 波羅的海文|CHAR/VARCHAR （預設值）|  
    |cp 1251|Windows 斯拉夫文|CHAR/VARCHAR （預設值）|  
    |cp 1256|Windows 阿拉伯文|CHAR/VARCHAR （預設值）|  
    |cp 1257|Windows 波羅的海文|CHAR/VARCHAR （預設值）|  
    |binary|二進位虛擬字元集|CHAR/VARCHAR （預設值）|  
    |geostd8|GEOSTD8 喬治亞文|CHAR/VARCHAR （預設值）|  
    |cp932|對於 Windows 日文 SJIS|NCHAR/NVARCHAR （預設值）|  
    |eucjpms|對於 Windows 日文 UJIS|NCHAR/NVARCHAR （預設值）|  
  
2.  **在資料庫、 類別或物件節點層級：**資料庫、 類別或物件節點層級中，字元集對應格線包含根中繼資料節點層級上相同的資料列 viz。:  
  
    1.  方格標題的第一個資料行**字元設定名稱**包含字元集的名稱。  
  
    2.  第二個資料行標題，**字元設定描述**包含字元集的描述。  
  
    3.  唯一的差別是方格的第三個資料行中的值。 第三個資料行標題，**目標資料型別**包含的特定字元集的對應設定。 資料行的值如下：  
  
        -   繼承 （CHAR/VARCHAR 或 NCHAR/NVARCHAR）  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   在字元集對應 MySQL 資料庫與資料庫、 類別和物件節點層級上的目標資料庫中的預設值在每個資料行的根目錄以外的層級上的特定字元集**目標資料型別**應該 '繼承'。  
> -   在方格中，值**繼承**後置字元為 '(CHAR/VARCHAR)' 或 '(NCHAR/NVARCHAR)' 根據哪個值繼承自父系由這個特定的字元集。  
  
