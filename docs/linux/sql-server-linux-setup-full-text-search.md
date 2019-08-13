---
title: 在 Linux 上安裝 SQL Server 全文檢索搜尋
description: 本文描述如何在 Linux 上安裝 SQL Server 全文檢索搜尋。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 9a637e6b12c674102bd09239739a137e1d442e12
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065096"
---
# <a name="install-sql-server-full-text-search-on-linux"></a>在 Linux 上安裝 SQL Server 全文檢索搜尋

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟會在 Linux 上安裝 [SQL Server 全文檢索搜尋](../relational-databases/search/full-text-search.md) (**mssql-server-fts**)。 全文檢索搜尋可讓您針對 SQL Server 資料表中以字元為基礎的資料執行全文檢索查詢。 如需此版本的已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

> [!NOTE]
> 安裝 SQL Server 全文檢索搜尋之前，請先[安裝 SQL Server](sql-server-linux-setup.md#platforms)。 這會設定您在安裝 **mssql-server-fts** 套件時所使用的金鑰和存放庫。

為您的平台安裝 SQL Server 全文檢索搜尋：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">在 RHEL 上安裝</a>

使用下列命令，在 Red Hat Enterprise Linux 上安裝 **mssql-server-fts**。 

```bash
sudo yum install -y mssql-server-fts
```

如果您已經安裝 **mssql-server-fts**，則可使用下列命令更新為最新版本：

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到全文檢索搜尋套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列命令，在 Ubuntu 上安裝 **mssql-server-fts**。 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

如果您已經安裝 **mssql-server-fts**，則可使用下列命令更新為最新版本：

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到全文檢索搜尋套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="SLES">在 SLES 上安裝</a>

使用下列命令，在 SUSE Linux Enterprise Server 上安裝 **mssql-server-fts**。 

```bash
sudo zypper install mssql-server-fts
```

如果您已經安裝 **mssql-server-fts**，則可使用下列命令更新為最新版本：

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到全文檢索搜尋套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="supported-languages"></a>支援的語言

全文檢索搜尋會使用[文字分隔](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)，決定如何根據語言識別個別字詞。 您可以查詢 **sys.fulltext_languages** 目錄檢視來取得已註冊的文字分隔清單。 下列語言的文字分隔會隨著 SQL Server 一起安裝：

| 語言 | 語言識別碼 |
|---|---|
| 中性語言 | 0 |
| 阿拉伯文 | 1025 |
| 孟加拉文 (印度) | 1093 |
| 巴克摩 | 1044 |
| 巴西文 | 1046 |
| 英式英文 | 2057 |
| 保加利亞文 | 1026 |
| 卡達隆尼亞文 | 1027 |
| 中文 (香港特別行政區、中國) | 3076 |
| 中文 (澳門特別行政區) | 5124 |
| 中文 (新加坡) | 4100 |
| 克羅埃西亞文 | 1050 |
| 捷克文 | 1029 |
| 丹麥文 | 1030 |
| 荷蘭文 | 1043 |
| 英文 | 1033 |
| 法文 | 1036 |
| 德文 | 1031 |
| 希臘文 | 1032 |
| 古吉拉特文 | 1095 |
| Hebrew | 1037 |
| Hindi | 1081 |
| 冰島文 | 1039 |
| 印尼文 | 1057 |
| 義大利文 | 1040 |
| 日文 | 1041 |
| 坎那達文 | 1099 |
| 韓文 | 1042 |
| 拉脫維亞文 | 1062 |
| 立陶宛文 | 1063 |
| 馬來文 - 馬來西亞 | 1086 |
| 馬來亞拉姆文 | 1100 |
| 馬拉提文 | 1102 |
| 波蘭文 | 1045 |
| 葡萄牙文 | 2070 |
| 旁遮普文 | 1094 |
| 羅馬尼亞文 | 1048 |
| 俄文 | 1049 |
| 塞爾維亞文 (斯拉夫) | 3098 |
| 塞爾維亞文 (拉丁) | 2074 |
| 簡體中文 | 2052 |
| 斯洛伐克文 | 1051 |
| 斯洛維尼亞文 | 1060 |
| 西班牙文 | 3082 |
| 瑞典文 | 1053 |
| 坦米爾文 | 1097 |
| 特拉古文 | 1098 |
| 泰文 | 1054 |
| 繁體中文 | 1028 |
| 土耳其文 | 1055 |
| 烏克蘭文 | 1058 |
| 烏都文 | 1056 |
| 越南文 | 1066 |

## <a id="filters"></a> 篩選

全文檢索搜尋也適用於儲存在二進位檔案中的文字。 但是在此情況下，您必須已安裝篩選才能處理檔案。 如需篩選的詳細資訊，請參閱[設定及管理搜尋的篩選](../relational-databases/search/configure-and-manage-filters-for-search.md)。

您可以呼叫 **sp_help_fulltext_system_components 'filter'** 來查看已安裝的篩選清單。 SQL Server 會安裝下列篩選：

| 元件名稱 | 類別識別碼 | Version |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ans | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.asc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asm | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.asp | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cls | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.csa | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.css | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dos | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hhc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.html | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ics | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.idq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.mak | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.prc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rgs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sol | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.tab | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tdl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.udt | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.url | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>語意搜尋
[語意搜尋](../relational-databases/search/semantic-search-sql-server.md)是以全文檢索搜尋功能為基礎，可擷取相關「關鍵片語」  並以統計方式編制索引。 這可讓您查詢資料庫中文件內的意義。 它也有助於識別類似的文件。

若要使用語意搜尋，您必須先將語意語言統計資料的資料庫還原至您的電腦。

1. 使用 [sqlcmd](sql-server-linux-setup-tools.md) 這類工具，在您的 Linux SQL Server 執行個體上執行下列 Transact-SQL 命令。 此命令會還原語言統計資料的資料庫。

   ```sql
   RESTORE DATABASE [semanticsdb] FROM
   DISK = N'/opt/mssql/misc/semanticsdb.bak' WITH FILE = 1,
   MOVE N'semanticsdb' TO N'/var/opt/mssql/data/semanticsDB.mdf',
   MOVE N'semanticsdb_log' TO N'/var/opt/mssql/data/semanticsdb_log.ldf', NOUNLOAD, STATS = 5
   GO
   ```

   > [!NOTE]
   > 如有必要，請更新先前 RESTORE 命令中的路徑，以調整您的設定。

1. 執行下列 Transact-SQL 命令，以註冊語意語言統計資料的資料庫。

    ```sql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO
    ```

## <a name="next-steps"></a>後續步驟

如需全文檢索搜尋的資訊，請參閱 [SQL Server 全文檢索搜尋](../relational-databases/search/full-text-search.md)。 
