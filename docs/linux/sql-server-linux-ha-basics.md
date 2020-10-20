---
title: Linux 部署的 SQL Server 高可用性基本概念
description: 了解 Linux 上 SQL Server 的高可用性選項，例如 Always On 可用性群組、容錯移轉叢集執行個體 (FCI) 和記錄傳送。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 411fe456ae96afdd5a01c0d6cb649035e121fb1b
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115641"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>適用於 Linux 部署的 SQL Server 可用性基本概念

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

從 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 開始，Linux 和 Windows 上均支援 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如同 Windows 型 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 資料庫和執行個體必須在 Linux 下具有高可用性。 此文章涵蓋規劃和部署高可用性 Linux 型 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 資料庫和執行個體的技術層面，以及一些與 Windows 型安裝的差異。 因為 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 對 Linux 專業人員而言可能是新的，而 Linux 對 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 專業人員而言可能是新的，所以，此文章有時會介紹一些某些人可能很熟悉但其他人並不熟悉的概念。

## <a name="ssnoversion-md-availability-options-for-linux-deployments"></a>適用於 Linux 部署的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 可用性選項
除了備份和還原之外，Linux 上提供了三個與 Windows 型部署所使用的相同可用性功能：
-   Always On 可用性群組 (AG)
-   Always On 容錯移轉叢集執行個體 (FCI)
-   [記錄傳送](sql-server-linux-use-log-shipping.md)

在 Windows 上，FCI 一律需要基礎 Windows Server 容錯移轉叢集 (WSFC)。 視部署案例而定，AG 通常需要基礎 WSFC，但 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 中新的「無」變體除外。 WSFC 不存在於 Linux 中。 Linux 中的叢集實作會在 [Linux 上適用於 Always On 可用性群組和容錯移轉叢集執行個體的 Pacemaker](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux) 一節中進行討論。

## <a name="a-quick-linux-primer"></a>Linux 快速入門
雖然有些 Linux 安裝可能會與介面一併安裝，但大部分都不會，這表示在作業系統層上幾乎所有內容都是透過命令列完成的。 在 Linux 世界中，適用於此命令列的常見詞彙是「Bash 殼層」。

在 Linux 中，許多命令都需要以提高的權限來執行，非常類似於 Windows Server 中必須以系統管理員身分完成許多工作。 有兩個主要方法可使用提高的權限來執行：
1. 在適當使用者的內容中執行。 若要變更為不同的使用者，請使用 `su` 命令。 如果 `su` 是在沒有使用者名稱的情況下單獨執行，只要您知道密碼，現在就能以 *root* 身分位於殼層中。
   
2. 用來執行動作之更常見且具安全性意識的方式，就是在執行任何動作之前先使用 `sudo`。 此文章中有許多範例都會使用 `sudo`。

一些常用命令，其中每一個都有可在線上研究的各種參數和選項：
-   `cd`：變更目錄
-   `chmod`：變更檔案或目錄的權限
-   `chown`：變更檔案或目錄的擁有權
-   `ls`：顯示目錄內容
-   `mkdir`：在磁碟機上建立資料夾 (目錄)
-   `mv`：將檔案從一個位置移到另一個
-   `ps`：顯示所有運作中的程序
-   `rm`：在伺服器上本機刪除檔案
-   `rmdir`：刪除資料夾 (目錄)
-   `systemctl`：啟動、停止或啟用服務
-   文字編輯器命令。 在 Linux 上，有各種文字編輯器選項，例如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-ssnoversion-md-on-linux"></a>Linux 上適用於 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 可用性設定的通用工作
本節涵蓋所有 Linux 型 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署通用的工作。

### <a name="ensure-that-files-can-be-copied"></a>確保可以複製檔案
將檔案從一部伺服器複製到另一部，是 Linux 上任何使用 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的人都應該能夠執行的工作。 此工作對 AG 設定而言非常重要。

權限問題之類的項目均可存在於 Linux 以及 Windows 型安裝上。 不過，熟悉如何在 Windows 上從伺服器複製到伺服器的人，可能不熟悉如何在 Linux 上進行此動作。 常見的方法是使用命令列公用程式 `scp`，這代表安全複製。 在幕後，`scp` 會使用 OpenSSH。 SSH 代表安全殼層。 視 Linux 發行版本而定，可能不會安裝 OpenSSH 本身。 如果未安裝，則必須先安裝 OpenSSH。 如需設定 OpenSSH 的詳細資訊，請參閱下列適用於每個發行版本之連結中的相關資訊：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

使用 `scp` 時，您必須提供伺服器的認證 (如果它不是來源或目的地)。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

將 MyAGCert.cer 檔案複製到另一部伺服器上指定的資料夾。 請注意，您必須擁有檔案的權限 (而且可能需要擁有權) 才能複製它，因此，在複製之前，也可能需要採用 `chown`。 同樣地，在接收端，正確的使用者需要存取權才能操作檔案。 例如，若要還原該憑證檔案，`mssql` 使用者必須能夠存取它。

Samba 是伺服器訊息區 (SMB) 的 Linux 變體，也可以用來建立 UNC 路徑 (例如 `\\SERVERNAME\SHARE`) 所存取的共用。 如需設定 Samba 的詳細資訊，請參閱下列適用於每個發行版本之連結中的相關資訊：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

您也可以使用 Windows 型 SMB 共用；SMB 共用不需要是 Linux 型的，只要 Samba 的用戶端部分會在裝載 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 Linux 伺服器上正確設定，且共用具有適當的存取權即可。 針對混合式環境中的人員，這是利用 Linux 型 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署之現有基礎結構的一種方式。

很重要的一點是，已部署的 Samba 版本應符合 SMB 3.0 規範。 已在 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)] 中新增 SMB 支援時，它需要所有共用才能支援 SMB 3.0。 如果針對共用使用 Samba，而非 Windows Server，則 Samba 型共用應該會使用 Samba 4.0 或更新版本 (最好是 4.3 或更新版本) 來支援 SMB 3.1.1。 SMB 和 Linux 上的良好資訊來源是 [Samba 中的 SMB3](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf) \(英文\)。

最後，可以選擇使用網路檔案系統 (NFS) 共用。 在 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 Windows 型部署上，無法選擇使用 NFS，只能針對 Linux 型部署加以使用。

### <a name="configure-the-firewall"></a>設定防火牆
類似於 Windows，Linux 發行版本具有內建的防火牆。 如果貴公司對伺服器使用外部防火牆，則或許能夠接受在 Linux 中停用防火牆。 不過，不論啟用防火牆的位置為何，都必須開啟連接埠。 下表記載 Linux 上高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署所需的通用連接埠。

| 連接埠號碼 | 類型     | 描述                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS：`rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (如果使用)：結束點對應程式                                                                                          |
| 137         | UDP      | Samba (如果使用)：NetBIOS 名稱服務                                                                                      |
| 138         | UDP      | Samba (如果使用)：NetBIOS 資料包                                                                                          |
| 139         | TCP      | Samba (如果使用)：NetBIOS 工作階段                                                                                           |
| 445         | TCP      | Samba (如果使用)：SMB over TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]：預設連接埠；如有需要，可以使用 `mssql-conf set network.tcpport <portnumber>` 進行變更                       |
| 2049        | TCP、UDP | NFS (如果使用)                                                                                                               |
| 2224        | TCP      | Pacemaker：由 `pcsd` 使用                                                                                                |
| 3121        | TCP      | Pacemaker：如果有 Pacemaker 遠端節點，則為必要項                                                                    |
| 3260        | TCP      | iSCSI 啟動器 (如果使用)：可以在 `/etc/iscsi/iscsid.config` (RHEL) 中改變，但應符合 Internet SCSI 目標的連接埠 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]：用於 AG 端點的預設連接埠；可在建立端點時變更                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker：如果使用多點傳送 UDP，則為 Corosync 的必要項                                                                     |
| 5405        | UDP      | Pacemaker：為 Corosync 的必要項                                                                                            |
| 21064       | TCP      | Pacemaker：為使用 DLM 之資源的必要項                                                                                 |
| 變數    | TCP      | AG 端點埠；預設值為 5022                                                                                           |
| 變數    | TCP      | NFS：適用於 `LOCKD_TCPPORT` 的連接埠 (可在 RHEL 上的 `/etc/sysconfig/nfs` 中找到)                                              |
| 變數    | UDP      | NFS：適用於 `LOCKD_UDPPORT` 的連接埠 (可在 RHEL 上的 `/etc/sysconfig/nfs` 中找到)                                              |
| 變數    | TCP/UDP  | NFS：適用於 `MOUNTD_PORT` 的連接埠 (可在 RHEL 上的 `/etc/sysconfig/nfs` 中找到)                                                |
| 變數    | TCP/UDP  | NFS：適用於 `STATD_PORT` 的連接埠 (可在 RHEL 上的 `/etc/sysconfig/nfs` 中找到)                                                 |

如需 Samba 可能使用的其他連接埠，請參閱 [Samba 連接埠使用方式](https://wiki.samba.org/index.php/Samba_Port_Usage) \(英文\)。

相反地，也可以將 Linux 底下的服務名稱新增為例外狀況，而不是連接埠；例如，適用於 Pacemaker 的 `high-availability`。 如果這是您想要追求的方向，請參閱您的發行版本以了解這些名稱。 例如，在 RHEL 上，要在 Pacemaker 中新增的命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火牆文件：**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-ssnoversion-md-packages-for-availability"></a>安裝 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 套件以取得可用性
在 Windows 型 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 安裝上，即使是在基本的引擎安裝中還是會安裝某些元件，其他的則不會安裝。 在 Linux 底下，只會在安裝過程中安裝 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 引擎。 其他所有項目都是選擇性的。 針對 Linux 底下高可用性的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 執行個體，應該使用 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 來安裝兩個套件：[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*mssql-server-agent*) 和高可用性 (HA) 套件 (*mssql-server-ha*)。 雖然 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent 在技術上是選擇性的，但它是 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的作業排程器，而且是記錄傳送所需的，因此建議安裝。 在 Windows 型安裝上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent 不是選擇性的。

>[!NOTE]
>對於 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的新手而言，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent 是 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的內建工作排程器。 這是 DBA 用來排程備份之類事項和其他 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 維護的常見方式。 不同於 Windows 型的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 安裝 (其中 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent 是一項完全不同的服務)，在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent 會在 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 本身的內容中執行。

在 Windows 型設定上設定 AG 或 FCI 時，它們都是叢集感知的。 叢集感知表示 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 具有 WSFC 知道的特定資源 DLL (適用於 FCI 的 sqagtres.dll 和 sqsrvres.dll，適用於 AG 的 hadrres.dll)，而且是由 WSFC 用來確保 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 叢集功能已啟動、正在執行且正常運作。 由於叢集不只對 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 而言是外部的，對 Linux 本身也是外部的，因此，Microsoft 必須針對 Linux 型的 AG 和 FCI 部署撰寫資源 DLL 對等項目的程式碼。 這是 *mssql-server-ha* 套件，也稱為適用於 Pacemaker 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 資源代理程式。 若要安裝 *mssql-server-ha* 套件，請參閱[安裝 HA 和 SQL Server Agent 套件](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)。

其他適用於 Linux 上之 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 全文檢索搜尋 (*mssql-server-fts*) 和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*) 的選用套件都不是針對 FCI 或 AG 取得高可用性的必要項。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Linux 上適用於 Always On 可用性群組和容錯移轉叢集執行個體的 Pacemaker
如先前所述，Microsoft 目前針對 AG 和 FCI 支援的唯一叢集機制是搭配 Corosync 的Pacemaker。 本節涵蓋瞭解該解決方案的基本資訊，以及如何針對 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 設定進行規劃和部署。

### <a name="ha-add-onextension-basics"></a>HA 附加元件/延伸模組的基本概念
所有目前支援的發行版本都會隨附高可用性附加元件/延伸模組，其會以 Pacemaker 叢集堆疊為基礎。 此堆疊結合兩個主要元件：Pacemaker 和 Corosync。 堆疊的所有元件如下：
-   Pacemaker：核心叢集元件，其會執行在叢集機器上進行協調之類的動作。
-   Corosync：一種架構和一組 API，可提供仲裁、能夠重新啟動失敗程序等動作。
-   libQB：提供記錄等動作。
-   資源代理程式：已提供的特有功能，讓應用程式能夠與 Pacemaker 整合。
-   隔離代理程式：指令碼/功能，可協助隔離節點，並在發生問題時加以處理。
    
> [!NOTE]
> 叢集堆疊在 Linux 世界中通常會稱為 Pacemaker。

此解決方案在某些方面很類似，但在許多方面不同於使用 Windows 部署叢集設定。 在 Windows 中，叢集的可用性形式 (稱為 Windows Server 容錯移轉叢集 (WSFC)) 內建於作業系統中，而能夠建立 WSFC 的功能 (容錯移轉叢集) 預設為停用。 在 Windows 中，AG 和 FCI 建置於 WSFC 之上，而且因為 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 所提供的特定資源 DLL 而共用緊密整合。 這種緊密結合的解決方案基本上是可行的，因為它全都來自一個廠商。

![HA 基本概念](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上，雖然每個支援的發行版本都有可用的 Pacemaker，但每個發行版本都可以自訂，而且實作和版本會有些微不同。 此文章中的指示將反映部分差異。 叢集層是開放原始碼，因此，即使它隨附於發行版本，也不會以 WSFC 在 Windows 底下的相同方式緊密整合。 這就是 Microsoft 提供 *mssql-server-ha* 的原因，因此 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 和 Pacemaker 堆疊可以提供接近 Windows 底下但不完全相同的 AGs 和 FCI 體驗。

如需有關 Pacemaker 的完整文件，包括針對 RHEL 和 SLES 提供所有內容完整參考資訊的更深入說明：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 沒有可用性指南。

如需整個堆疊的詳細資訊，另請參閱 Clusterlabs 網站上的官方 [Pacemaker 文件頁面](https://clusterlabs.org/doc/) \(英文\)。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念和詞彙
本節記載 Pacemaker 實作的常見概念和術語。

#### <a name="node"></a>節點
節點是參與叢集的伺服器。 Pacemaker 叢集原本最多支援 16 個節點。 如果 Corosync 未在其他節點上執行，則可超過此數目，但 Corosync 是 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的必要項。 因此，叢集可針對任何 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 型設定擁有的節點數目上限為 16；這是 Pacemaker 限制，而且不會針對 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 所加諸之 AG 或 FCI 的最大限制執行任何動作。 

#### <a name="resource"></a>資源
WSFC 和 Pacemaker 叢集具備資源的概念。 資源是在叢集內容中執行的特定功能，例如磁碟或 IP 位址。 例如，在 Pacemaker 底下，FCI 和 AG 資源均可建立。 這與 WSFC 中的作業並無任何不同，在設定 AG 時，您會在其中看到適用於 FCI 或 AG 資源的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 資源，但由於 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 與 Pacemaker 整合方式的基礎差異而不會完全相同。

Pacemaker 具有標準和複製資源。 複製資源是在所有節點上同時執行的資源。 基於負載平衡目的，在多個節點上執行的 IP 位址即為一例。 針對 FCI 建立的任何資源都會使用標準資源，因為在任何指定的時間中，只有一個節點可以裝載 FCI。

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

建立 AG 時，它需要一個特殊形式的複製資源 (稱為多狀態資源)。 當 AG 只有一個主要複本時，AG 本身會在其設定來處理的所有節點上執行，而且可能允許唯讀存取之類的動作。 由於這是節點的「即時」使用方式，因此，資源具有兩種狀態的概念：「主要」和「從屬」。 如需詳細資訊，請參閱[多狀態資源：含有多重模式的資源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>資源群組/集合

類似於 WSFC 中的角色，Pacemaker 叢集具有資源群組的概念。 資源群組 (在 SLES 中稱為「集合」) 是一起搭配運作的，且可作為單一單位從一個節點容錯移轉到另外一個節點的資源集合。 資源群組不能包含設為「主要/從屬」的資源；因此，資源群組無法用於 AG。 雖然資源群組可用於 FCI，但這通常不是建議的設定。

#### <a name="constraints"></a>條件約束
WSFC 具有各種適用於資源的參數以及相依性之類的項目，這讓 WSFC 能夠得知兩個不同資源之間的父/子關聯性。 相依性只是一個規則，可用來告知 WSFC 必須先將哪些資源上線。

Pacemaker 叢集沒有相依性的概念，但有限制式。 有三種限制式：共置、位置和排序。
-   共置限制式會強制兩個資源是否應該在相同的節點上執行。
-   位置限制式會告知 Pacemaker 叢集，資源是否可以執行。
-   排序限制式會告知 Pacemaker 叢集，應該啟動資源的順序。

> [!NOTE]
> 資源群組中的資源不需要共置限制式，因為那些限制全都會被視為單一單位。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁、隔離代理程式和 STONITH
概念上，Pacemaker 底下的仲裁會與 WSFC 有點類似。 整個叢集仲裁機制的目的就是要確保叢集能夠保持正常運作。 WSFC 和適用於 Linux 發行版本的 HA 附加元件都具有投票的概念，其中每個節點都會計入仲裁。 您希望讓大部分的投票運作，否則，在最糟的情況下，叢集將會關閉。

與 WSFC 不同的是，沒有任何見證資源可與仲裁搭配使用。 就像 WSFC 一樣，其目標是將投票者的數目保持為奇數。 仲裁設定對於 AG 的考量與 FCI 的不一樣。

WSFC 會監視參與的節點狀態，並在發生問題時加以處理。 較新版的 WSFC 提供如下功能：隔離不正常或無法使用的節點 (節點未開啟、網路通訊已關閉等)。 在 Linux 端，此類型的功能是由隔離代理程式所提供的。 此概念有時稱為隔離。 不過，這些隔離代理程式通常專屬於部署，一般是由硬體廠商和部分軟體廠商所提供，例如，提供 Hypervisor 的人員。 例如，VMware 提供的隔離代理程式可用於使用 vSphere 虛擬化的 Linux VM。

仲裁和隔離會繫結至另一個名為 STONITH (或 Shoot the Other Node in the Head) 的概念。 STONITH 在所有 Linux 發行版本上必須有支援的 Pacemaker 叢集。 如需詳細資訊，請參閱 [Red Hat 高可用性叢集中的隔離](https://access.redhat.com/solutions/15575) \(英文\) (RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf` 檔案包含叢集的設定。 其位於 `/etc/corosync` 中。 在正常的日常作業過程中，如果叢集已正確設定，則不需編輯此檔案。

#### <a name="cluster-log-location"></a>叢集記錄檔位置
Pacemaker 叢集的記錄檔位置會因發行版本而有所不同。
-   RHEL 和 SLES：`/var/log/cluster/corosync.log`
-   Ubuntu：`/var/log/corosync/corosync.log`

若要變更預設的記錄檔位置，請修改 `corosync.conf`。

## <a name="plan-pacemaker-clusters-for-ssnoversion-md"></a>規劃適用於 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 Pacemaker 叢集
本節將討論適用於 Pacemaker 叢集的重要規劃點。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-ssnoversion-md"></a>針對 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 將 Linux 型 Pacemaker 叢集虛擬化
使用虛擬機器來為 AG 和 FCI 部署 Linux 型[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署，會由與其 Windows 型對應項目相同的規則所涵蓋。 在 [Microsoft 支援服務 KB 956893](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment) \(機器翻譯\) 中，有一組基本規則適用於 Microsoft 所提供之虛擬化 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署的支援能力。 由於平台本身的差異，不同的 Hypervisor (例如 Microsoft 的 Hyper-V 和 VMware 的 ESXi) 可能會有不同的差異。

當它進入虛擬化的 AG 和 FCI 時，請確定已針對指定 Pacemaker 叢集的節點設定反親和性。 在 AG 或 FCI 設定中設定以取得高可用性時，裝載 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 VM 應該永遠不會在相同的 Hypervisor 主機上執行。 例如，如果已部署兩個節點的 FCI，則「至少」必須有三部 Hypervisor 主機，以便在某部主機發生故障時，讓其中一部裝載節點的 VM 能夠在某處執行，特別是使用「即時移轉」或 vMotion 之類的功能時。

如需更多詳細資訊，請參閱：
-   Hyper-V 文件：[使用客體叢集以提供高可用性](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn440540(v=ws.11)) \(英文\)
-   白皮書 (專為 Windows 型部署所撰寫，但大部分的概念仍適用)：[使用 VMware vSphere 規劃高可用性、任務關鍵性 SQL Server 部署](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf) \(英文\)

### <a name="networking"></a>網路功能
與 WSFC 不同，Pacemaker 不需要專用名稱，或至少一個固定 IP 位址以供 Pacemaker 叢集本身使用。 AG 和 FCI 將需要 IP 位址 (請參閱各自的文件，以取得詳細資訊)，但不需要名稱，因為沒有網路名稱資源。 SLES 確實允許基於系統管理目的來設定 IP 位址，但並非必要，因為可以在[建立 Pacemaker 叢集中](sql-server-linux-deploy-pacemaker-cluster.md#create)查看它。

就像 WSFC 一樣，Pacemaker 偏好使用多餘的網路功能，亦即具有個別 IP 位址的不同網路卡 (實體的 NIC 或 pNIC)。 就叢集設定而言，每個 IP 位址都有所謂自己的通道。 不過，就像現今的 WSFC，許多實作都會虛擬化或位於公用雲端，實際上只會將單一虛擬化的 NIC (vNIC) 呈現給伺服器。 如果所有 pNIC 和 vNIC 都連線到相同的實體或虛擬交換器，則網路層就不會有任何真正的冗餘，因此，設定多個 NIC 對虛擬機器而言就是一種假像。 網路冗餘通常內建於 Hypervisor 以用來虛擬化部署，而且一定會內建於公用雲端中。

相較於 WSFC，與多個 NIC 和 Pacemaker 的差異在於 Pacemaker 允許相同子網上的多個 IP 位址，但 WSFC 則不允許。 如需多個子網和 Linux 叢集的詳細資訊，請參閱[設定多個子網路](sql-server-linux-configure-multiple-subnet.md)一文。

### <a name="quorum-and-stonith"></a>仲裁和 STONITH
仲裁設定和需求與 AG 或 FCI 特定的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署有關。

支援的 Pacemaker 叢集需要 STONITH。 使用發行版本的文件來設定 STONITH。 適用於 SLES 之[以儲存體為基礎的隔離](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) \(英文\) 即為一例。 針對以 ESXI 為基礎的解決方案，還有適用於 VMware vCenter 的 STONITH 代理程式。 如需詳細資訊，請參閱[適用於 VMWare VM VCenter SOAP 隔離的 STONITH 外掛程式代理程式 (非官方)](https://github.com/olafrv/fence_vmware_soap) \(英文\)。

### <a name="interoperability"></a>互通性
本節記載 Linux 型叢集如何與 WSFC 或其他 Linux 發行版本互動。

#### <a name="wsfc"></a>WSFC
目前，沒有任何直接的方式可讓 WSFC 和 Pacemaker 叢集一起運作。 這表示，沒有任何方式能夠建立跨 WSFC 和 Pacemaker 運作的 AG 或 FCI。 不過，有兩個互通性解決方案，這兩者都是針對 AG 設計的。 FCI 可以參與跨平台設定的唯一方式是，在下列其中一個案例中以執行個體形式來參與：
-   叢集類型為「無」的 AG。 如需詳細資訊，請參閱 Windows [可用性群組文件](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分散式 AG 是一種特殊類型的可用性群組，可讓您將兩個不同的 AG 設定為它們自己的可用性群組。 如需分散式 AG 的詳細資訊，請參閱[分散式可用性群組](../database-engine/availability-groups/windows/distributed-availability-groups.md)一文。

#### <a name="other-linux-distributions"></a>其他 Linux 發行版本
在 Linux 上，Pacemaker 叢集的所有節點都必須位於相同的發行版本上。 例如，這表示 RHEL 節點不能屬於具有 SLES 節點的 Pacemaker 叢集。 此問題的主要原因如先前所述：發行版本可能有不同的版本和功能，因此無法正常運作。 混合發行版本與混合 WSFC 和 Linux 的故事相同：使用「無」或分散式 AG。

## <a name="next-steps"></a>後續步驟
[為 Linux 上的 SQL Server 部署 Pacemaker 叢集](sql-server-linux-deploy-pacemaker-cluster.md)