---
title: SQL Server 巨量資料叢集版本資訊
titleSuffix: SQL Server big data clusters
description: 本文描述 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (預覽) 的最新更新和已知問題。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e868d5db99c3f0be141d28a881d8d8bc6f9c241e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531633"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>SQL Server 巨量資料叢集版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

使用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 從您所有資料取得近乎即時的見解，可提供完整的環境來處理大型資料集，包括機器學習和 AI 功能。

本文列出最新版 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC) 的更新和已知問題。

## <a id="rtm"></a> SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 引進 SQL Server 巨量資料叢集。

使用 SQL Server 巨量資料叢集可執行下列動作：

- 為 Kubernetes 上執行的 SQL Server、Spark 和 HDFS 容器[部署可擴充叢集](../big-data-cluster/deploy-get-started.md)。 
- 讀取、寫入及處理來自 Transact-SQL 或 Spark 的巨量資料。
- 輕鬆結合及分析含有大量巨量資料的高價值關聯式資料。
- 查詢外部資料來源。
- 在 SQL Server 的受控 HDFS 中儲存巨量資料。
- 透過叢集查詢來自多個外部資料來源的資料。
- 使用 AI、機器學習和其他分析工作的資料。
- 在 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 中[部署及執行應用程式](../big-data-cluster/concept-application-deployment.md)。
- 使用 [PolyBase](../relational-databases/polybase/polybase-guide.md) 將資料虛擬化。 使用外部資料表來查詢來自外部 SQL Server、Oracle、Teradata、MongoDB 及 ODBC 資料來源的資料。
- 使用 Always On 可用性群組技術，為 SQL Server 主要執行個體和所有資料庫提供高可用性。

## <a name="sql-server-version"></a>SQL Server 版本

目前的 SQL Server 版本為 `15.0.2070.34`。

## <a name="image-tags"></a>映像標籤

此版本的映像標籤是 `2019-GDR1-ubuntu-16.04`。

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>可支援性

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

### <a name="tools"></a>工具

|平台|支援的版本|
|---------|---------|
|`azdata`|必須與伺服器具有相同的次要版本 (與 SQL Server 主要執行個體相同)。<br/>執行 `azdata –-version` 以驗證版本。 目前，版本為 `15.0.2070`。|
|Azure Data Studio|取得 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新組建。|

### <a name="sql-server-editions"></a>SQL Server 版本

|版本|注意|
|---------|---------|
|Enterprise<br/>標準<br/>開發人員| 巨量資料叢集版本是由 SQL Server 主要執行個體版本所決定。 在部署時，預設會部署 Developer Edition。 在部署後可以變更此版本。 請參閱[設定 SQL Server 主要執行個體](../big-data-cluster/configure-sql-server-master-instance.md)。 |

## <a name="known-issues"></a>已知問題

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>從 Azure Data Studio (ADS) 或 curl 提交 Livy 作業失敗，並出現 500 錯誤

**問題和對客戶的影響**︰在 HA 設定中，會使用多個複本來設定 Spark 共用資源 (sparkhead)。 在此情況下，您可能會遇到從 Azure Data Studio (ADS) 或 `curl` 提交 Livy 作業失敗。 若要確認，則對任何 sparkhead Pod 執行 `curl` 都會導致拒絕連線。 例如，`curl https://sparkhead-0:8998/` 或 `curl https://sparkhead-1:8998` 會傳回 500 錯誤。

在下列案例中會發生這個情況：

- 每個 Zookeeper 執行個體的 Zookeeper Pod 或處理序會重新啟動幾次。
- 當 Sparkhead Pod 與 Zookeeper Pod 之間的網路連線不可靠時。

**因應措施**：重新啟動這兩部 Livy 伺服器。

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

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
