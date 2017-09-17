---
title: "已更新-SQL Server on Linux 的文件 |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL Server on Linux 的最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的與最近的更新： SQL Server on Linux 的文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-07-18** &nbsp; -到- &nbsp; **2017年-09-11**
- *主旨區域：* &nbsp; **Microsoft SQL Server on Linux**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結跳至最近新增的新發行項。


1. [DB 郵件和電子郵件警示，在 Linux 上的 SQL 代理程式](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

此區段會顯示更新所收集從最近曾發生大規模的更新發行項的摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單所提供的摘錄的一節中所列的所有更新文章連結。

1. [SQL Server on Linux 會操作 HA 可用性群組](#TitleNum_1)
2. [設定 SQL Server 2017 容器映像 docker](#TitleNum_2)
3. [設定 SQL Server on Linux mssql conf 工具](#TitleNum_3)
4. [SQL Server on Linux 的客戶意見反應](#TitleNum_4)
5. [從 Windows 的 SQL Server 資料庫移轉至 Linux 使用備份與還原](#TitleNum_5)
6. [在 Linux 上的 SQL Server 2017 的版本資訊](#TitleNum_6)
7. [SQL Server on Linux 的安裝指南](#TitleNum_7)
8. [Linux 上安裝 SQL Server Integration Services (SSIS)](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1.&nbsp;[運作 HA 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-failover-ha.md)

*更新日期︰ 2017年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**可用性群組升級**


您將可用性群組升級之前，請檢閱位於 [升級可用性群組複本執行個體-..的最佳作法/ database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md）。

下列各節說明如何在 Linux 上執行輪流升級 SQL Server 執行個體，與可用性群組。

**在 Linux 上的升級步驟**


在 Linux 中的 SQL Server 執行個體上的可用性群組複本時，可用性群組的叢集類型是`EXTERNAL`或`NONE`。 除了 Windows Server 容錯移轉叢集 (WSFC) 是由叢集管理員的可用性群組`EXTERNAL`。 與 Corosync pacemaker 是外部叢集管理員的範例。 沒有叢集管理員與可用性群組有叢集類型`NONE`此處所述的升級步驟特有的可用性群組的叢集類型`EXTERNAL`或`NONE`。

1. 在開始之前，備份每個資料庫。
2. 升級 SQL Server 執行個體主控次要複本。

    a. 先升級非同步次要複本。

    b. 升級同步次要複本。

   >[!NOTE]
   >如果可用性群組只有非同步複本-若要避免遺失任何資料會將一個複本變更為同步，並等待同步處理。 接著升級此複本。

   b.1。 在裝載次要複本升級的目標節點上停止資源

   然後再執行 [升級] 命令，停止資源，因此叢集將不進行監視並不必要地容錯。 下列範例會將會在節點上的位置限制式上停止資源。 更新`ag_cluster-master`的資源名稱和`nodeName1`與裝載複本升級的目標節點。

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2.&nbsp;[Docker 設定 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)

*更新日期︰ 2017年-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. 識別 Docker**標記**您想要使用的版本。 若要檢視可用的標籤，請參閱[mssql-伺服器-linux Docker 中樞頁面](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

1. 提取 SQL Server 容器映像的結束標記。 例如，若要提取 RC1 映像，取代`<image_tag>`下列命令，以及在`rc1`。

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. 若要使用該映像執行新的容器，指定中的標記名稱`docker run`命令。 在下列命令，取代`<image_tag>`與您想要執行的版本。

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

這些步驟可以用於降級現有的容器。 例如，您可能想要復原或降級基於疑難排解或測試執行中的容器。 若要降級之後執行的容器，您必須使用持續性技術資料的資料夾。 遵循相同的步驟中所述 [升級] 區段-#upgrade），但當您執行新的容器，請指定較舊版本的標記名稱。

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3.&nbsp;[設定 SQL Server on Linux mssql conf 工具](sql-server-linux-configure-mssql-conf.md)

*更新日期︰ 2017年-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>設定本機稽核的目錄**


**Telemetry.userrequestedlocalauditdirectory**設定可讓本機稽核，並建立可讓您設定本機的稽核記錄，其中的目錄。

1. 建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新**/tmp/稽核**目錄：

```
   sudo mkdir /tmp/audit
```

1. 變更擁有者和群組的目錄**mssql**使用者：

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. 重新啟動 SQL Server 服務：

```
   sudo systemctl restart mssql-server
```

如需詳細資訊，請參閱 [Linux--sql-server-linux-customer-feedback.md 上的 SQL Server 客戶回函。）

**<a id="lcid"></a>變更 SQL Server 的地區設定**


**Language.lcid**設定變更為任何支援的語言識別碼 (LCID) 的 SQL 伺服器地區設定。

1. 下列範例會變更為法文的地區設定 (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. 重新啟動才能套用變更的 SQL Server 服務：

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>設定記憶體限制**


**Memory.memorylimitmb**到 SQL Server 設定控制實體可用的記憶體數量 （以 mb 為單位）。 預設為 80%的實體記憶體。

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**memory.memorylimitmb**。 下列範例會變成 3.25 gb (3328 MB) 的 SQL Server 中可用的記憶體。

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. 重新啟動才能套用變更的 SQL Server 服務：



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4.&nbsp;[客戶的意見反應 for SQL Server on Linux](sql-server-linux-customer-feedback.md)

*更新日期︰ 2017年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**Docker**

若要啟用本機稽核 docker，您必須擁有 Docker [保存您 data--sql-server-linux-configure-docker.md）。

1. 新的本機稽核記錄檔的目標目錄會在容器中。 在您的電腦上的主機目錄建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新**/稽核**目錄：

```
   sudo mkdir <host directory>/audit
```


1. 新增`mssql.conf`檔案行`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主機目錄中：

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. 執行容器映像
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**接下來的步驟**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5.&nbsp;[從 Windows 的 SQL Server 資料庫移轉至 Linux 使用備份與還原](sql-server-linux-migrate-restore-database.md)

*更新日期︰ 2017年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* 具有下列的 Windows 電腦：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安裝。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安裝。
  * 若要移轉的目標資料庫。

* Linux 機器會有安裝下列項目：
  * SQL Server 2017 RC2。 請參閱用於安裝快速入門 [RHEL--quickstart-install-connect-red-hat.md)，[SLES-快速入門-安裝-連線-suse.md)，或 [Ubuntu-快速入門-安裝-連線-ubuntu.md)。
  * SQL Server 2017 RC2 [命令列 tools--sql-server-linux-setup-tools.md)。

**在 Windows 上建立備份**


有幾種方式可以在 Windows 上建立資料庫的備份檔案。 下列步驟會使用 SQL Server Management Studio (SSMS)。

1. 啟動**SQL Server Management Studio** Windows 電腦上。

1. 在 [連接] 對話方塊中，輸入**localhost**。

1. 在 [物件總管] 中，展開**資料庫**。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6.&nbsp;[Linux 上的 SQL Server 2017 的版本資訊](sql-server-linux-release-notes.md)

*更新日期︰ 2017年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (第 2017 年 8 月)**


此版本的 SQL Server 引擎版本是 14.0.900.75。

**支援的平台**


| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 伺服器和桌面 | XFS 或 EXT4 | [安裝 guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安裝指南-快速入門-安裝-連線-suse.md） |
| Ubuntu 16.04LTS | EXT4 | [安裝指南-快速入門-安裝-連線-ubuntu.md） |
| Docker 引擎 1.8 + Windows、 Mac 或 Linux 上 | 不適用 | [安裝指南-快速入門-安裝-連線-docker.md） |

> [!NOTE]
> 您需要至少 3.25 GB 的記憶體來執行 SQL Server on Linux。
> SQL Server 引擎已在此階段中測試 1.5 TB 的記憶體。

**封裝詳細資料**


下表中會列出套件詳細資料及針對 RPM 和 Debian 封裝的下載位置。 請注意，您不需要直接下載這些封裝，如果您使用下列的安裝指南中的步驟：

- [安裝 SQL Server 封裝--sql server-linux setup.md）
- [安裝全文檢索搜尋 package--sql-server-linux-setup-full-text-search.md）
- [安裝 SQL Server Agent package--sql-server-linux-setup-sql-agent.md）

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.900.75-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7.&nbsp;[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)

*更新日期︰ 2017年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>復原 SQL Server**


若要復原先前版本的 SQL Server 降級，使用下列步驟：

1. 識別您想要降級至 SQL Server 封裝的版本號碼。 如需封裝的數字的清單，請參閱 [發行 notes--sql-server-linux-release-notes.md)。

1. 降級為舊版的 SQL Server。 在下列命令，取代`<version_number>`與您在第一個步驟所識別的 SQL Server 版本號碼。

   | 平台 | 套件更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 只支援降級至相同的主要版本，例如 SQL Server 2017 內的版本。

> [!IMPORTANT]
> RC2 之間 RC1 此時只支援降級。




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8.&nbsp;[Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)

*更新日期︰ 2017年-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



如果您已經有`mssql-server-is`安裝，您可以更新為最新版本，使用下列命令：

```
sudo apt-get install mssql-server-is
```


若要移除`mssql-server-is`，您可以執行下列命令：
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>RHEL 上中安裝 SSIS**

若要安裝`mssql-server-is`RHEL 上的套件，請遵循下列步驟：


1.  輸入超級使用者模式。

```
    sudo su
```


2.  下載 Microsoft SQL Server Red Hat 儲存機制設定檔。

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  結束超級使用者模式。

```
    exit
```


4.  執行下列命令來安裝 SQL Server Integration Services。

```
    sudo yum install -y mssql-server-is
```


5.  安裝之後，請執行`ssis-conf`。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

此區段會列出最近已更新的發行項，在我們的公用 GitHub.com 儲存機制中的其他主體區域中的非常類似文件： [MicrosoftDocs/sql 的文件](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 12): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **Tools for SQL**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **Master Data Services (MDS) sql**文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



