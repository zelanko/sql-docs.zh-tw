---
title: 非根巨量資料叢集容器
titleSuffix: SQL Server big data clusters
description: 本文描述如何在 SQL Server 巨量資料叢集中部署非根容器
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e74e08146ea4c92f23ba17816738122147150e7b
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257118"
---
# <a name="non-root-big-data-clusters-containers"></a>非根巨量資料叢集容器

SQL Server 2019 CU5 引入對非根容器的支援。 確定在所有支援的平台上，所有容器應用程式都在預設以非根使用者身分啟動的 BDC 內執行，如此平台實作會更安全。 所有使用 SQL Server 2019 CU5 對應映像標籤的新部署，都能使用這些功能。 這項變更不會影響現有的 CU5 BDC 預先部署，且這些叢集中的應用程式還會繼續以根使用者身分執行。 

## <a name="technical-background"></a>技術背景

請參閱[本技術白皮書](https://aka.ms/sql-bdc-openshift-security)，其使用非根使用者擷取可容納部署的安全性設計細節，並著重在特定情況下，巨量資料叢集能暫時提高哪些權限及其原因。 白皮書的內容是由 SQL Server 和 Red Hat 的安全性專家共同開發，並著重於 OpenShift 中的安全性內容和功能，但 BDC 的安全性概念和設計適用於全部所支援平台。

> [!NOTE]
> 在 CU5 版本中，使用[應用程式部署](concept-application-deployment.md)介面部署的應用程式安裝步驟，執行身分仍然必須是「根」使用者。 這是必要的，因為在安裝期間，會安裝應用程式將使用的其他套件。 部署為應用程式一部分的其他使用者程式碼，將會以低權限使用者的身分執行。 

> [!NOTE]
> 我們建議使用預設的非根設定來執行叢集。 如果想要還原回 CU5 預先行為，且以 `root` 使用者身分執行 BDC 內的容器，則可使用新的功能參數 `allowRunAsRoot`，並關閉預設行為。 這只能在部署階段設定。 若要設定此項目，請在 `control.json` 部署組態檔的 `security` 區段下指定設定：

```json
 "security": {
  …
    "allowRunAsRoot": true,
  …
}
```

> [!IMPORTANT]
> 不支援在 OpenShift 環境中變更此設定。

以非根使用者身分執行 BDC 內的服務，會導致透過閘道端點連線到服務所用認證不使用 `root` 使用者名稱。 如果連線到閘道端點所用應用程式正在使用錯誤的認證，您就會看到驗證錯誤。 閘道端點其新使用者名稱是以通過 `AZDATA_USERNAME` 環境變數的值為基礎。 這和控制器及 SQL Server 端點所用的使用者名稱相同。 這只會影響新的部署，使用任何舊版部署的現有巨量資料叢集會繼續使用 `root`。 當叢集部署為使用 Active Directory 驗證時，不會對認證造成任何影響。 

## <a name="use-the-latest-azure-data-studio"></a>使用最新版 Azure Data Studio

Azure Data Studio 會以透明的方式控制透過閘道變更的連線認證，以在 [物件總管] 中啟用 HDFS 瀏覽體驗，或透過筆記本提交 Spark 作業。 安裝[最新版的 Azure Data Studio 測試人員組建](../azure-data-studio/download-azure-data-studio.md#download-insiders-build-of-azure-data-studio)。 此組建包含此使用案例的必要變更。

至於必須提供認證以透過閘道存取服務的其他案例 (例如，使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 登入、存取 Spark 的 Web 儀表板)，請務必使用正確的認證。 如果您的目標是在 CU5 之前部署的現有叢集，即使叢集升級至 CU5 之後，仍會繼續使用 `root` 使用者名稱來連線到閘道。 如果使用 CU5 組建部署新的叢集，則要提供對應至 `AZDATA_USERNAME` 環境變數的使用者名稱來登入。

## <a name="configuration-file-switches"></a>組態檔參數

從 CU5 開始，新增了兩個新功能參數，以控制 Pod 和節點計量集合。 如果使用不同的解決方案監視 Kubernetes 基礎結構，您可在 `control.json` 部署組態檔中，將 `allowNodeMetricsCollection` 和 `allowPodMetricsCollection`* 設定為 `false`，以關閉 Pod 和主機節點的內建計量集合。 

例如： 

```json
"security": {
  ...
  "allowPodMetricsCollection": true,
  "allowNodeMetricsCollection": true,
  ...
}
```

> [!NOTE]
> 根據預設，針對 OpenShift 環境，這些設定會在內建的部署設定檔中設定為 false。 收集 Pod 和節點計量所需特殊權限功能及建議的 OpenShift 安全性內容，是以「限制的」條件約束為基礎。

從 CU5 開始，根據預設，特殊權限的容器除外，所有新 BDC 部署在所有支援平台上的容器，都會以非根使用者的身分執行。 所有使用 SQL Server 2019 CU5 對應映像標籤的新部署，都能使用這些功能。 現有的 CU5 BDC 預先部署不受影響，且這些叢集中的應用程式還會繼續以根使用者的身分執行。

## <a name="next-steps"></a>後續步驟
[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)

[在 OpenShift 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-openshift.md)

[安全性白皮書](https://aka.ms/sql-bdc-openshift-security)
