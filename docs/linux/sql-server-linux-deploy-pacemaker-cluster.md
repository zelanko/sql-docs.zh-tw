---
title: "部署 SQL Server on Linux Pacemaker 叢集 |Microsoft 文件"
description: "本教學課程會示範如何將 Pacemaker 叢集部署的 SQL Server on Linux。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 303629364a954fec1328d571ec3b6f3df57b6527
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Pacemaker 叢集部署的 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程中記載部署 Linux Pacemaker 叢集所需的工作[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Always On 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI)。 不同於緊密繫結的 Windows Server /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]堆疊、 Pacemaker 建立叢集，以及在 Linux 上的可用性群組 (AG) 組態即可之前或之後安裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 正在設定叢集後，即會完成的整合和資源 Pacemaker 部分 AG 或 FCI 的部署組態。
> [!IMPORTANT]
> 叢集類型為 None AG 沒有*不*需要 Pacemaker 叢集中，同時也不可以它受 Pacemaker。 

> [!div class="checklist"]
> * 安裝高可用性的附加元件，並安裝 Pacemaker。
> * 準備 Pacemaker （RHEL 和 Ubuntu 只） 節點。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server 高可用性和 SQL Server Agent 的封裝。
 
## <a name="prerequisite"></a>必要條件
[安裝 SQL Server 2017](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安裝高可用性的附加元件
使用下列語法來安裝封裝的每個散發的 Linux 的高可用性 (HA) 附加元件所組成。 

**Red Hat Enterprise Linux (RHEL)**
1.  註冊伺服器，請使用下列語法。 系統提示您輸入有效的使用者名稱和密碼。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出可用的集區註冊。
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    其中*PoolId*是從上一個步驟的高可用性訂用帳戶的集區識別碼。
    
4.  啟用要能夠使用高可用性的附加元件的儲存機制。
    
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

YaST 中安裝高可用性模式，或做為伺服器的主要安裝的一部分。 做為來源或線上取得它，可以完成安裝與 ISO/DVD。
> [!NOTE]
> SLES，在建立叢集時，取得初始化的 HA 附加元件。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>準備節點 Pacemaker （RHEL 和 Ubuntu 只）
Pacemaker 本身會使用名為通訊群組上建立使用者*hacluster*。 RHEL 和 Ubuntu 上安裝高可用性的附加元件時，取得建立使用者。
1. 每個伺服器上將做為 Pacemaker 叢集的節點，建立可供叢集使用者的密碼。 在範例中使用的名稱是*hacluster*，但是可以使用任何名稱。 名稱和密碼必須參與 Pacemaker 叢集中的所有節點上相同。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 在將成為 Pacemaker 叢集一部分的每個節點，啟用和啟動`pcsd`服務使用下列命令 （RHEL 和 Ubuntu）：

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   然後執行
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   若要確保`pcsd`已啟動。
3. 啟用 Pacemaker 服務 Pacemaker 叢集的每個可能的節點上。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   在 Ubuntu，您會看到錯誤：
   
   *pacemaker 預設開始包含沒有 runlevels，正在中止。*
   
   這個錯誤是已知的問題。 儘管有錯誤，啟用 Pacemaker 服務成功，而這個 bug 會固定在某個時間點在未來。
   
4. 接下來，建立並啟動 Pacemaker 叢集。 沒有其中一個差異 RHEL 和 Ubuntu 在此步驟。 在這兩個發行版本中，安裝`pcs`的 Pacemaker 叢集 RHEL、 執行這個命令會終結現有的組態設定的預設組態檔，以及建立新的叢集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>建立 Pacemaker 叢集 
本節說明如何建立及設定的每個散發的 Linux 叢集。

**RHEL**

1. 授權節點
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   其中*NodeX*是節點的名稱。
2. 建立叢集
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   其中*PMClusterName*是指派給 Pacemaker 叢集的名稱和*Nodelist*是以空格分隔的節點名稱的清單。

**Ubuntu**

設定 Ubuntu 是 RHEL 類似。 不過，沒有一項主要差異： 安裝 Pacemaker 封裝會建立叢集，以及啟用和啟動基底組態`pcsd`。 如果您嘗試設定完全遵循 RHEL 指示 Pacemaker 叢集，您會收到錯誤。 若要修正此問題，請執行下列步驟： 
1. 從每個節點中移除預設 Pacemaker 組態。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 請遵循建立 Pacemaker 叢集 RHEL 」 一節中的步驟。

**SLES**

建立 Pacemaker 叢集的程序是完全不同上 SLES RHEL 和 Ubuntu 上。 下列步驟文件如何 SLES 以建立叢集。
1. 執行啟動的叢集設定程序 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   其中一個節點。 未設定 NTP 和位於沒有監視裝置，您可能會提示您。 這是正常的事情快速安裝和執行。 監視與 STONITH，如果您使用儲存體架構 SLES 的內建範圍。 可以稍後再設定 NTP 和監視。
   
2. 系統會提示您設定 Corosync。 系統會詢問要繫結，以及多點傳送的位址和連接埠的網路位址。 網路位址不使用; 的子網路例如，192.191.190.0。 您可以接受預設值在每個提示字元中，或視需要變更。
   
3. 接下來，您會要求您是否要設定架 SBD，也就是以磁碟為基礎的隔離。 此組態可以稍後完成，如有需要。 如果不是架 SBD 設定不同於 RHEL 和 Ubuntu，`stonith-enabled`會依預設會設定為 false。
   
4. 最後，您必須要設定的 IP 位址管理。 此 IP 位址為選擇性，但是函式類似於 Windows Server 容錯移轉叢集 (WSFC)，這表示要用於連接到它透過 HA Web Konsole （鷹） 叢集中建立 IP 位址的 IP 位址。 此設定，也是選擇性的。
   
5. 確保叢集已啟動並執行發行 
   ```bash
   sudo crm status
   ```
   
6. 變更*hacluster*密碼 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果您設定管理的 IP 位址，可以測試在瀏覽器中也會測試的密碼變更*hacluster*。
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 在另一個 SLES 伺服器將會在叢集的節點上執行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出現提示時，輸入名稱或 IP 位址，已設定為在先前步驟中叢集的第一個節點的伺服器。 伺服器會以節點加入至現有的叢集。
   
10. 確認節點已新增藉由發出 
   ```bash
   sudo crm status
   ```
   
11. 變更*hacluster*密碼 
   ```bash
   sudo passwd hacluster
   ```
   
12. 重複步驟 8-11 為所有其他伺服器新增至叢集。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安裝 SQL Server 高可用性和 SQL Server Agent 的封裝
使用下列命令來安裝 SQL Server 高可用性套件和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理程式，如果不已安裝。 在安裝之後安裝 HA 封裝[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需要重新啟動[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，才能使用。 這些指示假設，Microsoft 封裝的儲存機制已設定好，因為[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該在此時安裝。
> [!NOTE]
> - 如果您不會使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]記錄傳送或任何其他用途的代理程式，它並沒有安裝，因此封裝*mssql server agent*可以略過。
> - 其他選擇性套件[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文檢索搜尋 (*mssql-伺服器-fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql 伺服器是*)，不是高可用性、 FCI 或 AG 的必要項。

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

## <a name="next-steps"></a>後續的步驟

在本教學課程中，您學會如何 Pacemaker 叢集部署的 SQL Server on Linux。 您已了解如何以：
> [!div class="checklist"]
> * 安裝高可用性的附加元件，並安裝 Pacemaker。
> * 準備 Pacemaker （RHEL 和 Ubuntu 只） 節點。
> * 建立 Pacemaker 叢集。
> * 安裝 SQL Server 高可用性和 SQL Server Agent 的封裝。

若要建立及設定可用性群組的 SQL Server on Linux，請參閱：

> [!div class="nextstepaction"]
> [建立及設定可用性群組的 SQL Server on Linux](sql-server-linux-create-availability-group.md)。

