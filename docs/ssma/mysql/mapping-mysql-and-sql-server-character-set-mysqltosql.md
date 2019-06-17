---
title: 對應 MySQL 和 SQL Server 字元集設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312365"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>對應 MySQL 和 SQL Server 字元集 (MySQLToSQL)
可以針對 MySQL 字元資料型別、 運算式和常值中指定字元集 （字元集）。  
  
## <a name="charset-mapping"></a>字元集對應  
字元集對應會定義每個 MySQL 字元集，且在字元資料類型轉換期間使用。 它會指定如何將轉換的特定字元集的字元字串資料類型：  
  
-   為國家的 SQL Server 字元類型 (NCHAR/NVARCHAR)，或  
  
-   一般的 SQL Server 字元類型 (CHAR/VARCHAR)  
  
1.  **national**目標資料庫字元資料類型為：  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **一般**目標資料庫字元資料類型為：  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  只允許類型對應的對應**國家**字元資料類型。 MySQL 字元資料類型根據型別對應轉換之後，會套用字元集對應。  
  
> [!NOTE]  
> 字元集對應定義上中繼資料物件總管 中的每個節點層級，且呈現關於所有字元集，從 MySQL 讀取。  
  
## <a name="charset-mapping-on-different-node-levels"></a>在不同節點層級上對應的字元集  
字元集對應而異於不同節點層級，也就是：  
  
1.  在根中繼資料節點層級  
  
2.  針對資料庫、 類別和物件節點層級  
  
> [!NOTE]  
> 編輯字元集對應中，選取 [] 索引標籤包含三個按鈕，無論在不同節點層級上的對應。  
>   
> 其中包括：  
>   
> 1.  **適用於：** 適用於編輯字元集對應且尚未儲存時，才啟用的使用者所做的變更。  
> 2.  **取消：** 取消使用者所做的變更。 字元集對應編輯，但不是會儲存時，取得啟用 按鈕。  
> 3.  **重設預設值：** 所有對應重設都為預設值。  
  
1.  **在根中繼資料節點層級：** 字元集對應方格包含與個別的資料行，每個字元集的 charset 方格。 方格的資料行如下：  
  
    1.  名為格線的第一個資料行**字元集名稱**包含字元集名稱。  
  
    2.  第二個名為**Charset 描述**包含字元集的描述。  
  
    3.  第三個資料行標題**目標字元集類型**包含特定字元集對應設定。 此資料行的值如下：  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定的字集的預設值之後 CHAR/VARCHAR 或 NCHAR/NVARCHAR，有前置詞 '（預設值）'。  
  
    MySQL 資料庫介於根中繼資料節點層級上的目標資料庫的字元集對應如下所示：  
  
    ||||  
    |-|-|-|  
    |**字元集名稱**|**Charset 描述**|**目標字元集類型 （預設值）**|  
    |big5|Big5 繁體中文|NCHAR/NVARCHAR （預設值）|  
    |dec8|DEC 西方語系|CHAR/VARCHAR （預設值）|  
    |cp850|DOS 西方語系|CHAR/VARCHAR （預設值）|  
    |hp8|HP 西方語系|CHAR/VARCHAR （預設值）|  
    |koi8r|KOI8-R Relcom 俄文|CHAR/VARCHAR （預設值）|  
    |拉丁文 1|cp1252 西方語系|CHAR/VARCHAR （預設值）|  
    |latin2|ISO 8859-2 中歐語系|CHAR/VARCHAR （預設值）|  
    |swe7|7 位元瑞典文|CHAR/VARCHAR （預設值）|  
    |ascii|US ASCII|CHAR/VARCHAR （預設值）|  
    |ujis|EUC-JP 日文|NCHAR/NVARCHAR （預設值）|  
    |sjis|日文 (SHIFT-JIS)|NCHAR/NVARCHAR （預設值）|  
    |希伯來文|ISO 8859-8 希伯來文|CHAR/VARCHAR （預設值）|  
    |tis620|TIS620 泰文|CHAR/VARCHAR （預設值）|  
    |euckr|韓文 EUC-KR|NCHAR/NVARCHAR （預設值）|  
    |koi8u|KOI8-U 烏克蘭文|CHAR/VARCHAR （預設值）|  
    |gb2312|GB2312 Simplified Chinese|NCHAR/NVARCHAR （預設值）|  
    |希臘文|ISO 8859-7 希臘文|CHAR/VARCHAR （預設值）|  
    |cp 1250|Windows 中歐語系|CHAR/VARCHAR （預設值）|  
    |gbk|GBK Simplified Chinese|NCHAR/NVARCHAR （預設值）|  
    |latin5|ISO 8859-9 土耳其文|CHAR/VARCHAR （預設值）|  
    |armscii8|ARMSCII 8 亞美尼亞文|CHAR/VARCHAR （預設值）|  
    |utf8|Utf-8 Unicode|NCHAR/NVARCHAR （預設值）|  
    |ucs2|Ucs-2 Unicode|NCHAR/NVARCHAR （預設值）|  
    |cp866|DOS 俄文|CHAR/VARCHAR （預設值）|  
    |keybcs2|DOS Kamenicky 捷克文-斯洛伐克文|CHAR/VARCHAR （預設值）|  
    |macce|Mac 中歐語系|CHAR/VARCHAR （預設值）|  
    |macroman|Mac 西方語系|CHAR/VARCHAR （預設值）|  
    |cp852|DOS 中部語系|CHAR/VARCHAR （預設值）|  
    |latin7|ISO 8859-13 Baltic|CHAR/VARCHAR （預設值）|  
    |cp 1251|Windows Cyrillic|CHAR/VARCHAR （預設值）|  
    |cp 1256|Windows Arabic|CHAR/VARCHAR （預設值）|  
    |cp 1257|Windows Baltic|CHAR/VARCHAR （預設值）|  
    |BINARY|二進位虛擬字元集|CHAR/VARCHAR （預設值）|  
    |geostd8|GEOSTD8 喬治亞文|CHAR/VARCHAR （預設值）|  
    |cp932|對於 Windows 日文 SJIS|NCHAR/NVARCHAR （預設值）|  
    |eucjpms|對於 Windows 日文 UJIS|NCHAR/NVARCHAR （預設值）|  
  
2.  **資料庫、 類別或物件節點層級：** 資料庫、 類別或物件節點層級中，字元集對應方格包含根中繼資料節點層級上相同的資料列上來。:  
  
    1.  方格標題的第一個資料行**字元設定名稱**包含字元集名稱。  
  
    2.  第二個資料行標題**字元設定描述**包含字元集的描述。  
  
    3.  唯一的差別是格線的第三個資料行中的值。 第三個資料行標題**目標資料型別**包含特定字元集對應設定。 資料行的值如下：  
  
        -   繼承 （CHAR/VARCHAR 或 NCHAR/NVARCHAR）  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   字元集之間的對應中的 MySQL 資料庫和資料庫、 類別和物件節點層級上的目標資料庫，則預設值在每個資料行的根目錄以外的層級上的特定字元集**目標資料型別**應該是 '繼承的 '。  
> -   在方格中，值**繼承**會加上其中一個 '(CHAR/VARCHAR)' 或 '(NCHAR/NVARCHAR)' 取決於哪一個值繼承自父代的這個特定的字元集。  
  
