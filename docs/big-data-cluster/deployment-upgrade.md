---
title: 升級為新版本
titleSuffix: SQL Server Big Data Clusters
description: 了解如何將 SQL Server 巨量資料叢集升級至新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f8ca3e42221387470ee4fc4cbd6873b526bc8b7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77256861"
---
# <a name="how-to-upgrade-big-data-clusters-2019"></a>如何升級 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

升級路徑相依於 SQL Server 巨量資料叢集 (BDC) 的目前版本。 若要從支援的版本 (包括一般發行版本 (GDR)、累積更新 (CU) 或快速檢修 (QFE) 更新) 升級，您可以就地升級。 不支援從客戶技術預覽 (CTP) 或候選版 BDC 就地升級。 您必須移除並重新建立叢集。 下列小節說明針對每個案例所要執行的步驟：

- [從支援的版本升級](#upgrade-from-supported-release)
- [從 CTP 或候選版更新 BDC 部署](#update-a-bdc-deployment-from-ctp-or-release-candidate)

>[!NOTE]
>第一個支援的巨量資料叢集版本是 SQL Server 2019 GDR1。

## <a name="upgrade-release-notes"></a>升級版本資訊

在繼續之前，請查看[升級版本資訊以了解已知問題](release-notes-big-data-cluster.md#known-issues)。

## <a name="upgrade-from-supported-release"></a>從支援的版本升級

本節會說明如何將 SQL Server BDC 從支援的版本 (從 SQL Server 2019 GDR1 起) 升級至較新的支援版本。

1. 備份 SQL Server 主要執行個體。
2. 備份 HDFS。

   ```
   azdata bdc hdfs cp --from-path <path> --to-path <path>
   ```
   
   例如： 

   ```
   azdata bdc hdfs cp --from-path hdfs://user/hive/warehouse/%%D --to-path ./%%D
   ```

3. 更新 `azdata`。

   遵循安裝 `azdata` 的指示。 
   - [Windows 安裝程式](deploy-install-azdata-installer.md)
   - [Linux 搭配 apt](deploy-install-azdata-linux-package.md)
   - [Linux 搭配 yum](deploy-install-azdata-yum.md)
   - [Linux 搭配 zypper](deploy-install-azdata-zypper.md)

   >[!NOTE]
   >如果 `azdata` 是使用 `pip` 安裝的，您必須先手動加以移除，再使用 Windows 安裝程式或 Linux 套件管理員安裝。

1. 更新巨量資料叢集。

   ```
   azdata bdc upgrade -n <clusterName> -t <imageTag> -r <containerRegistry>/<containerRepository>
   ```

   例如，下列指令碼使用 `2019-CU1-ubuntu-16.04` 映像標籤：

   ```
   azdata bdc upgrade -n bdc -t 2019-CU1-ubuntu-16.04 -r mcr.microsoft.com/mssql/bdc
   ```

>[!NOTE]
>您可以在 [SQL Server 2019 巨量資料叢集版本資訊](release-notes-big-data-cluster.md)取得最新的映像標籤。

>[!IMPORTANT]
>如果您使用私人存放庫來預先提取要部署或升級 BDC 的映像，請確定目前的組建映像與目標組建映像都在私人存放庫中。 這可確保成功的復原 (如果有必要)。 此外，如果在原始部署之後變更了私人存放庫的認證，請更新對應的環境變數 DOCKER_PASSWORD 和 >DOCKER_USERNAME。 不支援使用不同私人存放庫升級目前組建與目標組建。

### <a name="increase-the-timeout-for-the-upgrade"></a>增加升級的逾時

如果未在配置時間內升級特定元件，就可能發生逾時。 下列程式碼顯示失敗看起來的樣子：

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

若要增加升級的逾時，請使用 **--controller-timeout** 和 **--component-timeout** 參數，在您發出升級時指定較高的值。 僅自 SQL Server 2019 CU2 版本開始提供此選項。 例如：

   ```bash
   azdata bdc upgrade -t 2019-CU2-ubuntu-16.04 --controller-timeout=40 --component-timeout=40 --stability-threshold=3
   ```
**--controller-timeout** 指定等待控制器或控制器資料庫完成升級的分鐘數。
**--component-timeout** 指定升級所必須完成每個後續階段的時間長度。

若要在 SQL Server 2019 CU2 以前的版本中增加升級逾時，請編輯升級 config 對應。 編輯升級設定對應：

執行以下命令：

   ```bash
   kubectl edit configmap controller-upgrade-configmap
   ```

編輯下列欄位：

   **controllerUpgradeTimeoutInMinutes** 指定等待控制器或控制器資料庫完成升級的分鐘數。 預設值為 5。 更新為至少 20。
   **totalUpgradeTimeoutInMinutes**：指定控制器與控制器資料庫完成升級的合併時間長度 (控制器 + 控制器資料庫升級)。預設值為 10。 更新為至少 40。
   **componentUpgradeTimeoutInMinutes**：指定升級必須完成之每個後續階段的時間量。 預設值為 30。 更新為 45。

儲存並結束。

## <a name="update-a-bdc-deployment-from-ctp-or-release-candidate"></a>從 CTP 或候選版更新 BDC 部署

不支援從 SQL Server 巨量資料叢集的 CTP 或發行候選組建就地升級。 下一節說明如何手動移除及重新建立叢集。

### <a name="backup-and-delete-the-old-cluster"></a>備份和刪除舊叢集

在 SQL Server 2019 GDR1 版本之前部署的巨量資料叢集沒有就地升級。 升級至新版本的唯一方法是手動移除並重新建立叢集。 每個版本都有與先前版本不相容的唯一 `azdata` 版本。 此外，如果新版容器映像是在以不同舊版部署的叢集上下載的，則最新映像可能會與叢集上的舊版映像不相容。 若在容器設定的部署設定檔中使用 `latest` 映像標籤，系統會提取新版映像。 根據預設，每個版本都有一個對應至 SQL Server 發行版本的特定映像標籤。 若要升級至最新版本，請遵循下列步驟：

1. 在刪除舊叢集之前，請先備份 SQL Server 主要執行個體和 HDFS 上的資料。 針對 SQL Server 主要執行個體，您可以使用 [SQL Server 備份和還原](data-ingestion-restore-database.md)。 針對 HDFS，您[可以使用 `curl` 來複製資料](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令刪除舊叢集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用符合您叢集的 `azdata` 版本。 請勿使用較新版本的 `azdata` 來刪除舊叢集。

   > [!Note]
   > 發出 `azdata bdc delete` 命令會導致刪除巨量資料叢集名稱所識別命名空間中建立的所有物件，但不會刪除命名空間本身。 命名空間只要是空的且其中未建立任何其他應用程式，就可以重複用於後續部署。

1. 將舊版 `azdata` 解除安裝。

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 安裝最新版 `azdata`。 下列命令會從最新版本安裝 `azdata`：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 針對每個版本，`azdata` 的 `n-1` 版本路徑會有所變更。 即使您先前已安裝 `azdata`，您還是必須從最新的路徑重新安裝，才能建立新的叢集。

### <a name="verify-the-azdata-version"></a><a id="azdataversion"></a> 確認 azdata 版本

在您部署新的巨量資料叢集之前，請使用 `--version` 參數，確認您所使用的是最新版 `azdata`：

```bash
azdata --version
```

### <a name="install-the-new-release"></a>安裝新版本

在您移除先前的巨量資料叢集並安裝最新的 `azdata` 之後，請使用目前的部署指示來部署新巨量資料叢集。 如需詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)。 接著，還原任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。
