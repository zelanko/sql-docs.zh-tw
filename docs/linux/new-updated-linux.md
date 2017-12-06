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
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 4adfcb675e52b5b73bd4dcc4867bf79350a26d52
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>新的與最近的更新： SQL Server on Linux 的文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-09-28** &nbsp; -到- &nbsp; **2017年-12-02**
- *主旨區域：* &nbsp; **Microsoft SQL Server on Linux**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [在雲端中執行 SQL Server 2017](quickstart-install-connect-clouds.md)
2. [變更 GA 儲存機制預覽儲存機制從儲存機制](sql-server-linux-change-repo.md)
3. [效能最佳作法和 Linux 上的 SQL Server 2017 的設定指導方針](sql-server-linux-performance-best-practices.md)
4. [容錯移轉叢集執行個體的 SQL Server on Linux](sql-server-linux-shared-disk-cluster-concepts.md)
5. [設定容錯移轉叢集執行個體-iSCSI-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
6. [設定容錯移轉叢集執行個體-NFS-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
7. [設定容錯移轉叢集執行個體-SMB-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
8. [操作容錯移轉叢集執行個體-SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)
9. [限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)
10. [Linux Docker 容器中的 SQL Server 資料庫還原](tutorial-restore-backup-in-sql-server-container.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [執行 SQL Server 2017 容器映像使用 Docker](#TitleNum_1)
2. [設定 Alwayson 可用性群組的 SQL Server on Linux](#TitleNum_2)
3. [可用性群組組態的高可用性與資料保護](#TitleNum_3)
4. [設定 SQL Server 2017 容器映像 docker](#TitleNum_4)
5. [加密連接到 SQL Server on Linux](#TitleNum_5)
6. [建立和執行在 Linux 上的 SQL Server Agent 作業](#TitleNum_6)
7. [SQL Server on Linux 的安裝指南](#TitleNum_7)
8. [設定容錯移轉叢集執行個體的 SQL Server 上 Linux (RHEL)](#TitleNum_8)
9. [疑難排解 SQL Server on Linux](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-run-the-sql-server-2017-container-image-with-dockerquickstart-install-connect-dockermd"></a>1.&nbsp;[執行 SQL Server 2017 容器映像使用 Docker](quickstart-install-connect-docker.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 261.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2aaf953c2f1fb675b1304186108fbef1eebf6f8f f7cd42bb320a8892a5ec63ce999186438097636a  (PR=4150  ,  Filename=quickstart-install-connect-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**移除您的容器**


如果您想要移除此教學課程中使用的 SQL Server 容器，請執行下列命令：

```
sudo docker stop sql1
sudo docker rm sql1
```

```
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 停止並移除容器，永久刪除容器中的任何 SQL Server 資料。 如果您要保留您的資料，[建立和複製備份的檔案超出 container--tutorial-restore-backup-in-sql-server-container.md） 或使用 [容器資料持續性 technique--sql-server-linux-configure-docker.md#persist）。




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-always-on-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-configure-hamd"></a>2.&nbsp;[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 129.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c7e6bc862e5b062a855918efbeee5fe748b7236 6900c9a30ce04ce54e7aaa270ef7d276c18f9afd  (PR=4150  ,  Filename=sql-server-linux-availability-group-configure-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



- 具有兩個同步複本及設定複本建立可用性群組：

   >[!IMPORTANT]
   >此架構可讓任何版本的 SQL Server 以裝載第三個複本。 例如，第三個複本可以裝載於 SQL Server Enterprise Edition。 在 Enterprise 版本中，唯一有效的端點類型是`WITNESS`。

```sql
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
       N'**<node1>**' WITH (
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node2>**' WITH (
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node3>**' WITH (
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**',
          AVAILABILITY_MODE = CONFIGURATION_ONLY
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-high-availability-and-data-protection-for-availability-group-configurationssql-server-linux-availability-group-hamd"></a>3.&nbsp;[的可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 106.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e6bee794ce19f1ed62298b4a0cce7207550f1595 b64726cd6e91721850721786d26c170d59fc320a  (PR=4150  ,  Filename=sql-server-linux-availability-group-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



預設值為`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`為 0。 下表描述可用性行為。

| |高可用性 （& s) </br> 資料保護 | 資料保護
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|主要複本中斷 | 自動容錯移轉。 新的主要是 R / W | 自動容錯移轉。 新的主要不適用於使用者交易。
|次要複本中斷 | 主要是 R/W，公開執行資料遺失 （如果主要失敗，且無法復原）。 如果主要沒有自動容錯移轉也會失敗。 | 主要不適用於使用者交易。 沒有任何容錯移轉至主要複本也會失敗。
|組態的唯一複本中斷 | 主要是 R / W 如果主要沒有自動容錯移轉也會失敗。 | 主要是 R / W 如果主要沒有自動容錯移轉也會失敗。
|同步的次要 + 組態只複本中斷| 主要不適用於使用者交易。 沒有自動容錯移轉。 | 主要不適用於使用者交易。 如果容錯移轉沒有任何複本主要也會失敗。
<sup>*</sup>預設值

>[!NOTE]
>裝載組態的唯一複本的 SQL Server 執行個體也可以裝載其他資料庫。 它也可以做為多個可用性群組的組態資料庫。

**需求**


* 與組態的唯一複本可用性群組中的所有複本都必須都是 SQL Server 2017 CU 1 或更新版本。
* 任何版本的 SQL Server 可以裝載設定唯一的複本，包括 SQL Server Express。
* 可用性群組必須至少一個次要複本-除了主要複本。
* 組態的唯一複本不會計入每個 SQL Server 執行個體的複本數目上限。 SQL Server standard edition 則允許多達三個複本，SQL Server Enterprise Edition 則允許最多 9。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>4.&nbsp;[Docker 設定 SQL Server 2017 容器映像](sql-server-linux-configure-docker.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 34.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c759fb88ae8d654414202f28c5fc58dfd02581bf fd270118f2f4608fceaf563fc143951b41097bdb  (PR=4150  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



此組態 > 主題提供下列各節中的其他使用案例。

**<a id="production"></a>執行實際執行的容器映像**


快速入門教學課程中的，如上一節中會執行從 Docker Hub 免費的 SQL Server 的開發人員版本。 如果您想要執行實際執行的容器映像，例如 Enterprise、 Standard 或 Web edition，仍適用於大部分的資訊。 不過，有幾項差異，此處所述。

- 如果您有有效的授權，可以只在生產環境中使用 SQL Server。 您可以取得免費的 SQL Server Express 生產授權[這裡](https://go.microsoft.com/fwlink/?linkid=857693)。 SQL Server Standard 和 Enterprise Edition 授權都是透過[Microsoft 大量授權](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx)。

- 實際執行 SQL Server 容器映像必須取自[Docker 存放區](https://store.docker.com)。 如果您還沒有一個 Docker 存放區上建立帳戶。

- 開發人員的容器映像，Docker 存放區上可以設定為執行的實際執行版本。 若要執行實際執行版本中使用下列步驟：

   1. 首先，您的 docker id 登入，從命令列。

```
      docker login
```

   1. 接著，您必須取得免費的開發人員 Docker 存放區上的容器映像。 移至[https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux)，按一下 **繼續簽出**，並遵循指示。

   1. 檢閱需求，和執行程序，在 [快速入門教學課程--快速入門-安裝-連線-docker.md）。 但是，有兩個差異。 您必須先提取映像**存放區/microsoft/mssql-伺服器-linux:\<標記名稱\>**從 Docker 存放區。 您必須指定與您生產環境版本**MSSQL_PID**環境變數。 下列範例會示範如何執行 Enterprise edition 的最新的 SQL Server 2017 容器映像：



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-encrypting-connections-to-sql-server-on-linuxsql-server-linux-encrypted-connectionsmd"></a>5.&nbsp;[加密連接到 SQL Server on Linux](sql-server-linux-encrypted-connections.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 45.  ms.author= meetb;rickbyh.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e3187866df060903e30000d60d673edad46d210 bcb1f2771e6c29b535a30b9f23ac296954509187  (PR=4150  ,  Filename=sql-server-linux-encrypted-connections.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



        sudo chown mssql:mssql mssql.pem mssql.key
        sudo chmod 600 mssql.pem mssql.key
        sudo mv mssql.pem /etc/ssl/certs/
        sudo mv mssql.key /etc/ssl/private/

- **設定 SQL Server**

        systemctl stop mssql-server
        cat /var/opt/mssql/mssql.conf
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

- **註冊用戶端電腦 （Windows、 Linux 或 macOS） 上的憑證**

    -   如果您使用 CA 簽署的憑證，您必須將憑證授權單位 (CA) 憑證，而不是使用者憑證複製到用戶端電腦。
    -   如果您只使用自我簽署的憑證將.pem 檔案複製到下列資料夾發佈到個別和執行命令，讓它們

        - **Windows**:.pem 檔案，做為憑證以目前使用者]-> [匯入信任的根憑證授權單位]-> [憑證
        - **macOS**:

-   **範例連接字串**

    - **..!裡 NotShown-s-md.../includes/ssmanstudiofull-md.md)]** ！ [SSMS 連接 dialog--media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png"SSMS 連接對話方塊 」）



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-create-and-run-sql-server-agent-jobs-on-linuxsql-server-linux-run-sql-server-agent-jobmd"></a>6.&nbsp;[建立和執行在 Linux 上的 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 35.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1598129bb5f98434435d8ad02336a9adf76c7870 6fe3fe7df3a60dbac31f1df59aac9860d293421a  (PR=4150  ,  Filename=sql-server-linux-run-sql-server-agent-job.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



若要完成本教學課程中，需要下列必要條件：

* Linux 機器會有下列先決條件：
  * SQL Server 2017 ([RHEL--quickstart-install-connect-red-hat.md)，[SLES-快速入門-安裝-連線-suse.md)，或 [Ubuntu-快速入門-安裝-連線-ubuntu.md)) 的命令列工具。

下列必要條件為選擇性：

* 使用 SSMS 的 Windows 電腦：
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)選擇性 SSMS 步驟。

**安裝 SQL Server Agent**


若要在 Linux 上使用 SQL Server 代理程式，您必須先安裝**mssql server agent**已安裝的 SQL Server 2017 機器上的封裝。

1. 安裝**mssql server agent**與 Linux 作業系統的適當命令。

   | 平台 | 安裝命令 |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. 使用下列命令，重新啟動 SQL Server:

```
   sudo systemctl restart mssql-server
```

**建立範例資料庫**


使用下列步驟來建立範例資料庫名為**SampleDB**。 此資料庫用於每日備份工作。

1. 在您的 Linux 電腦上開啟 bash 終端機工作階段。



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7.&nbsp;[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)

*更新日期︰ 2017年-12-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880 eedddcfb64c6432215f56b74dc91700d9804fce8  (PR=4160  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=085dd05d56afecbb454206ed8402cfbaa597cfbe) -->



**<a id="repositories"></a>設定來源儲存機制**


當您安裝或升級 SQL Server 時，您收到最新版本的 SQL Server 設定的 Microsoft 儲存機制。

**儲存機制選項**


有兩種類型的每個散發的儲存機制：

- **累計更新 (CU)**: 累計更新 (CU) 儲存機制自該版本包含基底的 SQL Server 版本和 bug 修正或改進的封裝。 累計更新的發行版本，例如 SQL Server 2017 特有。 它們會以一般的步調發行。

- **GDR**: GDR 儲存機制 含有該發行以來的基底的 SQL Server 版本和僅重大修正程式和安全性更新的封裝。 這些更新也會新增到下一個 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該儲存機制。 從 GDR 發行更新至目前的版本支援適用於 SQL Server 變更設定的儲存機制。 您也可以 [降級-#rollback） 至您的主要版本內任何發佈 (例如： 2017年)。 更新不支援從 CU GDR 發行的版本。

**請檢查設定的儲存機制**


如果您想要確認哪些儲存機制已設定，請使用下列平台相關技術。

| 平台 | 程序 |
|-----|-----|
| RHEL | 1.檢視中的檔案**/etc/yum.repos.d**目錄：`sudo ls /etc/yum.repos.d`<br/>2.尋找檔案，以設定 SQL Server 目錄，例如**mssql server.repo**。<br/>3.列印檔案的內容：`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4.**名稱**屬性是設定的儲存機制。|
| SLES | 1.執行下列命令：`sudo zypper info mssql-server`<br/>2.**儲存機制**屬性是設定的儲存機制。 |
| Ubuntu | 1.執行下列命令：`sudo cat /etc/apt/sources.list`<br/>2.檢查 mssql 伺服器的套件 URL。 |



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-configure-failover-cluster-instance---sql-server-on-linux-rhelsql-server-linux-shared-disk-cluster-configuremd"></a>8.&nbsp;[設定容錯移轉叢集執行個體-SQL Server 上 Linux (RHEL)](sql-server-linux-shared-disk-cluster-configure.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 25.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 308fa1809c80a009f7f15b5ca6917f6b76588c3e 71f18baa320041ff10c94e8c7668e40dff45cac3  (PR=4150  ,  Filename=sql-server-linux-shared-disk-cluster-configure.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



> [!div class="checklist"]
> * 安裝及設定 Linux
> * 安裝及設定 SQL Server
> * 設定主機檔案。
> * 設定共用存放裝置，並移動資料庫檔案
> * 安裝和設定每個叢集節點上 Pacemaker
> * 設定容錯移轉叢集執行個體

本文說明如何建立 SQL Server 共用的磁碟的雙節點容錯移轉叢集執行個體 (FCI)。 本文包括指示和範例指令碼 Red Hat Enterprise Linux (RHEL)。 Ubuntu 分佈是 RHEL 類似，因此指令碼範例將通常 Ubuntu 上也能運作。

概念性資訊，請參閱 [SQL Server 容錯移轉叢集執行個體 (FCI) 上 Linux--sql-server-linux-shared-disk-cluster-concepts.md)。

**必要條件**


若要完成以下的端對端案例中，您需要將兩個節點叢集和儲存體的另一部伺服器部署的兩部電腦。 下列步驟概述這些伺服器設定的方式。

**安裝及設定 Linux**


第一個步驟是設定叢集節點上的作業系統。 在叢集中每個節點，設定 linux 散發套件。 兩個節點上使用相同的通訊群組和版本。 使用一或其他的下列發佈：

* RHEL HA 附加元件的有效訂用帳戶

**安裝及設定 SQL Server**


1. 安裝和設定兩個節點上的 SQL Server。  如需詳細指示，請參閱 [安裝 SQL Server on Linux-sql server-linux setup.md)。
1. 將一個節點指定為主要伺服器與另一個則為次要，基於的組態。 使用下列這些詞彙本指南。
1. 在次要節點，停止並停用 SQL Server。
    下列範例會停止，並停用 SQL Server:
```
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
```

    > [!NOTE]
    > At set up time, a Server Master Key is generated for the SQL Server instance and placed at `var/opt/mssql/secrets/machine-key`. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-troubleshoot-sql-server-on-linuxsql-server-linux-troubleshooting-guidemd"></a>9.&nbsp;[疑難排解 SQL Server on Linux](sql-server-linux-troubleshooting-guide.md)

*更新日期︰ 2017年-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f8557a34b38e028ff6e5ac370b6d2d6bf315091 196e56187b57bdd79cc5cdc5e6fce3d41e82af0c  (PR=4150  ,  Filename=sql-server-linux-troubleshooting-guide.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**最基本的組態，或在單一使用者模式啟動 SQL Server**


**以最低組態模式啟動 SQL Server**

如果組態值設定 (如過度調配記憶體) 造成伺服器無法啟動，這就很有用。

```
   sudo -u mssql /opt/mssql/bin/sqlservr -f
```

**以單一使用者模式啟動 SQL Server**

在某些情況下，您可能要以單一使用者模式啟動 SQL Server 執行個體使用啟動選項-m。 例如，您可能想要變更伺服器組態選項，或復原損毀的 master 資料庫或其他系統資料庫。 例如，您可能想要變更伺服器組態選項或復原損毀的 master 資料庫或其他系統資料庫

以單一使用者模式啟動 SQL Server
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m
```

使用 SQLCMD 的單一使用者模式啟動 SQL Server
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
```

> [!WARNING]
>  以 "mssql" 使用者身分啟動 Linux 上的 SQL Server，以免未來發生啟動問題。 例如，"sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]"

如果您不小心與其他使用者啟動 SQL Server，您必須將 SQL Server 資料庫檔案的擁有權變更回之前啟動 SQL Server 與 systemd 'mssql' 使用者。 例如，若要變更 'mssql' 使用者 /var/opt/mssql 底下的所有資料庫檔案的擁有權，執行下列命令

```
   chown -R mssql:mssql /var/opt/mssql/
```







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 14): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (87 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (5 + 4):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (2 + 2): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (10 + 9): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (2 + 4):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (4 + 2): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (21 + 0): **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (5 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新 + 更新 (0 + 0):**資料移轉小幫手 (DMA) sql**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


