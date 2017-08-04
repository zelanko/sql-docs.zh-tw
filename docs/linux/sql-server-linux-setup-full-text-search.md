---
title: "Linux 上安裝 SQL Server 全文檢索搜尋 |Microsoft 文件"
description: "本主題描述如何在 Linux 上安裝 SQL Server 全文檢索搜尋。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 8dd5d857efc47a0dc181a0fc9bf1537cb8b08441
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-full-text-search-on-linux"></a>Linux 上安裝 SQL Server 全文檢索搜尋

下列步驟安裝[SQL Server 全文檢索搜尋](https://msdn.microsoft.com/library/ms142571.aspx)(**mssql-伺服器-fts**) 在 Linux 上。 全文檢索搜尋可讓您針對 SQL Server 資料表中的字元資料執行全文檢索查詢。 如需此版本的已知問題，請參閱[Release Notes](sql-server-linux-release-notes.md)。

> [!NOTE]
> 之前先安裝 SQL Server 全文檢索搜尋，[安裝 SQL Server](sql-server-linux-setup.md#platforms)。 這會設定索引鍵和您在安裝時使用的儲存機制**mssql-伺服器-fts**封裝。

安裝 SQL Server 全文檢索搜尋，您為平台：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL 上安裝</a>

使用下列命令，安裝**mssql-伺服器-fts** Red Hat Enterprise Linux 上。 

```bash
sudo yum update
sudo yum install -y mssql-server-fts
```

如果您已經有**mssql-伺服器-fts**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

如果您需要離線安裝，找出全文檢索搜尋的封裝下載中[版本資訊](sql-server-linux-release-notes.md)。 請使用相同的離線安裝步驟 > 主題所述，[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列命令，安裝**mssql-伺服器-fts** Ubuntu 上。 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

如果您已經有**mssql-伺服器-fts**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

如果您需要離線安裝，找出全文檢索搜尋的封裝下載中[版本資訊](sql-server-linux-release-notes.md)。 請使用相同的離線安裝步驟 > 主題所述，[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="SLES">SLES 上安裝</a>

使用下列命令，安裝**mssql-伺服器-fts** SUSE Linux Enterprise Server 上。 

```bash
sudo zypper install mssql-server-fts
```

如果您已經有**mssql-伺服器-fts**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

如果您需要離線安裝，找出全文檢索搜尋的封裝下載中[版本資訊](sql-server-linux-release-notes.md)。 請使用相同的離線安裝步驟 > 主題所述，[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="supported-languages"></a>支援的語言

全文檢索搜尋會使用[斷詞工具](https://msdn.microsoft.com/library/ms142509.aspx)，以決定如何識別個別單字語言為基礎。 您可以藉由查詢來取得一份已註冊的斷詞工具**sys.fulltext_languages**目錄檢視。 針對下列語言的斷詞工具會隨 SQL Server 2017 RC2:

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

## <a id="filters"></a>篩選器

全文檢索搜尋也可以搭配儲存在二進位檔案中的文字。 但在此情況下，必須已安裝的篩選器處理檔案。 如需篩選器的詳細資訊，請參閱[設定及管理搜尋的篩選](https://msdn.microsoft.com/library/ms142499.aspx)。

您可以看到一份已安裝篩選器藉由呼叫**sp_help_fulltext_system_components 'filter'**。 SQL Server 2017 rc2，會安裝下列的篩選器：

| 元件名稱 | 類別識別碼 | 版本 |
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
|:.dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
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
|指定.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
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
[語意搜尋](https://msdn.microsoft.com/library/gg492075.aspx)來擷取和索引統計上相關的全文檢索搜尋功能為基礎*主要片語*。 這可讓您查詢資料庫中的文件中的意義。 這也有助於識別相似的文件。

若要使用語意搜尋，您必須先下載並附加[語義語言統計資料庫](https://msdn.microsoft.com/library/gg509085.aspx)。

1. 在 Windows 電腦、[下載。語意語言統計資料庫的 MSI 檔案](https://www.microsoft.com/download/details.aspx?id=54277)。

    > [!NOTE]
    > 在此時間是資料庫的下載。MSI 檔案，因此一部 Windows 電腦需要此步驟。

2. 執行。要擷取資料庫和記錄檔的 MSI 檔案。

3. 將資料庫和記錄檔移至您的 Linux SQL Server 電腦。

    > [!TIP]
    > 如需有關如何將檔案從 Windows 移至 Linux 指引，請參閱[檔案傳輸至 Linux](sql-server-linux-migrate-restore-database.md#transfer-the-backup-file-to-linux)。

4. 若要附加的語言統計資料庫 Linux SQL Server 執行個體上執行下列 TRANSACT-SQL 命令。

    ```tsql
    CREATE DATABASE semanticsdb  
            ON ( FILENAME = N'var/opt/mssql/data/semanticsdb.mdf' )  
            LOG ON ( FILENAME = N'var/opt/mssql/data/semanticsdb_log.ldf' )  
            FOR ATTACH;  
    GO  
    ```

5. 執行下列 TRANSACT-SQL 命令註冊語意語言統計資料庫。

    ```tsql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO  
    ```

## <a name="next-steps"></a>後續的步驟

全文檢索搜尋的相關資訊，請參閱[SQL Server 全文檢索搜尋](../relational-databases/search/full-text-search.md)。 

