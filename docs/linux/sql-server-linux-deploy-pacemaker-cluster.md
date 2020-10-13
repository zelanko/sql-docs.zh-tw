---
title: 為 Linux 上的 SQL Server 部署 Pacemaker 叢集
description: 了解如何針對 SQL Server Always On 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI) 部署 Linux Pacemaker 叢集。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: b2e5c3adb5f04f3e138b1d0644a047b8a443fde7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785174"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>為 Linux 上的 SQL Server 部署 Pacemaker 叢集

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本教學課程記載為 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI) 部署 Linux Pacemaker 叢集所需的工作。 與緊密結合的 Windows Server/ [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 堆疊不同，Linux 上的 Pacemaker 叢集建立以及可用性群組 (AG) 設定可以在安裝 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 之前或之後完成。 在設定叢集之後，將完成 AG 或 FCI 部署的 Pacemaker 部分的資源整合和設定。
> [!IMPORTANT]
> 叢集類型為 None 的 AG「不需要」Pacemaker 叢集，也不能由 Pacemaker 管理。 

> [!div class="checklist"]
> * 安裝高可用性附加元件並安裝 Pacemaker。
> * 準備 Pacemaker 的節點 (僅限 RHEL 和 Ubuntu)。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server HA 和 SQL Server Agent 套件。
 
## <a name="prerequisite"></a>必要條件
[安裝 SQL Server 2017](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安裝高可用性附加元件
使用下列語法，針對每個 Linux 散發安裝組成高可用性 (HA) 附加元件的套件。 

**Red Hat Enterprise Linux (RHEL)**
1.  使用下列語法來註冊伺服器。 系統會提示您輸入有效的使用者名稱和密碼。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出可用的集區以進行註冊。
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  執行下列命令，以將 RHEL 高可用性與訂用帳戶產生關聯
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    其中 *PoolId* 是上一個步驟中高可用性訂用帳戶的集區識別碼。
    
4.  讓存放庫能夠使用高可用性附加元件。
    
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

在 YaST 中安裝高可用性模式，或將它作為伺服器主要安裝的一部分進行安裝。 您可以使用 ISO/DVD 做為來源，或將其上線來完成安裝。
> [!NOTE]
> 在 SLES 上，HA 附加元件會在建立叢集時初始化。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>準備 Pacemaker 的節點 (僅限 RHEL 和 Ubuntu)
Pacemaker 本身使用在名為 *hacluster* 的散發上建立的使用者。 在 RHEL 和 Ubuntu 上安裝 HA 附加元件時，會建立使用者。
1. 在將用作 Pacemaker 叢集節點的每部伺服器上，為叢集所要使用的使用者建立密碼。 範例中使用的名稱是 *hacluster*，但可以使用任何名稱。 所有參與 Pacemaker 叢集的節點上的名稱和密碼必須相同。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 在將成為 Pacemaker 叢集一部分的每個節點上，使用下列命令 (RHEL 和 Ubuntu) 啟用並啟動 `pcsd` 服務：

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   然後執行
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   以確保 `pcsd` 已啟動。
3. 在 Pacemaker 叢集的每個可能節點上啟用 Pacemaker 服務。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   在 Ubuntu 上，您會看到錯誤：
   
   *pacemaker Default-Start contains no runlevels, aborting.*
   
   此錯誤是已知的問題。 儘管發生錯誤，啟用 Pacemaker 服務也會成功，而此錯誤 (bug) 將在未來的某個時間點修正。
   
4. 接下來，建立並啟動 Pacemaker 叢集。 在此步驟中，RHEL 和 Ubuntu 有一項差異。 在這兩個散發上，安裝 `pcs` 為 Pacemaker 叢集設定預設組態檔，在 RHEL 上執行此命令會終結任何現有設定並建立新的叢集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>建立 Pacemaker 叢集 
本節說明如何針對每個 Linux 散發建立和設定叢集。

**RHEL**

1. 授權節點
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   其中 *NodeX* 是節點的名稱。
2. 建立叢集
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   其中 *PMClusterName* 是指派給 Pacemaker 叢集的名稱，而 *Nodelist* 是以空格分隔的節點名稱清單。

**Ubuntu**

設定 Ubuntu 與 RHEL 類似。 不過，有一項主要的差異：安裝 Pacemaker 套件會建立叢集的基本設定，並啟用和啟動 `pcsd`。 如果您嘗試完全遵循 RHEL 指示來設定 Pacemaker 叢集，您會收到錯誤。 若要修正此問題，請執行下列步驟： 
1. 從每個節點移除預設的 Pacemaker 設定。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 請遵循 RHEL 區段中的步驟來建立 Pacemaker 叢集。

**SLES**

在 SLES 上建立 Pacemaker 叢集的程序，與在 RHEL 和 Ubuntu 上的程序完全不同。 下列步驟記錄如何使用 SLES 建立叢集。
1. 啟動叢集設定程序，方法是執行 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   在其中一個節點上。 系統可能會提示您未設定 NTP，而且找不到任何監視程式裝置。 這適用於啟動和執行。 如果您使用以儲存體為基礎的 SLES 內建隔離，則監視程式與 STONITH 相關。 之後可以設定 NTP 和監視程式。
   
2. 系統會提示您設定 Corosync。 系統會要求您提供要繫結的網路位址，以及多點傳送位址和連接埠。 網路位址是您要使用的子網路，例如，192.191.190.0。 您可以在每個提示字元中接受預設值，或視需要進行變更。
   
3. 接下來，系統會詢問您是否要設定 SBD，這是以磁碟為基礎的隔離。 此設定可在稍後視需要完成。 如果未設定 SBD，則與 RHEL 和 Ubuntu 不同，`stonith-enabled` 預設會設定為 false。
   
4. 最後，系統會詢問您是否要設定 IP 位址以進行管理。 此 IP 位址是選擇性的，但其功能類似於 Windows Server 容錯移轉叢集 (WSFC) 的 IP 位址，因為它會在叢集中建立 IP 位址，以便透過 HA Web 主控台 (HAWK) 連線到此 IP 位址。 此設定也是選擇性的。
   
5. 確定叢集已啟動且正在執行，方法是發出 
   ```bash
   sudo crm status
   ```
   
6. 將 *hacluster* 密碼變更為 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果您已設定 IP 位址以進行管理，您可以在瀏覽器中進行測試，這也會測試 *hacluster* 的密碼變更。
   ![hacLuster](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 在另一個將成為叢集節點的 SLES 伺服器上，執行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出現提示時，輸入先前步驟中設定為叢集第一個節點的伺服器名稱或 IP 位址。 伺服器會新增為現有叢集的節點。
   
10. 驗證是否新增節點，方法是發出 
   ```bash
   sudo crm status
   ```
   
11. 將 *hacluster* 密碼變更為 
   ```bash
   sudo passwd hacluster
   ```
   
12. 針對要新增至叢集的所有其他伺服器，重複步驟 8-11。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安裝 SQL Server HA 和 SQL Server Agent 套件
使用下列命令來安裝 SQL Server HA 套件和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理程式 (如果尚未安裝)。 在安裝 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 後安裝 HA 套件，需要重新啟動 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 才能使用它。 這些指示假設已設定 Microsoft 套件的存放庫，因為此時應該會安裝 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
> [!NOTE]
> - 如果您不使用 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理程式進行記錄傳送或任何其他用途，則不需要安裝代理程式，因此可以略過套件 *mssql-server-agent*。
> - 其他適用於 Linux 上之 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 全文檢索搜尋 (*mssql-server-fts*) 和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*) 的選用套件都不是針對 FCI 或 AG 取得高可用性的必要項。

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

在本教學課程中，您已了解如何為 Linux 上的 SQL Server 部署 Pacemaker 叢集。 您已了解如何︰
> [!div class="checklist"]
> * 安裝高可用性附加元件並安裝 Pacemaker。
> * 準備 Pacemaker 的節點 (僅限 RHEL 和 Ubuntu)。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server HA 和 SQL Server Agent 套件。

若要為 Linux 上的 SQL Server 建立和設定可用性群組，請參閱：

> [!div class="nextstepaction"]
> [為 Linux 上的 SQL Server 建立和設定可用性群組](sql-server-linux-create-availability-group.md)。

