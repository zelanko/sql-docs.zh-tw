---
title: 控制器是什麼？
titleSuffix: SQL Server big data clusters
description: 本文描述 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的控制器。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 96a652a562ea5b38df593dc9642a46cd32c41f8b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73532405"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 巨量資料叢集上的控制器？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

控制器會裝載用於部署和管理大型資料叢集的核心邏輯。 其負責與 Kubernetes、SQL Server 執行個體 (為叢集的一部分) 和其他元件 (例如 HDFS 和 Spark) 的互動。

控制器服務提供下列核心功能：

- 管理叢集生命週期：叢集啟動程序與刪除、更新設定
- 管理主要 SQL Server 執行個體
- 管理計算、資料和存放集區
- 公開監視工具以觀察叢集的狀態
- 公開疑難排解工具以偵測並修復非預期的問題
- 管理叢集安全性：
  - 確保叢集端點安全
  - 管理使用者和角色
  - 設定叢集內通訊的認證

## <a name="deploying-the-controller-service"></a>部署控制器服務

控制器會部署並裝載在客戶想要建立巨量資料叢集的相同 Kubernetes 命名空間中。 這項服務是由 Kubernetes 系統管理員在叢集啟動程序期間使用 **azdata** 命令列公用程式來安裝。 如需詳細資訊，請參閱[開始使用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-get-started.md)。

增建工作流程會在 Kubernetes 功能齊全的 SQL Server 巨量資料叢集之上進行配置，其中包含[概觀](big-data-cluster-overview.md)一文中所述的所有元件。 啟動程序工作流程會先建立控制器服務，在完成部署之後，控制器服務會協調主要、計算、資料和存放集區中其餘服務部分的安裝與設定。

## <a name="managing-the-cluster-through-the-controller-service"></a>透過控制器服務管理叢集

您可以使用任一 **azdata** 命令來透過控制器服務管理叢集。 如果您將其他 Kubernetes 物件 (例如 Pod) 部署至相同的命名空間，控制器服務就不會管理或監視它們。 您也可以使用 **kubectl** 命令來管理 Kubernetes 層級的叢集。 如需詳細資訊，請參閱[監視和針對 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md)進行疑難排解。

針對巨量資料叢集建立的控制器和 Kubernetes 物件 (具狀態集合、Pod、祕密等) 都位於專用的 Kubernetes 命名空間。 控制器服務將由 Kubernetes 叢集管理員授與，以管理該命名空間內的所有資源。  此案例的 RBAC 原則會在使用 **azdata** 進行初始叢集部署的過程中自動設定。

### <a name="azdata"></a>azdata

**azdata** 是以 Python 撰寫的命令列公用程式，可讓叢集系統管理員透過由控制器服務公開的 REST API 來啟動並管理大型資料叢集。

## <a name="controller-service-security"></a>控制器服務安全性

所有與控制器服務的通訊都是透過 HTTPS 上的 REST API 進行。 系統會在啟動程序時自動為您產生自我簽署憑證。 

控制器服務端點的驗證是使用 Active Directory 身分識別或是以使用者名稱和密碼為基礎。 這些認證會在叢集啟動時佈建，並使用環境變數 `AZDATA_USERNAME` 和 `AZDATA_PASSWORD` 的輸入。

> [!NOTE]
> 您必須提供符合 [SQL Server 密碼複雜性需求](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)的密碼。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
