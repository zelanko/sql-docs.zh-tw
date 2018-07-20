---
title: 已更新-Linux 文件上的 SQL Server |Microsoft Docs
description: 顯示最近變更過的文件，在 Linux 上的 Microsoft SQL Server 的更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.date: 04/28/2018
ms.openlocfilehash: f7f1e437e0b9d4c2940293280ee2c5529da85e6c
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082480"
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的與最近更新的文章： SQL Server on Linux 文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2018-02-03** &nbsp; -到- &nbsp; **2018-04-28**
- *主旨區域：* &nbsp; **Microsoft SQL Server on Linux**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


1. [Linux 上的 SQL Server 的 active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)
2. [設定 SQL Server Always On 可用性群組上 Windows 和 Linux （跨平台）](sql-server-linux-availability-group-cross-platform.md)
3. [一律對 Linux 上的可用性群組](sql-server-linux-availability-group-operate-ha.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [設定存放庫進行安裝及升級 Linux 上的 SQL Server](#TitleNum_1)
2. [使用 mssql-conf 工具，設定在 Linux 上的 SQL Server](#TitleNum_2)
3. [Linux 上的 SQL Server 2017 的版本資訊](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-repositories-for-installing-and-upgrading-sql-server-on-linuxsql-server-linux-change-repomd"></a>1.&nbsp; [設定存放庫進行安裝及升級 Linux 上的 SQL Server](sql-server-linux-change-repo.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 72.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5ccaa0fcb8895f25c162e4e0494ad4872773de3 29a959be6ee7d58fe0c53e8f91bdd282fb2e6d29  (PR=5676  ,  Filename=sql-server-linux-change-repo.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- 列印出檔案的內容。

```
   sudo cat /etc/yum.repos.d/mssql-server.repo
```

- **名稱**屬性是設定的儲存機制。 您可以使用這份文件的 [儲存機制] 區段中的資料表來識別它。

**移除舊的存放庫 (RHEL)**

如有需要，移除舊的存放庫，使用下列命令。

```
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假設，如上一節中所識別的檔案命名為**mssql server.repo**。

**設定新的存放庫 (RHEL)**

設定新的存放庫，若要使用 SQL Server 安裝與升級。 使用下列命令之一來設定您選擇的存放庫。

| Repository | 命令 |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

**<a id="sles"></a> 設定 SLES 儲存機制**

您可以使用下列步驟來在 SLES 上設定存放庫。

**檢查先前設定的存放庫 (SLES)**

先確認是否已註冊的 SQL Server 儲存機制。

- 使用**zypper 資訊**取得任何先前設定的儲存機制的資訊。

```
   sudo zypper info mssql-server
```

- **存放庫**屬性是設定的儲存機制。 您可以使用這份文件的 [儲存機制] 區段中的資料表來識別它。

**移除舊的存放庫 (SLES)**

如有需要，移除舊的存放庫。 使用其中一個下列的命令，根據先前設定的存放庫的類型。

| Repository | 若要移除的命令 |
|---|---|
| **預覽** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>2.&nbsp; [使用 mssql-conf 工具，設定在 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1))  |  [下一步](#TitleNum_3))

<!-- Source markdown line 151.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3664c4d64ea4840dcbc718461ed04403cc486f30 89f708af45ce262057e967e9047f1328e19248ba  (PR=5676  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->




**<a id="masterdatabasedir"></a> 變更預設 master 資料庫檔案目錄位置**


**Filelocation.masterdatafile**並**filelocation.masterlogfile**設定變更 SQL Server 引擎從中尋找 master 資料庫檔案的位置。 根據預設，此位置會是 /var/opt/mssql/data。

若要變更這些設定，請使用下列步驟：

- 建立新的錯誤記錄檔的目標目錄。 下列範例會建立新 **/tmp/masterdatabasedir**目錄：

```
   sudo mkdir /tmp/masterdatabasedir
```

- 變更擁有者和群組的目錄**mssql**使用者：

```
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
```

- 若要變更與 master 的資料和記錄檔的預設 master 資料庫目錄使用 mssql conf**設定**命令：

```
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
```

- 停止 SQL Server 服務：

```
   sudo systemctl stop mssql-server
```

- 將 master.mdf 和 masterlog.ldf 移：

```
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
```

- 啟動 SQL Server 服務：

```
   sudo systemctl start mssql-server
```

> [!NOTE]
> 如果 SQL Server 指定的目錄中找不到 master.mdf 和 mastlog.ldf 檔、 樣板化系統資料庫的複本將會自動建立在指定的目錄中，而且 SQL Server 將成功啟動。 不過，中繼資料，例如使用者資料庫、 伺服器登入、 伺服器憑證、 加密金鑰、 SQL agent 作業或舊的 SA 登入密碼不會更新新的 master 資料庫中。 您必須停止 SQL Server 並將您的舊 master.mdf 和 mastlog.ldf 移至新的指定位置並啟動 SQL Server 以繼續使用現有的中繼資料。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>3.&nbsp; [Linux 上的 SQL Server 2017 的版本資訊](sql-server-linux-release-notes.md)

*更新日期︰ 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 367d112a9427bbdd18e0e52cc82264dd169c91ae 63a67be08fa39ece778cf9ca0b9746dd28694574  (PR=5676  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- [啟用 SQL Server Agent]

**<a id="CU6"></a> CU6 (第 2018 年 4 月)**


這是 SQL Server 2017 的累計更新 6 (CU6) 版本。 此版本的 SQL Server 引擎版本是 14.0.3025.34。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)。

**套件詳細資料**


若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3025.34-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) |
| SLES RPM 套件 | 14.0.3025.34-3 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) |
| Ubuntu 16.04 的 Debian 套件 | 14.0.3025.34-3 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新增 + 更新 (11 + 6): &nbsp; &nbsp; **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新增 + 更新 (18 + 0): &nbsp; &nbsp; **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新增 + 更新 (218 + 14):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新增 + 更新 (14 + 0): &nbsp; &nbsp; **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新增 + 更新 (3 + 2): &nbsp; &nbsp; **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新增 + 更新 (3 + 3): &nbsp; &nbsp; **sql Linux**文件](../linux/new-updated-linux.md)
- [新增 + 更新 (7 + 10): &nbsp; &nbsp;**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新增 + 更新 (0 + 2): &nbsp; &nbsp; **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新增 + 更新 (1 + 3): &nbsp; &nbsp; **SQL Operations Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新增 + 更新 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新增 + 更新 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新增 + 更新 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新增 + 更新 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新增 + 更新 (1 + 1): &nbsp; &nbsp; **Tools for SQL**文件](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新增 + 更新 (0 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新增 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新增 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新增 + 更新 (0 + 0)：**適用於 SQL 的多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新增 + 更新 (0 + 0)：**ODBC (開放式資料庫連接) for SQL** 文件](../odbc/new-updated-odbc.md)
- [新增 + 更新 (0 + 0)：**適用於 SQL 的 PowerShell** 文件](../powershell/new-updated-powershell.md)
- [新增 + 更新 (0 + 0):**範例 sql**文件](../samples/new-updated-samples.md)
- [新增 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新增 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)

