---
title: 控制器是什麼？
titleSuffix: SQL Server big data clusters
description: 本文說明 SQL Server 2019 big data cluster (預覽) 的控制器。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419542"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>SQL Server big data 叢集上的控制器是什麼？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

控制器會裝載用於部署和管理大型資料叢集的核心邏輯。 它會負責與 Kubernetes、屬於叢集一部分的 SQL Server 實例, 以及其他元件 (例如 HDFS 和 Spark) 的互動。

控制器服務提供下列核心功能:

- 管理叢集生命週期: 叢集啟動程式 & 刪除、更新設定
- 管理主要 SQL Server 實例
- 管理計算、資料和存放集區
- 公開監視工具以觀察叢集的狀態
- 公開疑難排解工具, 以偵測並修復非預期的問題
- 管理叢集安全性:
  - 確保安全的叢集端點
  - 管理使用者和角色
  - 設定叢集內通訊的認證

## <a name="deploying-the-controller-service"></a>部署控制器服務

控制器會部署並裝載在客戶想要建立 big data 叢集的相同 Kubernetes 命名空間中。 這項服務是由 Kubernetes 系統管理員在叢集啟動程式期間, 使用**azdata**命令列公用程式來安裝。 如需詳細資訊, 請參閱[開始使用 SQL Server big data](deploy-get-started.md)叢集。

增建工作流程會在 Kubernetes 功能齊全的 SQL Server big data 叢集之上進行版面配置, 其中包含[總覽](big-data-cluster-overview.md)文章中所述的所有元件。 啟動程式工作流程會先建立控制器服務, 一旦部署之後, 控制器服務就會協調主要、計算、資料和存放集區中其餘服務部分的安裝和設定。

## <a name="managing-the-cluster-through-the-controller-service"></a>透過控制器服務管理叢集

您可以使用任一個**azdata**命令, 透過控制器服務來管理叢集。 如果您將其他 Kubernetes 物件 (例如 pod) 部署到相同的命名空間中, 控制器服務就不會管理或監視它們。 您也可以使用**kubectl**命令來管理 Kubernetes 層級的叢集。 如需詳細資訊, 請參閱[監視和疑難排解 SQL Server big data](cluster-troubleshooting-commands.md)叢集。

針對 big data 叢集所建立的控制器和 Kubernetes 物件 (具狀態集、pod、秘密等) 都位於專用的 Kubernetes 命名空間中。 Kubernetes 叢集系統管理員將授與控制站服務的許可權, 以管理該命名空間內的所有資源。  此案例的 RBAC 原則會在使用**azdata**進行初始叢集部署的過程中自動設定。

### <a name="azdata"></a>azdata

**azdata**是以 Python 撰寫的命令列公用程式, 可讓叢集系統管理員透過控制器服務所公開的 REST api 來啟動和管理大型資料叢集。

## <a name="controller-service-security"></a>控制器服務安全性

所有與控制器服務的通訊都是透過 HTTPS 透過 REST API 進行。 系統會在啟動程式時自動為您產生自我簽署憑證。 

控制器服務端點的驗證是以使用者名稱和密碼為基礎。 這些認證會在叢集啟動時布建, 並使用環境變數`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`的輸入。

> [!NOTE]
> 您必須提供符合[SQL Server 密碼複雜性需求](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)的密碼。

## <a name="next-steps"></a>後續步驟

若要深入瞭解 SQL Server big data 叢集, 請參閱下列資源:

- [什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)
- [發現Microsoft SQL Server big data 叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
