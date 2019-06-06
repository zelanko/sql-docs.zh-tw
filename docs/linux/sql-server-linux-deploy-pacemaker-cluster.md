---
title: 部署在 Linux 上的 SQL server 的 Pacemaker 叢集 |Microsoft Docs
description: 本教學課程會示範如何在 Linux 上的 SQL server 部署 Pacemaker 叢集。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: be1bae381cf9eb07180299130917cb6cbf3bfec3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705548"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>部署在 Linux 上的 SQL server 的 Pacemaker 叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程文件的部署的 Linux Pacemaker 叢集所需的工作[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Always On 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI)。 不同於緊密結合的 Windows Server /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]堆疊、 建立 Pacemaker 叢集，以及 Linux 上的可用性群組 (AG) 設定可以進行之前或之後安裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 整合和部署 AG 或 FCI 的 Pacemaker 一部分的資源組態完成之後設定叢集。
> [!IMPORTANT]
> 未使用 None 叢集類型 AG*不*需要 Pacemaker 叢集，同時也不可以它受 Pacemaker。 

> [!div class="checklist"]
> * 安裝高可用性附加元件，並安裝 Pacemaker。
> * 準備 Pacemaker （RHEL 和僅限 Ubuntu） 的節點。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server HA 和 SQL Server Agent 的封裝。
 
## <a name="prerequisite"></a>必要條件
[安裝 SQL Server 2017](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安裝高可用性附加元件
使用下列語法，以安裝 Linux 的每個散發的高可用性 (HA) 附加元件所組成的套件。 

**Red Hat Enterprise Linux (RHEL)**
1.  註冊伺服器，請使用下列語法。 系統會提示您輸入有效的使用者名稱和密碼。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出可用的集區進行註冊。
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  執行下列命令以 RHEL 高可用性相關聯的訂用帳戶
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    何處*PoolId*是從上一個步驟的高可用性訂用帳戶的集區識別碼。
    
4.  啟用要能夠使用高可用性附加元件儲存機制。
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  安裝 Pacemaker。
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

YaST 中安裝高可用性模式，或做為伺服器的主要安裝的一部分。 可以使用 ISO/DVD 完成安裝，做為來源，或藉由線上取得它。
> [!NOTE]
> 在 SLES，在建立叢集時，取得初始化 HA 附加元件。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>準備節點的 Pacemaker （RHEL 和僅限 Ubuntu）
Pacemaker 本身會使用名為通訊群組上建立的使用者*hacluster*。 RHEL 和 Ubuntu 上安裝 HA 附加元件時，取得建立使用者。
1. 每個伺服器上將做為 Pacemaker 叢集的節點，建立可供叢集使用者的密碼。 在範例中使用的名稱是*hacluster*，但可以使用任何名稱。 名稱和密碼必須參與 Pacemaker 叢集的所有節點上相同。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 在將成為 Pacemaker 叢集一部分的每個節點，啟用並啟動`pcsd`服務使用下列命令 （RHEL 和 Ubuntu）：

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   然後執行
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   若要確定`pcsd`已啟動。
3. 啟用 Pacemaker 叢集的每個可能的節點上的 Pacemaker 服務。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   在 Ubuntu 上，您會看到錯誤：
   
   *pacemaker 預設開始包含沒有 runlevels，正在中止。*
   
   此錯誤是已知的問題。 忽略錯誤，啟用 Pacemaker 服務成功，但未來在某個時間點會修正此 bug。
   
4. 接下來，建立並啟動 Pacemaker 叢集。 沒有一項差異 Ubuntu 與 RHEL，在此步驟。 在這兩個發行版本中上, 安裝`pcs`RHEL，執行此命令上的 Pacemaker 叢集會終結任何現有的設定可設定預設的組態檔，並建立新的叢集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>建立 Pacemaker 叢集 
本節說明如何建立和設定的每個散發的 Linux 叢集。

**RHEL**

1. 授權的節點
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   何處*NodeX*是節點的名稱。
2. 建立叢集
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   何處*PMClusterName*是指派給 Pacemaker 叢集的名稱並*Nodelist*是以空格分隔的節點名稱的清單。

**Ubuntu**

設定 Ubuntu 與 RHEL 如下。 不過，還有一項主要差異： 安裝 Pacemaker 套件會建立叢集，啟用和啟動的基底組態`pcsd`。 如果您嘗試將完全遵循 RHEL 指示設定 Pacemaker 叢集，您會收到錯誤。 若要修正此問題，請執行下列步驟： 
1. 移除每個節點的 Pacemaker 預設設定。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 請遵循建立 Pacemaker 叢集 RHEL 節的步驟。

**SLES**

建立 Pacemaker 叢集的程序是在 SLES 上比在 RHEL 和 Ubuntu 截然不同。 下列步驟說明如何建立以 SLES 的叢集。
1. 開始執行的叢集設定程序 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   在其中一個節點。 未設定 NTP，而且位於沒有監視程式的裝置，您可能會提示您。 這是正常的項目啟動並執行。 如果您使用的儲存體為基礎的 SLES 的內建隔離，監視程式被與 STONITH。 NTP 和看門狗可以在稍後設定。
   
2. 系統會提示您設定 Corosync。 系統會要求您要繫結，以及多點傳送的位址和連接埠的網路位址。 網路位址是您使用; 的子網路比方說，192.191.190.0。 您可以接受預設值在每個提示字元中，或視需要變更。
   
3. 接下來，您會問您是否設定 SBD，也就是以磁碟為基礎的隔離。 如有需要，可以稍後再進行此設定。 如果不是 SBD 設定不同於在 RHEL 和 Ubuntu 上`stonith-enabled`會依預設會設定為 false。
   
4. 最後，您會問您是否設定系統管理 IP 位址。 此 IP 位址為選擇性，但功能類似於 Windows Server 容錯移轉叢集 (WSFC) 在於，它用來連線至其透過 HA Web Konsole (HAWK) 叢集中建立的 IP 位址的 IP 位址。 此設定時，也會是選擇性項目。
   
5. 請確定叢集發出已啟動並執行 
   ```bash
   sudo crm status
   ```
   
6. 變更*hacluster*密碼 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果您設定系統管理 IP 位址，您可以測試在瀏覽器中，這也會測試的密碼變更*hacluster*。
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 在另一個 SLES 伺服器將成為叢集的節點上執行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出現提示時，輸入名稱或 IP 位址，已設定為在先前步驟中叢集的第一個節點的伺服器。 伺服器是做為節點新增至現有的叢集。
   
10. 確認節點已成功發行 
   ```bash
   sudo crm status
   ```
   
11. 變更*hacluster*密碼 
   ```bash
   sudo passwd hacluster
   ```
   
12. 重複步驟 8-11 為所有其他伺服器新增至叢集。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安裝 SQL Server HA 和 SQL Server Agent 的封裝
使用下列命令來安裝 SQL Server HA 套件和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式，如果不已安裝。 在安裝之後安裝 HA 套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需要重新啟動[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，才能使用。 這些指示假設，Microsoft 套件存放庫已設定好，因為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該在此時安裝。
> [!NOTE]
> - 如果您不會使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]記錄傳送或任何其他用途的代理程式，它並沒有安裝，因此封裝*mssql server agent*可以略過。
> - 其他選擇性的套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文檢索搜尋 (*mssql-server-fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql server 是*)，不是針對 FCI 或 AG 的高可用性的必要項。

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何部署 Linux 上的 SQL Server 的 Pacemaker 叢集。 您已學到如何以：
> [!div class="checklist"]
> * 安裝高可用性附加元件，並安裝 Pacemaker。
> * 準備 Pacemaker （RHEL 和僅限 Ubuntu） 的節點。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server HA 和 SQL Server Agent 的封裝。

若要建立及設定 Linux 上的 SQL Server 可用性群組，請參閱：

> [!div class="nextstepaction"]
> [建立及設定可用性群組的 SQL Server on Linux](sql-server-linux-create-availability-group.md)。

