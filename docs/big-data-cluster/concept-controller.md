---
title: 什麼是控制器？
titleSuffix: SQL Server big data clusters
description: 本文說明 SQL Server 2019 巨量資料叢集 （預覽） 中的控制站。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 3677a2a68799ab1cfa7b6101893fe2b799b5b04a
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860069"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>什麼是 SQL Server 的巨量資料叢集上的控制站？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

控制站會裝載部署及管理巨量資料叢集的核心邏輯。 它會負責與 Kubernetes 叢集與 HDFS 和 Spark 等其他元件的一部分的 SQL Server 執行個體的所有互動。 

控制器服務提供核心功能如下：

- 管理叢集生命週期： 叢集啟動程序與刪除、 更新組態
- 管理主要的 SQL Server 執行個體
- 管理計算、 資料和儲存體集區
- 若要觀察的叢集狀態的監視工具公開 （expose)
- 公開 （expose) 來偵測並修復未預期的問題的疑難排解工具
- 管理叢集安全性： 確保安全的叢集端點、 管理使用者和角色、 設定叢集間通訊的認證
- 管理升級的工作流程，以便安全地實作 （不適用於 CTP 2.4）
- （不適用於 CTP 2.4） 叢集中具狀態服務的管理高可用性和 DR

## <a name="deploying-the-controller-service"></a>部署控制器服務

控制器會部署並裝載於相同的客戶，想要建置巨量資料叢集的 Kubernetes 命名空間。 此服務管理員安裝的 Kubernetes 叢集啟動程序，使用 mssqlctl 命令列公用程式期間：

```bash
mssqlctl cluster create --name <name of your cluster>
```

增建工作流程會在 Kubernetes 上的版面配置功能完整的 SQL Server 巨量資料叢集，其中包含所述的所有元件[概觀](big-data-cluster-overview.md)文章。 啟動程序的工作流程首先會建立控制器服務，以及安裝和設定的主機、 計算、 資料和儲存體集區的服務一部分的其餘部分，這部署之後，將協調控制器服務。

## <a name="managing-the-cluster-through-the-controller-service"></a>管理透過控制器服務叢集

您可以管理純粹是透過使用控制器服務在叢集`mssqlctl`Api 或裝載於叢集內的叢集系統管理入口網站。 如果您將其他像是 pod 的 Kubernetes 物件部署到相同的命名空間時，不受管理或監視的控制器服務。

建立適用於巨量資料叢集的 Kubernetes 物件 （可設定狀態的集合，pod、 密碼等） 和的控制站位於專用的 Kubernetes 命名空間。 控制器服務將 Kubernetes 叢集系統管理員可以管理該命名空間內的所有資源授與權限。  在初始叢集部署使用自動設定此案例中的 RBAC 原則`mssqlctl`。 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` 命令列公用程式是以 Python，可讓叢集系統管理員啟動及管理巨量資料叢集透過控制器服務所公開的 REST Api 撰寫。

### <a name="cluster-administration-portal"></a>叢集系統管理入口網站

一旦控制器服務已啟動並執行，叢集系統管理員可以使用[叢集管理網站](cluster-admin-portal.md)若要監視部署進度，偵測及疑難排解在叢集內的服務。

## <a name="controller-service-security"></a>控制器服務的安全性

Controller 服務的所有通訊是透過 REST API 都進行 HTTPS。 自我簽署的憑證將會自動產生為您在啟動程序時之用。 

控制器服務端點的驗證根據使用者名稱和密碼。 這些認證會在叢集啟動程序時使用環境變數的輸入佈建`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`。

> [!NOTE]
> 您必須提供的密碼均遵守[SQL Server 密碼複雜性需求](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列資源：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
- [研討會：Microsoft SQL Server 的巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
