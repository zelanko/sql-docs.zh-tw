---
title: 什麼是應用程式部署？
titleSuffix: SQL Server Big Data Clusters
description: 了解應用程式部署如何提供介面，在 SQL Server 2019 巨量資料叢集上建立、管理及執行應用程式。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ac26973c4d1ff8b2a9e689f3aa372d3888f939d6
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914293"
---
# <a name="what-is-application-deployment-on-a-sql-server-big-data-cluster"></a>SQL Server 巨量資料叢集的應用程式部署是什麼？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

應用程式部署可提供建立、管理和執行應用程式的介面，藉以在 SQL Server 巨量資料叢集上部署應用程式。 部署在 SQL Server 巨量資料叢集上的應用程式除可利用叢集的計算能力，還可存取叢集提供的資料。 這會增加應用程式的延展性和效能，同時管理資料所在的應用程式。 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 支援的應用程式執行階段為 R、Python、SSIS、MLeap。

下列各節描述應用程式部署的架構和功能。

## <a name="application-deployment-architecture"></a>應用程式部署架構

應用程式部署是由控制器和應用程式執行階段處理常式所組成。 建立應用程式時，會提供規格檔案 (`spec.yaml`)。 此 `spec.yaml` 檔案包含控制器為了成功部署應用程式所需知道的所有內容。 下列是 `spec.yaml` 內容的範例：

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

控制器會檢查 `spec.yaml` 檔案中指定的 `runtime`，並呼叫對應的執行階段處理常式。 執行階段處理常式會建立應用程式。 首先，會建立包含一或多個 Pod 的 Kubernetes 複本集，其中每個 Pod 都包含要部署的應用程式。 Pod 數目是由應用程式 `spec.yaml` 檔案中設定的 `replicas` 參數所定義。 每個 Pod 都可以具有一個以上的集區。 集區數目是由 `spec.yaml` 檔案中設定的 `poolsize` 參數所定義。

這些設定會影響部署可以平行處理的要求數目。 一個特定時間的要求數目上限等於 `replicas` 乘上 `poolsize`。 如果您有 5 個複本，每個複本有 2 個集區，則部署可以平行處理 10 個要求。 下圖為 `replicas` 和 `poolsize` 的圖形表示：

![集區大小和複本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

建立複本集並啟動 Pod 之後，即會建立 cron 作業 (如果已在 `spec.yaml` 檔案中設定 `schedule` )。 最後，會建立可用於管理與執行應用程式的 Kubernetes 服務 (請參閱下方)。

執行應用程式時，應用程式的 Kubernetes 服務會將要求傳送給複本並傳回結果。

## <a name="security-considerations-for-applications-deployments-on-openshift"></a><a id="app-deploy-security"></a> OpenShift 上應用程式部署的安全性考量

SQL Server 2019 CU5 可支援 Red Hat OpenShift 上的巨量資料叢集部署，以及 BDC 的已更新安全性模型，因此不再需要特殊權限容器。 針對所有使用 SQL Server 2019 CU5 的新部署，除了沒有特殊權限以外，容器還預設會以非根使用者的身分執行。

在 CU5 版本中，使用[應用程式部署]()介面部署的應用程式安裝步驟，執行身分仍然必須是「根」使用者。 這是必要項目，因為在安裝期間，系統會安裝應用程式將使用的其他套件。 部署為應用程式一部分的其他使用者程式碼，將會以低權限使用者的身分執行。 

此外， **CAP_AUDIT_WRITE** 功能是允許使用 Cron 作業為 SSIS 應用程式排程所需的選擇性功能。 當應用程式的 YAML 規格檔案指定排程時，應用程式會透過 Cron 作業觸發，這需要額外的功能。  或者，可視需要透過 Web 服務呼叫來使用 *azdata app run* 以觸發應用程式，這不需要 CAP_AUDIT_WRITE 功能。 

> [!NOTE]
> [OpenShift 部署一文](deploy-openshift.md)中的自訂 SCC 不包含這項功能，因為巨量資料叢集的預設部署不需要該功能。 若要啟用這項功能，必須先更新自訂 SCC YAML 檔案，以將 CAP_AUDIT_WRITE 包含在 

```yml
...
allowedCapabilities:
- SETUID
- SETGID
- CHOWN
- SYS_PTRACE
- AUDIT_WRITE
...
```

## <a name="how-to-work-with-application-deployment"></a>如何使用應用程式部署

應用程式部署的兩個主要介面為： 
- [命令列介面 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](app-create.md)
- [Visual Studio Code 和 Azure Data Studio 延伸模組](app-deployment-extension.md)

您也可以使用 RESTful Web 服務來執行應用程式。 如需詳細資訊，請參閱[取用巨量資料叢集上的應用程式](app-consume.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上建立並執行應用程式，請參閱下列各項：

- [使用 azdata 部署應用程式](app-create.md)
- [使用應用程式部署延伸模組部署應用程式](app-deployment-extension.md)
- [取用巨量資料叢集上的應用程式](app-consume.md)

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列概觀：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)