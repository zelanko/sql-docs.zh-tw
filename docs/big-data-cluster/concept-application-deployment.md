---
title: 什麼是應用程式部署？
titleSuffix: SQL Server 2019 big data clusters
description: 本文說明 SQL Server 2019 big data cluster (預覽) 上的應用程式部署。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419413"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>什麼是 SQL Server 2019 big data 叢集上的應用程式部署？

應用程式部署藉由提供介面來建立、管理和執行應用程式, 讓您能夠在 big data 叢集上部署應用程式。 部署在 big data 叢集上的應用程式可受益于叢集的計算能力, 並且可以存取叢集上可用的資料。 這會增加應用程式的擴充性和效能, 同時管理資料所在的應用程式。
下列各節說明應用程式部署的架構和功能。

## <a name="application-deployment-architecture"></a>應用程式部署架構

應用程式部署是由控制器和應用程式執行時間處理常式所組成。 建立應用程式時, 會提供規格檔案`spec.yaml`()。 此`spec.yaml`檔案包含控制器為了成功部署應用程式所需知道的一切。 以下是的內容`spec.yaml`範例:

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

控制器會檢查檔案`runtime` `spec.yaml`中指定的, 並呼叫對應的執行時間處理常式。 執行時間處理常式會建立應用程式。 首先, 會建立包含一或多個 pod 的 Kubernetes ReplicaSet, 其中每個 pod 都包含要部署的應用程式。 Pod 數目是由應用程式檔案`replicas` `spec.yaml`中所設定的參數所定義。 每個 pod 可以有一個以上的集區。 集區的數目是由檔案`poolsize` `spec.yaml`中設定的參數所定義。

這些設定會影響部署可以平行處理的要求數量。 一個給定時間的要求數目上限等於`replicas`次。 `poolsize` 如果您有5個複本和每個複本2個集區, 部署可以平行處理10個要求。 如需`replicas`和的圖形表示, `poolsize`請參閱下圖:

![Poolsize 和複本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

建立 ReplicaSet 並啟動 pod 之後, 如果`schedule`在檔案`spec.yaml`中設定了, 就會建立 cron 作業。 最後, 會建立一個可用於管理和執行應用程式的 Kubernetes 服務 (請參閱下文)。

當執行應用程式時, 應用程式的 Kubernetes 服務會將要求傳送給複本, 並傳回結果。

## <a name="how-to-work-with-application-deployment"></a>如何使用應用程式部署

應用程式部署的兩個主要介面如下: 
- [命令列介面`azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 延伸模組](app-deployment-extension.md)

您也可以使用 RESTful web 服務來執行應用程式。 如需詳細資訊, 請參閱[在大型資料叢集上使用應用程式](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>後續步驟

若要深入瞭解如何在 SQL Server big data 叢集上建立和執行應用程式, 請參閱下列各項:

- [使用 azdata 部署應用程式](big-data-cluster-create-apps.md)
- [使用應用程式部署擴充功能部署應用程式](app-deployment-extension.md)
- [在大型資料叢集上使用應用程式](big-data-cluster-consume-apps.md)

若要深入瞭解 SQL Server big data 叢集, 請參閱下列總覽:

- [什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)
