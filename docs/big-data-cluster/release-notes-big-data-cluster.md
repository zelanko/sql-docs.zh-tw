---
title: SQL Server 巨量資料叢集版本資訊
titleSuffix: SQL Server big data clusters
description: 本文說明 SQL Server 巨量資料叢集的最新更新和已知問題。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9de368594383ef1f7fe3ae3c062f92873fb15698
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256897"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>SQL Server 2019 巨量資料叢集版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列版本資訊適用於 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。 此文章已針對每個版本細分為數個小節。 每個版本都具有描述 CU 變更的支援文章連結，以及能下載 Linux 套件的連結。 此文章也列出最新版 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 的[已知問題](#known-issues)。

## <a name="supported-platforms"></a>支援的平台

本節說明 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 支援的平台。

### <a name="kubernetes-platforms"></a>Kubernetes 平台

|平台|支援的版本|
|---------|---------|
|Kubernetes|BDC 需要 Kubernetes 最低版本為 1.13。 如需 Kubernetes 版本支援原則，請參閱 [Kubernetes version and version skew support policy](https://kubernetes.io/docs/setup/release/version-skew-policy/) (Kubernetes 版本和版本扭曲支援原則)。|
|Azure Kubernetes Service (AKS)|BDC 需要 AKS 最低版本為 1.13。<br/>如需版本支援原則，請參閱 [AKS 中支援的 Kubernetes 版本](/azure/aks/supported-kubernetes-versions)。|

### <a name="host-os-for-kubernetes"></a>適用於 Kubernetes 的主機 OS

|平台|支援的版本|
|---------|---------|
|Red Hat Enterprise Linux|7.3、7.4、7.5、7.6|
|Ubuntu|16.04|

### <a name="sql-server-editions"></a>SQL Server 版本

|版本|注意|
|---------|---------|
|Enterprise<br/>標準<br/>開發人員| 巨量資料叢集版本是由 SQL Server 主要執行個體版本所決定。 在部署時，預設會部署 Developer Edition。 在部署後可以變更此版本。 請參閱[設定 SQL Server 主要執行個體](../big-data-cluster/configure-sql-server-master-instance.md)。 |

## <a name="tools"></a>工具

|平台|支援的版本|
|---------|---------|
|`azdata`|必須與伺服器具有相同的次要版本 (與 SQL Server 主要執行個體相同)。<br/><br/>執行 `azdata –-version` 以驗證版本。<br/><br/>自 SQL Server 2019 CU2 起，本版為 `15.0.4013`。|
|Azure Data Studio|取得 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新組建。|

## <a name="release-history"></a>版本歷程記錄

下表列出 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的版本歷程記錄。

| 版本               | 版本       | 發行日期 |
|-----------------------|---------------|--------------|
| [CU2](#cu2)           | 15.0.4013.40    | 2020-02-13   |
| [CU1](#cu1)           | 15.0.4003.23   | 2020-01-07   |
| [GDR1](#rtm)            | 15.0.2070.34  | 2019-11-04   |

## <a name="how-to-install-updates"></a>如何安裝更新

若要安裝更新，請參閱[如何升級 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md)。

## <a id="cu2"></a> CU2 (2020 年 2 月)

SQL Server 2019 的累積更新 2 (CU2) 版本。 此版本的 SQL Server 資料庫引擎版本為 15.0.4003.23。

|套件版本 | 映像標籤 |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a id="cu1"></a> CU1 (2020 年 1 月)

SQL Server 2019 的累積更新 1 (CU1) 版。 此版本的 SQL Server 資料庫引擎版本為 15.0.4003.23。

|套件版本 | 映像標籤 |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a id="rtm"></a> GDR1 (2019 年 11 月)

SQL Server 2019 一般發行版本 1 (GDR1) - 引進 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)] 的公開推出。 此版本的 SQL Server 資料庫引擎版本為 15.0.2070.34。

|套件版本 | 映像標籤 |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>已知問題

### <a name="deployment-with-private-repository"></a>使用私人存放庫進行部署

- **問題和對客戶的影響**︰從私人存放庫升級具有特定需求

- **因應措施**：如果您使用私人存放庫來預先提取要部署或升級 BDC 的映像，請確定目前的組建映像與目標組建映像都在私人存放庫中。 這可確保成功的復原 (如果有必要)。 此外，如果您在原始部署之後變更私人存放庫的認證，請在升級之前，先更新 Kubernetes 中對應的祕密。 `azdata` 不支援透過 `AZDATA_PASSWORD` 與 `AZDATA_USERNAME` 環境變數來更新認證。 使用 [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret) 更新祕密。 

不支援使用不同的存放庫來進行目前與目標組建升級。

### <a name="upgrade-may-fail-due-to-timeout"></a>升級可能會因為逾時而失敗

- **問題和對客戶的影響**︰升級可能會因為逾時而失敗。

   下列程式碼顯示失敗看起來的樣子：

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   當您在 Azure Kubernetes Service (AKS) 中升級 BDC 時，很可能會發生此錯誤。

- **因應措施**：增加升級的逾時。 

   若要增加升級的逾時，請編輯升級設定對應。 編輯升級設定對應：

   1. 執行以下命令：

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2.   編輯下列欄位：

       **`controllerUpgradeTimeoutInMinutes`** 指定等待控制器或控制器資料庫完成升級的分鐘數。 預設值為 5。 更新為至少 20。

       **`totalUpgradeTimeoutInMinutes`** ：指定控制器與控制器資料庫完成升級的合併時間量 (控制器 + 控制器資料庫升級)。預設值為 10。 更新為至少 40。

       **`componentUpgradeTimeoutInMinutes`** ：指定升級必須完成之每個後續階段的時間量。  預設值為 30。 更新為 45。

   3.   儲存並結束

   下面的 python 指令碼是設定逾時的另一種方式：

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>從 Azure Data Studio (ADS) 或 curl 提交 Livy 作業失敗，並出現 500 錯誤

- **問題和對客戶的影響**︰在 HA 設定中，會使用多個複本來設定 Spark 共用資源 `sparkhead`。 在此情況下，您可能會遇到從 Azure Data Studio (ADS) 或 `curl` 提交 Livy 作業失敗。 若要確認，則對任何 `sparkhead` Pod 執行 `curl` 都會導致拒絕連線。 例如，`curl https://sparkhead-0:8998/` 或 `curl https://sparkhead-1:8998` 會傳回 500 錯誤。

   在下列案例中會發生這個情況：

   - 每個 Zookeeper 執行個體的 Zookeeper Pod 或處理序都會重新啟動幾次。
   - 當 `sparkhead` Pod 與 Zookeeper Pod 之間的網路連線不可靠時。

- **因應措施**：重新啟動這兩部 Livy 伺服器。

   ```bash
   kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

   ```bash
   kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>當主要執行個體在可用性群組中時，建立記憶體最佳化資料表

- **問題和對客戶的影響**︰您不能使用公開用來連線到可用性群組資料庫 (接聽程式) 的主要端點來建立記憶體最佳化資料表。

- **因應措施**：當 SQL Server 主要執行個體是可用性群組設定時，若要建立記憶體最佳化資料表，請[連線到 SQL Server 執行個體](deployment-high-availability.md#instance-connect)，公開端點，連線到 SQL Server 資料庫，然後在使用新連線所建立的工作階段中建立記憶體最佳化資料表。

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>插入外部資料表的 Active Directory 驗證模式

- **問題和對客戶的影響**︰當 SQL Server 主要執行個體處於 Active Directory 驗證模式時，查詢只會從外部資料表 (其中至少有一個外部資料表位於儲存集區) 進行選取，並插入另一個外部資料表中，而此查詢會傳回：

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **因應措施**：使用下列其中一種方式來修改查詢。 將儲存集區資料表聯結至本機資料表，或先插入本機資料表，然後從本機資料表讀取以插入資料集區。

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>透明資料加密功能無法搭配屬於 SQL Server 主要執行個體中可用性群組一部分的資料庫使用

- **問題和對客戶的影響**︰在 HA 設定中，已啟用加密的資料庫無法在容錯移轉之後使用，因為在每個複本上用來加密的主要金鑰都不同。 

- **因應措施**：此問題目前沒有任何因應措施。 建議您在修正程式準備就緒之前，不要在此設定中啟用加密。

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
