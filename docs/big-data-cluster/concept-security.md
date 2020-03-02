---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 巨量資料叢集的安全性概念。 此內容包括叢集端點與叢集驗證的說明。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0fc816325d4008d1913f0e07e3032677a0eddb4d
ms.sourcegitcommit: 11691bfa8ec0dd6f14cc9cd3d1f62273f6eee885
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074419"
---
# <a name="security-concepts-for-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文將涵蓋巨量資料叢集中與安全性相關的重要概念

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 能提供一致的授權和驗證。 巨量資料叢集可以與 Active Directory (AD) 整合，方法是透過完全自動化部署針對現有網域設定 AD 整合。 在搭配 AD 整合設定巨量資料叢集之後，您可以利用現有的身分識別與使用者群組在所有端點上進行統一存取。 此外，在您於 SQL Server 中建立外部資料表之後，您可以透過將外部資料表的存取權授與 AD 使用者與群組，進而將資料存取原則集中到單一位置，來控制對資料來源的存取。

在這段 14 分鐘的影片中，您將會看到巨量資料叢集安全性的概觀：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Security/player?WT.mc_id=dataexposed-c9-niner]


## <a name="authentication"></a>驗證

外部叢集端點支援 AD 驗證。 使用您的 AD 身分識別來向巨量資料叢集進行驗證。

### <a name="cluster-endpoints"></a>叢集端點

巨量資料叢集有五個進入點

* 主要執行個體 - 用來透過資料庫工具和如 SSMS 或 Azure Data Studio 之類的應用程式存取叢集中 SQL Server 主要執行個體的 TDS 端點。 使用來自 Azdata 的 HDFS 或 SQL Server 命令時，視作業而定，該工具將會連線到其他端點。

* 用來存取 HDFS 檔案的閘道，Spark (Knox) - 用來存取服務 (例如 webHDFS 與 Spark) 的 HTTPS 端點。

* 叢集管理服務 (控制器) 端點 - 公開 REST API 來管理叢集的巨量資料叢集管理服務。 Azdata 工具需要連線到此端點。

* 管理 Proxy - 用來存取「記錄搜尋」儀表板和「計量」儀表板。

* 應用程式 Proxy - 管理部署於巨量資料叢集內部之應用程式的端點。

![叢集端點](media/concept-security/cluster_endpoints.png)

目前沒有開啟其他連接埠從外部存取叢集的選項。

## <a name="authorization"></a>授權

在整個叢集中，從 Spark 與 SQL Server 一路將查詢發送到 HDFS 時，不同元件之間的整合式安全性將能使原始使用者的身分識別能夠傳遞。 如上所述，有各式各樣的外部叢集端點支援 AD 驗證。

在管理資料存取的叢集中有兩個層級的授權檢查。 巨量資料內容中的授權是在 SQL Server 中完成，方法是在物件上和具有控制清單 (ACL) 的 HDFS 中使用傳統 SQL Server 權限，這會將使用者身分識別與特定權限相關聯。

安全的巨量資料叢集是指在 SQL Server 與 HDFS/Spark 之間，針對驗證和授權案例提供一致且連貫的支援。 驗證是驗證使用者或服務識別的程序，並確保其為所宣稱的身分。 授權是指根據要求使用者的識別，授與或拒絕對特定資源的存取。 此步驟是在透過驗證識別使用者之後執行。

巨量資料內容中的授權通常是透過存取控制清單 (ACL) 執行，這會建立使用者識別與特定權限的關聯。 HDFS 透限制對服務 API、HDFS 檔案與作業執行的存取來支援授權。

## <a name="encryption-and-other-security-mechanisms"></a>加密及其他安全性機制

針對用戶端和外部端點之間，以及叢集內元件之間通訊的加密，是搭配 TLS/SSL 使用憑證來保護。

SQL Server 與 SQL Server 之間的所有通訊 (例如與資料集區通訊的 SQL 主要執行個體) 都是使用 SQL 登入來保護。

> [!IMPORTANT]
>  巨量資料叢集會使用 etcd 來儲存認證。 最佳做法是，您必須確定 Kubernetes 叢集已設定為使用待用的 etcd 加密。 根據預設，不會加密儲存在 etcd 中的祕密。 Kubernetes 文件提供此管理工作的詳細資料： https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/ 和 https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/ 。


## <a name="basic-administrator-login"></a>基本系統管理員登入

您可以選擇在 AD 模式中，或是僅使用基本系統管理員登入來部署叢集。 不過，只使用基本系統管理員登入並非生產環境所支援的安全性模式，只應用於評估產品。

即使您選擇 Active Directory 模式，系統仍然會為叢集系統管理員建立基本登入。 此功能會提供替代存取權，以在 AD 連線中斷時使用。

在部署之後，系統便會將叢集中的系統管理員權限授與此基本登入。 登入的使用者將會成為 SQL Server 主要執行個體中的系統管理員，以及叢集控制器中的系統管理員。
Hadoop 元件不支援混合模式驗證，這表示基本系統管理員登入無法用來向閘道 (Knox) 進行驗證。

這些是您需要在部署期間定義的登入認證。

叢集管理使用者名稱：
 + `AZDATA_USERNAME=<username>`

叢集管理密碼：  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> 請注意，在非 AD 模式中，使用者名稱 "root" 必須搭配上述密碼使用，以針對閘道 (Knox) 進行驗證來存取 HDFS/Spark。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
