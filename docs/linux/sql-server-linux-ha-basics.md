---
title: Linux 部署的 SQL Server 可用性基本概念 |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: f311d9c3116083120b97fa78486242939a438de9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006100"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux 部署的 SQL Server 可用性基本概念

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

開頭[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]支援 Linux 和 Windows 上。 要以 Windows 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]資料庫和執行個體需要高度可用 Linux 底下。 本文章涵蓋技術層面的計劃和部署高可用性以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]資料庫和執行個體，以及一些從以 Windows 為基礎的安裝差異。 因為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 專業人員和 Linux 可能的新功能可能不熟悉[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]專業人員文件有時介紹可能熟悉一些與其他人不熟悉的概念。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 部署的可用性選項
除了備份和還原，相同的三個可用性功能則是在 Linux 上使用以 Windows 為基礎的部署項目：
-   Always On 可用性群組 (Ag)
-   Alwayson 容錯移轉叢集執行個體 (Fci)
-   [記錄傳送](sql-server-linux-use-log-shipping.md)

在 Windows，Fci 一律需要基礎 Windows Server 容錯移轉叢集 (WSFC)。 根據部署案例中，AG 通常需要基礎 WSFC，與例外狀況正在新 variant 中無[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 在 Linux 中沒有 WSFC。 叢集在 Linux 中的實作一節所述[在 Linux 上的 Pacemaker Always On 可用性群組和容錯移轉叢集執行個體](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)。

## <a name="a-quick-linux-primer"></a>快速的 Linux 入門
某些 Linux 安裝可能安裝使用介面中，大部分並不是，這表示，幾乎將一切都在作業系統層級在透過命令列完成。 此命令列，在 Linux 領域中常見的字詞是*bash 殼層*。

在 Linux 中，許多命令需要許多項目必須在 Windows Server 系統管理員身分執行時，如同使用提高的權限執行。 有兩種主要的方法，以提高的權限來執行：
1. 在適當的使用者內容中執行。 若要變更為不同的使用者，請使用命令`su`。 如果`su`本身上執行而不需要使用者名稱，只要您知道密碼，您現在會在殼層中作為*根*。
   
2. 若要執行動作更多一般和安全性意識方式是使用`sudo`之前執行任何動作。 在此範例的許多本文使用`sudo`。

每一個都有各種不同的參數和選項可以線上研究一些常用命令：
-   `cd` -將目錄變更
-   `chmod` -變更檔案或目錄的權限
-   `chown` -變更檔案或目錄的擁有權
-   `ls` – 顯示目錄的內容
-   `mkdir` – 磁碟機上建立資料夾 （目錄）
-   `mv` – 將檔案從一個位置移至另一個
-   `ps` – 顯示所有的工作處理序
-   `rm` -刪除伺服器上的本機檔案
-   `rmdir` – 刪除資料夾 （目錄）
-   `systemctl` -啟動、 停止或啟動服務
-   文字編輯器命令。 在 Linux 上，有各種不同的文字編輯器選項，例如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>一般工作的可用性組態[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上
本章節涵蓋通用於所有以 Linux 為基礎的工作[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

### <a name="ensure-that-files-can-be-copied"></a>請確定可以複製檔案
將檔案從一部伺服器複製到另一個是一項工作都能使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該能夠執行在 Linux 上。 這項工作是非常重要的 AG 組態。

Linux 及 Windows 為基礎的安裝，可以存在權限問題等項目。 不過，熟悉如何在 Windows 上，將複製伺服器對伺服器可能不熟悉如何在 Linux 上進行。 常見的方法是使用命令列公用程式`scp`，這代表 「 安全複製。 在幕後`scp`使用 OpenSSH。 SSH 代表安全殼層。 根據 Linux 散發套件可能不會安裝 OpenSSH 本身。 如果不存在，就必須先安裝 OpenSSH。 如需有關設定 OpenSSH 的詳細資訊，請參閱下列連結以取得每個散發的資訊：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

當使用`scp`，如果它不是來源或目的地，您必須提供伺服器的認證。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

將檔案 MyAGCert.cer 複製到另一部伺服器上所指定的資料夾。 請注意，您必須有權限 – 和可能擁有權 – 要複製的檔案，因此`chown`可能也需要複製之前所採用。 同樣地，在接收端，適當的使用者需要管理檔案的存取。 例如，若要還原該憑證檔案，`mssql`使用者必須能夠存取它。

Samba，也就是伺服器訊息區 (SMB) 的 Linux 變體，也可用來建立這類存取的 UNC 路徑的共用`\\SERVERNAME\SHARE`。 如需有關設定 Samba 的詳細資訊，請參閱下列連結以取得每個散發的資訊：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

也可以使用以 Windows 為基礎的 SMB 共用;以 Linux 為基礎，只要 Samba 用戶端部分已正確設定主控您建立的 Linux 伺服器上不需要 SMB 共用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和共用有正確的存取權。 對於混合式環境中，這會是一種方法運用現有的基礎結構以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

很重要的一點是，Samba 部署的版本應該是 SMB 3.0 相容。 當已加入 SMB 支援[!INCLUDE[sssql11-md](../includes/sssql11-md.md)]，它必須支援 SMB 3.0 的所有共用。 如果使用 Samba 共用並不是 Windows Server，Samba 為基礎的共用應該使用 Samba 4.0 或更新版本，並在理想情況下 4.3 或更新版本，支援 SMB 3.1.1。 理想的 SMB 和 Linux 上的資訊來源是[SMB3 中 Samba](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)。

最後，使用網路檔案系統 (NFS) 共用是一個選項。 使用 NFS 不是以 Windows 為基礎的部署選項[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，且僅用於以 Linux 為基礎的部署。

### <a name="configure-the-firewall"></a>設定防火牆
類似於 Windows，Linux 散發套件有內建的防火牆。 如果貴公司使用外部防火牆的伺服器，停用防火牆，在 Linux 中的可能可以接受。 不過，不論其中已啟用防火牆，連接埠必須開啟。 下表列出常見的連接埠進行高可用性[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上的部署。

| 通訊埠編號 | 類型     | 描述                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | （如果使用） samba – 結束點對應程式                                                                                          |
| 137         | UDP      | （如果使用） samba – NetBIOS 名稱服務                                                                                      |
| 138         | UDP      | （如果使用） samba – NetBIOS 資料包                                                                                          |
| 139         | TCP      | （如果使用） samba – NetBIOS 工作階段                                                                                           |
| 445         | TCP      | （如果使用） samba – SMB 透過 TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – 預設連接埠;如有需要，可以使用變更 `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP、UDP | NFS （如果使用）                                                                                                               |
| 2224        | TCP      | Pacemaker – 使用 `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – 需要有 Pacemaker 遠端節點                                                                    |
| 3260        | TCP      | iSCSI 啟動器 （如果使用） – 可以更改中`/etc/iscsi/iscsid.config`(RHEL)，但應符合的 iSCSI 目標的連接埠 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -AG 端點; 使用預設通訊埠建立端點時，可以變更                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – 如果使用多點傳送的 UDP，Corosync 所需                                                                     |
| 5405        | UDP      | Pacemaker – Corosync 所需                                                                                            |
| 21064       | TCP      | Pacemaker – 所需的資源使用 DLM                                                                                 |
| 變數    | TCP      | AG 端點的連接埠。預設值是 5022                                                                                           |
| 變數    | TCP      | NFS – 連接埠`LOCKD_TCPPORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                              |
| 變數    | UDP      | NFS – 連接埠`LOCKD_UDPPORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                              |
| 變數    | TCP/UDP  | NFS – 連接埠`MOUNTD_PORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                                |
| 變數    | TCP/UDP  | NFS – 連接埠`STATD_PORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                                 |

可能由 Samba 的其他連接埠，請參閱 < [Samba 連接埠使用量](https://wiki.samba.org/index.php/Samba_Port_Usage)。

相反地，在 Linux 服務的名稱也可以新增為例外狀況，而不是連接埠;比方說， `high-availability` pacemaker。 如果這是您想要追求的方向，請參閱您的散發套件的名稱。 例如，在 RHEL 上在 Pacemaker 中新增的命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火牆文件：**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>安裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]套件的可用性
以 Windows 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安裝，有些則不，甚至在基本引擎安裝中，會安裝某些元件。 在僅限 Linux[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]引擎會安裝為安裝程序的一部分。 所有其他項目是選擇性的。 針對高可用性[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]下的執行個體，應該使用安裝兩個套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]:[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式 (*mssql server agent*) 和高可用性 (HA) 套件 (*mssql server-ha*)。 雖然[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是就技術上而言是選擇性的它是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的工作排程器且不需要記錄傳送，因此建議您安裝。 在以 Windows 為基礎的安裝，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]不是選擇性的代理程式。

>[!NOTE]
>對於新手[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的內建工作排程器。 它是常見的方法，讓 Dba 來排程備份和其他等項目[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]維護。 不同於 Windows 型安裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]何處[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是完全不同的服務，在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式內容中執行[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]本身。

當以 Windows 為基礎的組態設定 Ag 或 Fci 時，它們是叢集感知。 叢集感知功能意謂著[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]具有特定資源 WSFC 知道 （sqagtres.dll 和 Fci 的 Ag hadrres.dll 的 sqsrvres.dll） 相關的 Dll，以及用來確保 WSFC[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]叢集的功能已啟動、 執行，並正常運作。 因為叢集外部不是只為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]但本身的 Linux，Microsoft 不得不程式碼相當於以 Linux 為基礎的 AG 和 FCI 部署的資源 DLL。 這是*mssql server-ha*套件，也稱為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的 Pacemaker 資源代理程式。 若要安裝*mssql server-ha*封裝，請參閱[安裝 HA 和 SQL Server Agent 的封裝](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)。

其他選擇性的套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文檢索搜尋 (*mssql-server-fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql server 是*)，不是針對 FCI 或 AG 的高可用性的必要項。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Always On 可用性群組和容錯移轉叢集執行個體，在 Linux 上的 pacemaker
如先前所述，目前支援 microsoft Ag 和 Fci 的叢集機制是使用 Corosync Pacemaker。 此章節將涵蓋基本的資訊來了解方案，以及如何規劃和部署針對[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]組態。

### <a name="ha-add-onextension-basics"></a>HA 附加的/擴充基本概念
目前支援的散發套件的所有寄送 「 高可用性附加-的/延伸模組，此作業取決於叢集堆疊 Pacemaker。 此堆疊會包含兩個主要元件： Pacemaker 和 Corosync。 堆疊的所有元件都如下：
-   Pacemaker – 叢集元件，跨叢集的電腦，像是座標的核心。
-   Corosync – 架構和一組 Api，提供像是仲裁、 重新啟動失敗的處理程序等等的能力。
-   libQB – 提供一些事，像是記錄。
-   資源代理程式 – 提供，讓應用程式可以整合 Pacemaker 的特定功能。
-   柵欄代理程式 – 指令碼功能，協助隔離的節點，並處理它們，如果有問題。
    
> [!NOTE]
> 叢集堆疊通常稱為 Pacemaker Linux 領域中。

此解決方案是在某些方面類似，但在許多方面不同於部署使用 Windows 叢集的組態。 在 Windows，群集中，稱為 Windows Server 容錯移轉叢集 (WSFC) 可用性形式是內建作業系統，並可讓您能夠建立 WSFC 容錯移轉叢集，預設會停用的功能。 在 Windows，Ag Fci WSFC 為建置基礎，並共用緊密整合，因為特定的資源所提供的 DLL [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 此緊密結合的解決方案可能是也因為它是由一家供應商所有。

![](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上，而每個支援的散發有 Pacemaker，每個散發可以自訂，並有稍微不同的實作和版本。 其中一些差異會反映在這篇文章中的指示。 此叢集的圖層的開放原始碼，因此即使它隨附的散發套件時，不緊密整合的方式 WSFC 是在 Windows 下。 這就是為什麼 Microsoft 會提供*mssql server-ha*，以便[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和 Pacemaker 堆疊可關閉 以，但不完全相同，體驗 Ag 和 Fci 在 Windows 下。

如需 Pacemaker 的完整文件，包括的所有項目都有完整的參考資訊，適用於 RHEL 和 SLES 更深入的說明：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 沒有可用性的指南。

如需整個堆疊的詳細資訊，請參閱官方[Pacemaker 文件頁面](http://clusterlabs.org/doc/)Clusterlabs 站台上。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念與術語
本節說明常見的概念和術語的 Pacemaker 實作。

#### <a name="node"></a>節點
節點是參與叢集的伺服器。 Pacemaker 叢集原本就支援最多 16 個節點。 如果 Corosync 未在其他節點上執行，但 Corosync 是需要，可能會超過此數字[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 因此，最大節點數目的叢集可以有任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-根據的設定為 16，這是 Pacemaker 限制，而且不執行任何動作與 Ag 或 Fci 所加諸的最大限制[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 

#### <a name="resource"></a>資源
WSFC 和 Pacemaker 叢集有資源的概念。 資源是在叢集中，例如磁碟或 IP 位址的內容中執行的特定功能。 例如，在 Pacemaker FCI 和 AG 資源可以取得建立。 這不是要在 WSFC 中，您會看到其中有何不同[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]fci 資源還是 AG 資源時設定 AG，但並不完全相同因為方式的基礎差異[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]與 Pacemaker 整合。

Pacemaker 會具有標準和複製的資源。 複製資源是在所有節點上同時執行。 範例會在達到負載平衡的多個節點執行的 IP 位址。 取得為 Fci 建立的任何資源會使用標準的資源，因為只有一個節點可以裝載 FCI 在任何指定時間。

建立 AG 時，它會需要一種特殊的形式的複製資源，名叫多重狀態的資源。 雖然 AG 只能有一個主要複本，AG 本身正在執行的所有節點設定為搭配使用，並可能會允許唯讀存取權等項目。 這是節點的 「 即時 」 使用，因為資源都有兩種狀態的概念： 主要和從屬。 如需詳細資訊，請參閱 <<c0> [ 多重狀態的資源： 有多個模式的資源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>資源群組/設定
類似於 WSFC 中的角色，Pacemaker 叢集有資源群組的概念。 （稱為 sles 的一組） 的資源群組是一起運作，而且可以從一個節點到另一個當做單一單位容錯移轉的資源集合。 資源群組不能包含設定為主要/從屬; 的資源因此，它們無法使用的 Ag。 雖然您可以使用的資源群組，Fci 的它不是通常是建議的設定。

#### <a name="constraints"></a>條件約束
Wsfc 有各種資源，以及像是告知兩個不同的資源之間的父子式關聯性的 WSFC 相依性的參數。 相依性是只是告訴 WSFC 資源必須在線上的第一次的規則。

Pacemaker 叢集沒有相依性的概念，但有限制。 有三種類型的條件約束： 共置、 位置和順序。
-   應該在相同的節點上執行兩個資源，會強制執行的共置條件約束。
-   位置條件約束會告知 Pacemaker 叢集資源可以 （或無法） 執行。
-   排序條件約束會告知 Pacemaker 叢集所在的資源應該啟動的順序。

> [!NOTE]
> 因為所有項目都被視為單一單位，就不需要在資源群組中，資源共置條件約束。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁、 柵欄代理程式和 STONITH
在 Pacemaker 的仲裁是有點類似 WSFC 的概念。 整個叢集的仲裁機制的目的是確保叢集保持啟動並執行。 WSFC 和 HA 附加元件，針對 Linux 發行版本都有 概念的投票，它會將其中的每個節點都會計入仲裁。 您想要取得多數票，否則在最糟的情況下，叢集將會關閉。

不同於 WSFC，沒有任何見證資源，才能使用仲裁。 WSFC 中，例如目標是讓投票者奇數數目。 仲裁組態都有不同的比 Fci 的 Ag 的考量。

Wsfc 會監視參與節點的狀態，並發生問題時，請處理它們。 更新版本的 Wsfc 提供這類功能做為隔離的異常行為或無法使用的節點 （節點不在、 網路通訊已相應減少，依此類推）。 在 Linux 方面，這種類型的功能會提供柵欄代理程式。 概念，有時稱為隔離。 不過，這些柵欄代理程式通常專屬於部署，而且通常由硬體廠商和某些軟體廠商，例如提供 hypervisor 的任何人提供。 例如，VMware 提供柵欄代理程式可以使用適用於 Linux Vm 使用 vSphere 虛擬化。

仲裁和隔離繫結到另一個概念或呼叫 STONITH，限定標頭中的其他節點。 STONITH 被需要有支援的 Pacemaker 叢集，所有的 Linux 發行版本上。 如需詳細資訊，請參閱 < [Red Hat 高可用性叢集中隔離](https://access.redhat.com/solutions/15575)(RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf`檔案包含叢集的設定。 此檔案位於`/etc/corosync`。 在正常的日常作業的過程中此檔案應該永遠不需要進行編輯，如果叢集已正確設定。

#### <a name="cluster-log-location"></a>叢集記錄檔位置
Pacemaker 叢集的記錄檔位置是根據散發而有所不同。
-   RHEL 與 SLES- `/var/log/cluster/corosync.log`
-   Ubuntu- `/var/log/corosync/corosync.log`

若要變更預設的記錄位置，請修改`corosync.conf`。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>計劃的 Pacemaker 叢集 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
本章節將討論規劃 Pacemaker 叢集的重點。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>適用於虛擬化以 Linux 為基礎的 Pacemaker 叢集 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
使用虛擬機器來部署以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Ag 和 Fci 的部署都會受到與以 Windows 為基礎的與其相同的規則。 沒有一組基本的規則來支援虛擬化[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]由 Microsoft 提供的部署[Microsoft 支援知識庫 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)。 不同的 hypervisor，例如 Microsoft 的 HYPER-V 和 VMware ESXi 可能除此之外，，有不同的變異數，因為平台本身的差異。

說到 Ag 和 Fci 下虛擬化，請確定指定的 Pacemaker 叢集的節點，設定反親和性。 當設定為高可用性，在 AG 或 FCI 組態中，裝載的 Vm[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該永遠不會在同一台 hypervisor 主機上執行。 比方說，如果部署兩個節點 FCI 時，那里需要要*至少*三個 hypervisor 主機，因此，某處的其中一個 Vm 裝載一個節點移發生主機故障時，特別是當使用功能像 Live移轉或 vMotion。

如需詳細資訊，請參閱：
-   Hyper V 文件 –[使用客體叢集以提供高可用性](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   （撰寫 Windows 為基礎的部署，但大部分的概念仍套用） – 白皮書[規劃高可用性的任務關鍵性 SQL Server 部署使用 VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>使用 stonith 進行與 Pacemaker 叢集 RHEL 尚不支援 hyper-v。 之前的支援，如需詳細資訊和更新，請參閱[RHEL 高可用性叢集的支援原則](https://access.redhat.com/articles/29440#3physical_host_mixing)。

### <a name="networking"></a>網路
不同於 WSFC，Pacemaker 不需要專用的名稱或至少一個專用的 IP 位址 Pacemaker 叢集本身。 Ag 和 Fci 會需要 （請參閱每個，如需詳細資訊的文件） 的 IP 位址，而不是名稱，因為沒有任何網路名稱資源。 SLES 允許的 IP 位址，以便於管理，組態，但不是必要項目，如中所見[建立 Pacemaker 叢集](sql-server-linux-deploy-pacemaker-cluster.md#create)。

WSFC 中，例如 Pacemaker 偏好備援網路，這表示不同的網路卡 （Nic 或實體的 pNICs） 擁有個別的 IP 位址。 根據叢集組態中，每個 IP 位址會有所謂的它自己的信號。 不過，使用 Wsfc 今日，許多實作虛擬化或公用雲端中，其實只有一個虛擬化 NIC (vNIC) 提供給伺服器。 如果所有 pNICs 和 Vnic 都連接到相同的實體或虛擬交換器，則沒有真正的備援在網路層，所以設定多個 Nic 的虛擬機器的假象。 網路備援通常內建 hypervisor 虛擬化部署，並明確建置到公用雲端。

具有多個 Nic 和 WSFC 和 Pacemaker 的一項差異是 Pacemaker，可讓多個 IP 位址位於相同的子網路，而 WSFC 則否。 如需有關多重子網路和 Linux 叢集的詳細資訊，請參閱文章[設定多個子網路](sql-server-linux-configure-multiple-subnet.md)。

### <a name="quorum-and-stonith"></a>仲裁和 STONITH
仲裁組態和需求相關的部署 AG 或 FCI 特定部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

STONITH 是為了支援的 Pacemaker 叢集。 使用 從發佈文件來設定 STONITH。 例如，在[儲存體為基礎的隔離](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)sles。 另外還有 ESXI 型解決方案的 VMware vCenter 的 STONITH 代理程式。 如需詳細資訊，請參閱 < [Stonith 外掛程式的代理程式的 VMWare VM VCenter SOAP 隔離 (Unofficial)](https://github.com/olafrv/fence_vmware_soap)。

> [!NOTE]
> 在撰寫這篇文章，HYPER-V 並沒有方案 STONITH。 這是適用於內部部署部署，而且也會影響以 Azure 為基礎的 Pacemaker 部署使用 RHEL 等某些散發套件。

### <a name="interoperability"></a>互通性
本節說明如何以 Linux 為基礎的叢集進行互動使用 WSFC 或其他 Linux 發行版本。

#### <a name="wsfc"></a>WSFC
目前沒有任何直接的方式，WSFC 和 Pacemaker 叢集一起運作。 這表示無法建立 AG 或 FCI 可跨 WSFC 和 Pacemaker。 不過，有兩種互通性解決方案，這兩種專為 Ag。 FCI 可以參與跨平台組態的唯一方法是正在參與內這兩種情況的其中一個的執行個體：
-   None 叢集類型 AG。 如需詳細資訊，請參閱 Windows[可用性群組文件](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分散式的 AG，也就是一種特殊類型，可讓兩個不同的 Ag，設定為其自己的可用性群組的可用性群組。 如需有關分散式 Ag 的詳細資訊，請參閱文件[分散式可用性群組](../database-engine/availability-groups/windows/distributed-availability-groups.md)。

#### <a name="other-linux-distributions"></a>其他 Linux 散發套件
在 Linux 上的 Pacemaker 叢集的所有節點都必須在相同的散發。 比方說，這表示，RHEL 節點不能有 SLES 節點的 Pacemaker 叢集的一部分。 主要的原因先前所述： 散發套件可能會有不同的版本和功能，讓項目可能無法正確運作。 混合的散發有相同的 story 混合使用 Wsfc 和 Linux： 使用 [無] 或分散式 Ag。

## <a name="next-steps"></a>後續的步驟
[Pacemaker 叢集部署的 SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)
