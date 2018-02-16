---
title: "SQL Server 可用性的基本概念 Linux 部署 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: fd2079b0b0186192fc3b55e7a6ccefd25c1a46bc
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Linux 部署的 SQL Server 可用性基本概念

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

從開始[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]適用於 Linux 和 Windows。 例如 windows[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]資料庫和執行個體必須要在 Linux 高可用性。 本文章涵蓋計劃和部署高可用性的技術層面 linux[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]資料庫和執行個體，以及從 windows 安裝的差異。 因為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 專業人員以及 Linux 可能新增的可能新[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]專業人員，文件有時候介紹可能是有些熟悉而且給其他人不熟悉的概念。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 部署的可用性選項
除了備份與還原，相同的三個可用性功能可在 Linux 上與 Windows 為基礎的部署：
-   Alwayson 可用性群組 (Ag)
-   Alwayson 容錯移轉叢集執行個體 (Fci)
-   [記錄傳送](sql-server-linux-use-log-shipping.md)

在 Windows 上，Fci 一律會要求基礎 Windows Server 容錯移轉叢集 (WSFC)。 根據部署案例中，AG 通常需要基礎 WSFC 中，例外狀況是新 variant 中無[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 WSFC 在 Linux 中不存在。 叢集實作在 Linux 中的一節所述[Pacemaker Always On 可用性群組和容錯移轉叢集執行個體在 Linux 上](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)。

## <a name="a-quick-linux-primer"></a>快速 Linux 入門
某些 Linux 安裝可安裝於介面，大部分並不是，這表示，幾乎所有的作業在作業系統層級已完成，透過命令列。 此命令列，在 Linux 世界中的一般術語是*撞殼層*。

在 Linux，許多命令需要方式一樣多個項目需要進行 Windows server 系統管理員身分執行，以提高的權限。 有兩種主要的方法，以提高的權限來執行：
1. 在適當的使用者內容中執行。 若要變更為不同的使用者，請使用命令`su`。 如果`su`執行其本身沒有使用者名稱，只要您知道密碼，您現在將會為殼層*根*。
   
2. 執行動作的多個通用和安全性做出明智的方式是使用`sudo`之前執行的任何項目。 在此範例的許多發行項使用`sudo`。

每一個都有各種參數和選項，可以線上研究一些常用命令：
-   `cd` – 將目錄變更
-   `chmod` -變更檔案或目錄的權限
-   `chown` -變更檔案或目錄的擁有權
-   `ls` – 顯示目錄的內容
-   `mkdir` – 磁碟機上建立資料夾 （目錄）
-   `mv` – 將檔案從一個位置移至另一個
-   `ps` – 顯示所有的工作處理序
-   `rm` – 刪除在本機伺服器上的檔案
-   `rmdir` – 刪除資料夾 （目錄）
-   `systemctl` – 啟動、 停止或啟動服務
-   文字編輯器命令。 在 Linux 上有各種文字編輯器選項，例如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>一般工作的可用性組態[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux
本章節涵蓋通用於所有以 Linux 為基礎的工作[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

### <a name="ensure-that-files-can-be-copied"></a>確認可以複製檔案
將檔案從一部伺服器複製到另一個是一項工作都能使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上應該能夠執行。 這項工作是非常重要 AG 組態。

在 Linux 和 Windows 為基礎的安裝上，可存在於等的權限問題。 不過，那些熟悉如何在 Windows 上複製伺服器可能不熟悉如何在 Linux 上執行。 常見的方法是使用命令列公用程式`scp`，它代表安全複製。 在幕後`scp`使用 OpenSSH。 SSH 代表安全殼層。 Linux 散發套件中，根據本身的 OpenSSH 可能未安裝。 如果不是，OpenSSH 必須先安裝。 如需設定 OpenSSH 的詳細資訊，請參閱下列連結以取得每個發佈的資訊：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

當使用`scp`，如果不是來源或目的地，您必須提供伺服器的認證。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

將檔案 MyAGCert.cer 複製到另一部伺服器上所指定的資料夾。 請注意，您必須有權限 – 且可能擁有權 – 要複製的檔案，因此`chown`也可能需要複製之前所用。 同樣地，在接收端，權限的使用者需要管理檔案的存取。 例如，若要還原該憑證的檔案，`mssql`使用者必須能夠存取它。

Samba，也就是伺服器訊息區 (SMB) 的 Linux 變體，也可用來建立這類存取的 UNC 路徑的共用`\\SERVERNAME\SHARE`。 如需設定 Samba 的詳細資訊，請參閱下列連結以取得每個發佈的資訊：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

也可以用 windows SMB 共用。SMB 共用就不需要是 Linux 為基礎，只要 Samba 用戶端部份主控您建立的 Linux 伺服器上已正確設定[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]共用且正確的存取權。 對於在混合環境中，這會是一種方式運用現有基礎結構，以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

重要的一件事是 Samba 部署的版本應該是 SMB 3.0 相容。 當已加入支援 SMB [!INCLUDE[sssql11-md](../includes/sssql11-md.md)]，它需要所有支援 SMB 3.0 共用。 如果使用 Samba 共用和非 Windows 伺服器，Samba 為基礎的共用應該使用 Samba 4.0 或更新版本，並在理想情況下 4.3 或更新版本，可支援 SMB 3.1.1。 是理想的 SMB 和 Linux 上的資訊來源[中 Samba SMB3](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)。

最後，使用網路檔案系統 (NFS) 共用是一個選項。 使用 NFS 不在 windows 部署中的選項[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，而且只能用於以 Linux 為基礎的部署。

### <a name="configure-the-firewall"></a>設定防火牆
類似於 Windows，Linux 散發套件已內建的防火牆。 如果貴公司使用外部防火牆的伺服器，停用在 Linux 防火牆可能是可接受。 不過，無論啟用防火牆的連接埠必須開啟。 下表說明常見的連接埠進行高可用性[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上的部署。

| 通訊埠編號 | 型別     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba （如果使用） – 端點對應程式                                                                                          |
| 137         | UDP      | Samba （如果使用） – NetBIOS 名稱服務                                                                                      |
| 138         | UDP      | Samba （如果使用） – NetBIOS 資料包                                                                                          |
| 139         | TCP      | Samba （如果使用） – NetBIOS 工作階段                                                                                           |
| 445         | TCP      | Samba （如果使用） – SMB over TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – 預設連接埠。如有需要，可以變更與 `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP、UDP | NFS （如果使用）                                                                                                               |
| 2224        | TCP      | Pacemaker – 使用 `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – 需要有 Pacemaker 遠端節點                                                                    |
| 3260        | TCP      | iSCSI 啟動器 （如果使用） – 可以更改中`/etc/iscsi/iscsid.config`(RHEL)，但應該符合的 iSCSI 目標的連接埠 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -AG 端點; 使用預設通訊埠建立端點時，可以變更                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – 如果使用多點傳送的 UDP，Corosync 所需                                                                     |
| 5405        | UDP      | Pacemaker – Corosync 所需                                                                                            |
| 21064       | TCP      | Pacemaker – 所需的資源使用 DLM                                                                                 |
| 變數    | TCP      | AG 端點連接埠。預設值是 5022                                                                                           |
| 變數    | TCP      | NFS 的連接埠`LOCKD_TCPPORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                              |
| 變數    | UDP      | NFS 的連接埠`LOCKD_UDPPORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                              |
| 變數    | TCP/UDP  | NFS 的連接埠`MOUNTD_PORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                                |
| 變數    | TCP/UDP  | NFS 的連接埠`STATD_PORT`(位於`/etc/sysconfig/nfs`RHEL 上)                                                 |

Samba 可能使用的其他通訊埠，請參閱[Samba 連接埠使用量](https://wiki.samba.org/index.php/Samba_Port_Usage)。

相反地，在 Linux 服務名稱也可以加入做為例外狀況，而非連接埠。例如， `high-availability` Pacemaker 的。 如果這是您想要執行的方向，請參閱您的發佈名稱。 例如，在上 RHEL 加入 Pacemaker 命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火牆文件集：**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>安裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]可用性的封裝
上以 Windows 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安裝，有些則不是基本引擎安裝中，即使在安裝某些元件。 Linux，只在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]引擎安裝的安裝程序的一部分。 所有其他項目是選擇性的。 針對高可用性[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]下 Linux 的執行個體，應以安裝兩個封裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]:[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式 (*mssql server agent*) 和高可用性 (HA) 套件 (*mssql-伺服器-ha*)。 雖然[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是選擇性技術上來說，它是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的工作排程器中，所需記錄傳送，因此建議您安裝。 在 windows 安裝中，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]不是選擇性的代理程式。

>[!NOTE]
>對於新[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的內建工作排程器。 它是適用於 Dba 排程備份和其他常見的作法[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]維護。 不同的 windows 安裝於[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]其中[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式是完全不同的服務，在 Linux 上[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式內容中執行[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]本身。

當 Ag 或 Fci 在 Windows 架構的組態設定時，它們是叢集感知。 叢集感知功能表示[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]具有特定資源 Dll WSFC 所知道 （sqagtres.dll 和 Fci，Ag 的 hadrres.dll 的 sqsrvres.dll） 以及用來確保 WSFC[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]叢集的功能已啟動、 執行，並正常運作。 因為叢集不外部只為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]但 Linux 本身、 Microsoft 有程式碼適用於以 Linux 為基礎的 AG 和 FCI 部署的資源 DLL 的對等項目。 這是*mssql-伺服器-ha*封裝，也稱為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Pacemaker 資源代理程式。 若要安裝*mssql-伺服器-ha*封裝，請參閱[安裝高可用性和 SQL Server Agent 的封裝](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)。

其他選擇性套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文檢索搜尋 (*mssql-伺服器-fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql 伺服器是*)，不是高可用性、 FCI 或 AG 的必要項。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Alwayson 可用性群組和容錯移轉叢集執行個體，在 Linux 上 pacemaker
為先前所述，目前支援 microsoft Ag 和 Fci 的唯一叢集機制是與 Corosync Pacemaker。 此章節將涵蓋基本的資訊來了解方案，以及如何規劃和部署為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]組態。

### <a name="ha-add-onextension-basics"></a>HA 附加 on/延伸基本概念
所有目前支援的發行版本現有附隨 「 高可用性附加-on/延伸模組，根據叢集堆疊 Pacemaker。 此堆疊會結合兩個主要元件： Pacemaker 和 Corosync。 堆疊的所有元件都如下：
-   Pacemaker – 核心叢集元件，請在叢集的電腦之間執行之類的座標。
-   Corosync – framework 和組 Api，可提供之類的仲裁，無法重新啟動處理程序等等的能力。
-   libQB – 提供項目，例如記錄。
-   資源代理程式 –，讓應用程式可以整合與 Pacemaker 提供特定功能。
-   柵欄代理程式 – 指令碼/功能，協助隔離節點和處理它們，如果有問題。
    
> [!NOTE]
> 叢集堆疊通常稱為 Pacemaker Linux 世界。

這個解決方案是在某些方面類似，但在許多方面不同於部署使用 Windows 叢集的設定。 在 Windows 中，叢集、 稱為 Windows Server 容錯移轉叢集 (WSFC) 可用性表單是內建作業系統，並讓您建立的 WSFC 容錯移轉叢集，預設會停用的功能。 在 Windows 中，Ag 和 Fci 所建置的 WSFC 上，而且因為特定的資源 DLL 所提供的共用緊密整合[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 這個緊密繫結的解決方案是可行的所以全部從一家供應商。

![](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上每個支援的發佈具有 Pacemaker 可用，而每個發佈可以自訂，而且有稍微不同的實作和版本。 其中一些差異會反映在這篇文章中的指示。 叢集的圖層是開放原始碼，因此即使它隨附了分佈時，不緊密整合以相同方式 WSFC 是在 Windows 下。 這就是為什麼 Microsoft 提供*mssql-伺服器-ha*，如此[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和 Pacemaker 堆疊可關閉 以，但不完全相同，為體驗 Ag 和 Fci 在 Windows 下。

如需 Pacemaker 的完整文件，包括的所有項目是完整的參考資訊，RHEL 和 SLES 的更深入的說明：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 沒有可用性的指南。

如需整個堆疊的詳細資訊，請參閱正式[Pacemaker 文件頁面](http://clusterlabs.org/doc/)Clusterlabs 站台上。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念與術語
本章節記載的一般概念和術語 Pacemaker 實作。

#### <a name="node"></a>節點
節點是參與叢集的伺服器。 Pacemaker 叢集原本就支援最多 16 個節點。 可以超過此數目，如果 Corosync 未執行其他節點上，但需要 Corosync [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 因此，最大節點數目的叢集可以具備任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-根據的設定為 16，這是 Pacemaker 限制，而且與 Ag 或 Fci 所加諸的最大限制無關[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 

#### <a name="resource"></a>資源
WSFC 和 Pacemaker 叢集有資源的概念。 資源是在叢集中，例如磁碟或 IP 位址的內容中執行的特定功能。 例如下 Pacemaker, FCI 和 AG 可以取得建立資源。 這不是與所完成的作業在 WSFC 中，您會看到其中相異[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]使用 fci 資源還是 AG 資源時設定 AG，但並不完全相同，因為基礎差異如何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Pacemaker 與整合。

Pacemaker 具有標準和複製的資源。 複製資源為的所有節點上同時執行。 範例會執行多個節點的負載平衡用途的 IP 位址。 取得建立 Fci 的任何資源使用標準的資源，因為只有一個節點可以裝載 FCI 在任何指定時間。

AG 建立時，它會需要一種特殊的形式的複製資源稱為多重狀態的資源。 AG 只能有一個主要複本，而 AG 本身執行中的所有節點間它已設定運作，且可能會允許唯讀存取權等。 這是節點的 「 即時 」 使用，因為資源有兩個狀態的概念： 主要和備用。 如需詳細資訊，請參閱[多重狀態的資源： 有多個模式的資源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>資源群組集
類似於在 WSFC 中的角色，Pacemaker 叢集有資源群組的概念。 資源群組 （稱為 SLES 中的一組） 是一起運作，且可以從一個節點到另一個當做單一單位容錯移轉的資源集合。 資源群組不能包含設定為主/從; 的資源因此，它們無法用於 Ag。 Fci 的可用資源群組，但並非一般建議的設定。

#### <a name="constraints"></a>條件約束
WSFCs 有各種資源，以及相依性，判斷兩個不同的資源之間的父子式關聯性的 WSFC 之類的參數。 相依性是只要告訴 WSFC 資源需要在線上，第一次的規則。

Pacemaker 叢集沒有相依性的概念，但條件約束。 有三種類型的條件約束： 共置、 位置和順序。
-   共置條件約束會強制執行，不論是否應該在相同的節點上執行兩個資源。
-   位置條件約束會告知 Pacemaker 叢集資源可以 （或無法） 執行的位置。
-   排序條件約束會告知 Pacemaker 叢集資源應該在其中啟動的順序。

> [!NOTE]
> 因為所有這些會當做單一單位出現，並不需要資源群組中，共置條件約束。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁，柵欄代理程式和 STONITH
與在概念上的 WSFC 稍微相似下 Pacemaker 仲裁。 叢集的仲裁機制的目的是確保在叢集中保持啟動且正在執行。 WSFC 和 Linux 發佈的 HA 附加元件有其中的每個節點都會計入仲裁的投票，概念。 您要的多數票，否則在最差的情況下，叢集將會關閉。

不同於在 WSFC 中，沒有任何見證資源，才能使用仲裁。 在 WSFC 中，例如目標是 mínimo el número de 奇數投票。 仲裁組態都有不同於 Fci 的 Ag 的考量。

WSFCs 監視參與節點的狀態，並處理這類問題發生時。 更新版本的 WSFCs 提供這類功能做為隔離異常行為或無法使用的節點 （節點不在、 網路通訊 是，等等）。 在 Linux 方面，這種類型的功能會提供柵欄代理程式。 概念有時候稱為 「 範圍。 不過，這些柵欄代理程式通常專屬於部署，而且通常由硬體廠商和某些軟體廠商，例如提供 hypervisor 所提供。 例如，VMware 提供柵欄代理程式可以使用適用於 Linux Vm 使用 vSphere 虛擬化。

仲裁及柵欄繫結到另一個概念或呼叫 STONITH，羊標頭中的其他節點。 STONITH 才能具有支援的 Pacemaker 叢集上所有 Linux 散發套件。 如需詳細資訊，請參閱[柵欄 Red Hat 高可用性叢集](https://access.redhat.com/solutions/15575)(RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf`檔案是否包含在叢集的設定。 它位於`/etc/corosync`。 在日常作業，此檔案應該永遠不會需要叢集已正確設定需要編輯。

#### <a name="cluster-log-location"></a>叢集記錄檔位置
Pacemaker 叢集記錄檔的位置而有所不同分佈。
-   RHEL 和 SLES- `/var/log/cluster/corosync.log`
-   Ubuntu – `/var/log/corosync/corosync.log`

若要變更預設的記錄位置，請修改`corosync.conf`。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>計劃 Pacemaker 叢集 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
本章節討論規劃 Pacemaker 叢集的重點。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>以 Linux 為基礎的虛擬化 Pacemaker 叢集以提供 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
使用虛擬機器來部署以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]相同的規則與 Windows 架構的與其所涵蓋的 Ag 和 Fci 的部署。 沒有一組基本的規則可支援性的虛擬化[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]由 Microsoft 提供的部署[Microsoft 支援知識庫 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)。 不同的 hypervisor，例如 Microsoft 的 HYPER-V 和 VMware 的 ESXi 可能會在該的變異，因為其本身的平台差異。

當談到 Ag 和 Fci 在虛擬化時，請指定 Pacemaker 叢集中的節點，設定反親和性。 當設定為高可用性在 AG 或 FCI 組態中，裝載的 Vm[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]永遠不應該在同一台 hypervisor 主機上執行。 例如，如果兩個節點 FCI 部署時，會需要*至少*三個 hypervisor 主機，所以的某處主控節點的 vm 主機失敗，請移至其中一個特別是當使用的功能類似 Live移轉或 vMotion。

如需更多特定資訊，請參閱：
-   使用 HYPER-V 的文件 –[使用客體叢集的高可用性](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   （針對撰寫 Windows 為基礎的部署，但是大部分的概念仍適用於） – 白皮書[規劃高可用性、 任務關鍵 SQL Server 部署與 VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL 與 Pacemaker 叢集與 STONITH 尚未支援 hyper-v。 之前的支援，如需詳細資訊和更新，請參閱[RHEL 高可用性叢集的支援政策](https://access.redhat.com/articles/29440#3physical_host_mixing)。

### <a name="networking"></a>網路
不同於 WSFC，Pacemaker 不需要專用的名稱或至少一個專用的 IP 位址 Pacemaker 叢集本身。 Ag 和 Fci 需要 IP 位址 （請參閱文件，如需詳細資訊的每個），而不是名稱，因為沒有任何網路名稱資源。 SLES 允許以便於管理，IP 位址組態，但不是必要項目，如下所示[建立 Pacemaker 叢集](sql-server-linux-deploy-pacemaker-cluster.md#create)。

WSFC 中，例如 Pacemaker 想使用多餘的網路功能，這表示不同的網路卡 （Nic 或實體的 pNICs） 擁有個別的 IP 位址。 根據叢集組態中，每個 IP 位址必須稱它自己的信號。 不過，使用 WSFCs 今天，許多實作會虛擬化或公用雲端在其中其實只有一個虛擬 NIC (vNIC) 呈現給伺服器。 如果所有 pNICs 和 vNICs 都連線至相同的實體或虛擬交換器，就沒有，則為 true 的備援性在網路層，因此設定多個 Nic 的虛擬機器幻影的位元。 網路備援通常 hypervisor 虛擬化部署中，內建，而且會明確建置到公用雲端。

與多個 Nic 與 WSFC Pacemaker 一項差異，是 Pacemaker 可讓多個 IP 位址位於相同子網路，而不在 WSFC。 如需有關多重子網路和 Linux 叢集的詳細資訊，請參閱文章[設定多個子網路](sql-server-linux-configure-multiple-subnet.md)。

### <a name="quorum-and-stonith"></a>仲裁及 STONITH
仲裁組態和需求相關的 AG 或 FCI 特定部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

需要支援的 Pacemaker 叢集 STONITH。 若要設定 STONITH 使用從發佈的文件。 例如，在[儲存體為基礎的隔離](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)sles。 另外還有 ESXI 架構解決方案的 VMware vCenter 的 STONITH 代理程式。 如需詳細資訊，請參閱[Stonith 外掛程式的代理程式的 VMWare VM VCenter SOAP 柵欄 (Unofficial)](https://github.com/olafrv/fence_vmware_soap)。

> [!NOTE]
> 這篇文章撰寫，HYPER-V 沒有方案的 STONITH。 這是適用於在內部部署部署中，而且也會影響以 Azure 為基礎的 Pacemaker 部署使用例如 RHEL 特定分佈。

### <a name="interoperability"></a>互通性
本節說明如何以 Linux 為基礎的叢集可以與互動 WSFC 或於其他 Linux。

#### <a name="wsfc"></a>WSFC
目前合作的 WSFC 和 Pacemaker 叢集沒有直接的方式。 這表示沒有方法可建立 AG 或 FCI 在 WSFC 和 Pacemaker。 不過，有兩種互通性解決方案，這兩種專為 Ag。 FCI 可以參與跨平台組態的唯一方法是如果參與這兩種情況的其中一個內的執行個體：
-   叢集類型為 None AG。 如需詳細資訊，請參閱 Windows[可用性群組的文件](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分散式的 AG，也就是一種特殊的可用性群組可讓兩個不同的 Ag 設定為自己的可用性群組。 如需有關分散式 Ag 的詳細資訊，請參閱文件[分散式可用性群組](../database-engine/availability-groups/windows/distributed-availability-groups.md)。

#### <a name="other-linux-distributions"></a>其他 Linux 散發套件
在 Linux 上 Pacemaker 叢集的所有節點都必須位於相同的通訊群組。 比方說，這表示 RHEL 節點不能有 SLES 節點 Pacemaker 叢集的一部分。 先前所述的主要原因： 發佈可能會有不同的版本和功能，讓項目可能無法正常運作。 混合分佈具有相同的劇本做為混合 WSFCs 和 Linux： 使用 [無] 或分散式 Ag。

## <a name="next-steps"></a>後續的步驟
[Pacemaker 叢集部署的 SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)
