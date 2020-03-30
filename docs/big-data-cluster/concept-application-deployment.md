---
title: 什麼是應用程式部署？
titleSuffix: SQL Server Big Data Clusters
description: 本文說明 SQL Server 2019 巨量資料叢集上的應用程式部署。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4b647ab4d03d110ce303388a8b62461f28033b6c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831573"
---
# <a name="what-is-application-deployment-on-a-big-data-cluster"></a>什麼巨量資料叢集上的應用程式部署？

應用程式部署藉由提供介面來建立、管理和執行應用程式，讓您能在巨量資料叢集上部署應用程式。 部署在巨量資料叢集上的應用程式可受益於叢集的計算能力，且可以存取叢集上可用的資料。 這會增加應用程式的延展性和效能，同時管理資料所在的應用程式。 SQL Server Big Data 叢集上支援的應用程式執行階段為 R、Python、SSIS、MLeap。

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

控制器會檢查 `runtime` 檔案中指定的 `spec.yaml`，並呼叫對應的執行階段處理常式。 執行階段處理常式會建立應用程式。 首先，會建立包含一或多個 Pod 的 Kubernetes 複本集，其中每個 Pod 都包含要部署的應用程式。 Pod 數目是由應用程式 `replicas` 檔案中設定的 `spec.yaml` 參數所定義。 每個 Pod 都可以具有一個以上的集區。 集區數目是由 `poolsize` 檔案中設定的 `spec.yaml` 參數所定義。

這些設定會影響部署可以平行處理的要求數目。 一個特定時間的要求數目上限等於 `replicas` 乘上 `poolsize`。 如果您有 5 個複本，每個複本有 2 個集區，則部署可以平行處理 10 個要求。 下圖為 `replicas` 和 `poolsize` 的圖形表示：

![集區大小和複本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

建立複本集並啟動 Pod 之後，即會建立 cron 作業 (如果已在 `schedule` 檔案中設定 `spec.yaml` )。 最後，會建立可用於管理與執行應用程式的 Kubernetes 服務 (請參閱下方)。

執行應用程式時，應用程式的 Kubernetes 服務會將要求傳送給複本並傳回結果。

## <a name="how-to-work-with-application-deployment"></a>如何使用應用程式部署

應用程式部署的兩個主要介面為： 
- [命令列介面 `azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 延伸模組](app-deployment-extension.md)

您也可以使用 RESTful Web 服務來執行應用程式。 如需詳細資訊，請參閱[取用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上建立並執行應用程式，請參閱下列各項：

- [使用 azdata 部署應用程式](big-data-cluster-create-apps.md)
- [使用應用程式部署延伸模組部署應用程式](app-deployment-extension.md)
- [取用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列概觀：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
