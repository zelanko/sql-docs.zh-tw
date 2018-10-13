---
title: SQL Server 2019 巨量資料叢集的版本資訊 |Microsoft Docs
description: 本文說明的最新的更新和已知的問題 （預覽） 的 SQL Server 2019 巨量資料叢集。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 13d5cfa95b9a37ecf26658ee255f93c8099faa8f
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085545"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>SQL Server 2019 巨量資料叢集的版本資訊

這篇文章會提供最新版的 SQL Server 的巨量資料叢集的最新的更新和已知的問題。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="ctp-20-october-2018"></a>CTP 2.0 (第 2018 年 10 月)

下列各節說明的新功能與 SQL Server 2019 CTP 2.0 中的巨量資料叢集的已知的問題。

### <a name="whats-in-the-ctp-20-release"></a>什麼是 CTP 2.0 版中？

- 簡單的部署經驗，使用 mssqlctl 管理工具
- 在 Azure 資料 Studio 中的原生的 notebook 體驗
- 查詢存放區執行個體的 SQL 伺服器透過 HDFS 檔案
- 透過 SQL Server、 Oracle、 MongoDB、 和 HDFS 的主要資料虛擬化
- SQL Server 和 Oracle 在 Azure 資料 Studio 中的資料虛擬化精靈
- 在主機上的 ML 服務
- 您可以使用監視和疑難排解的叢集系統管理入口網站
- 在 Azure 資料 Studio 中提交 Spark 作業 
- 在 叢集系統管理入口網站中的 Spark UI
- 磁碟區掛接到儲存體類別
- 透過從主要的資料集區的查詢
- 在 SSMS 中顯示分散式查詢的計的劃
- Pip 套件 mssqlctl 的管理工具
- 透過控制器服務的內建部署引擎

### <a name="known-issues"></a>已知問題

下列各節提供 SQL Server CTP 2.0 中的巨量資料叢集已知的問題。

#### <a name="deployment"></a>部署

- 如果您使用 Azure Kubernetes Service (AKS)，建議的 Kubernetes 版本是 1.10。 *，不支援調整磁碟大小。 您應該要確定您將會據以調整大小的儲存體在部署階段。 如需有關如何調整儲存體大小的詳細資訊，請參閱 <<c0> [ 資料持續性](concept-data-persistence.md)文章。 針對部署在 Vm 上的 Kubernetes，建議的版本是 1.11。

- 在部署之後在 AKS 上，您可能會看到部署的下列兩個警告事件。 這兩個事件的已知問題，但它們不會防止您成功部署在 AKS 上的巨量資料叢集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果巨量資料叢集部署失敗，不會移除相關聯的命名空間。 這可能會導致失去關聯的命名空間，在叢集上。 因應措施是手動刪除命名空間，才能部署具有相同名稱的叢集。

#### <a name="external-tables"></a>外部資料表

- 可以建立具有不支援的資料行類型為資料表的資料集區外部資料表。 如果您查詢外部資料表時，您收到訊息如下所示：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢儲存體集區外部資料表時，您可能會發生錯誤，如果在相同的時間基礎檔案複製到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和 notebook

- POD IP 位址可能變更 Kubernetes 環境中，Pod 重新啟動時。 在案例中，重新啟動主要 pod，Spark 工作階段可能會失敗並`NoRoteToHostException`。 這因為不使用新的 IP 取得重新整理的 JVM 快取的位址。

- 如果您在 Windows 上有已安裝的 Jupyter 和個別的 Python，可能會失敗 Spark notebook。 若要解決此問題，請升級為最新版本的 Jupyter。

- 在筆記本中，如果您按一下**新增文字**命令時，文字資料格會新增 [預覽] 模式，而不是編輯模式。 您可以按一下 [預覽] 圖示，切換至編輯模式和編輯儲存格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下檔案，以進行預覽，HDFS 中，您可能會看到下列錯誤：

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可預覽檔案大於 30 MB 的 Azure Data Studio。

- 不支援對 hdfs-site.xml 變更的 HDFS 組態變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 屬於環境的且可探索 （例如在線傾印檔案）。 您必須在部署之後，重設 SA_PASSWORD 主要執行個體上。 這不是 bug，但安全性步驟。 如需有關如何變更 SA_PASSWORD 的 Linux 容器的詳細資訊，請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄檔可能包含適用於巨量資料叢集部署的 SA 密碼。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
