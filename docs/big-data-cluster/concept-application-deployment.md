---
title: 什麼是應用程式部署？
titleSuffix: SQL Server 2019 big data clusters
description: 本文說明在 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式部署。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7e103acdcfd11b3693e6b1ba343258ee00c16572
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729191"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>什麼是 SQL Server 2019 巨量資料叢集上的應用程式部署？

應用程式部署會提供介面來建立、 管理及執行應用程式，以讓巨量資料叢集上的應用程式的部署。 巨量資料叢集上部署的應用程式會受益於叢集的運算能力，而且可以存取在叢集使用的資料。 這會增加延展性和效能的應用程式，同時管理資料的所在位置的應用程式。
下列各節描述的架構和應用程式部署功能。

## <a name="application-deployment-architecture"></a>應用程式部署架構

應用程式部署是由一個控制站和應用程式執行階段處理常式所組成。 建立應用程式，規格檔案時 (`spec.yaml`) 提供。 這`spec.yaml`檔案包含控制器必須知道若要成功部署應用程式的所有項目。 以下是針對內容的範例`spec.yaml`:

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

控制器會檢查`runtime`中所指定`spec.yaml`檔案，並呼叫對應的執行階段處理常式。 執行階段處理常式會建立應用程式。 首先，會建立 Kubernetes ReplicaSet，包含一或多個 pod，每個均包含應用程式部署。 所定義的 pod 數目`replicas`參數中設定`spec.yaml`應用程式檔案。 每個 pod 可以有多個集區的其中一個。 所定義的集區數目`poolsize`參數中設定`spec.yaml`檔案。

這些設定會影響部署可以平行處理的要求量。 一個給定時間的要求數目上限是等於`replicas`時間`poolsize`。 如果您有 5 個複本和 2 個集區，每個複本部署可以處理以平行方式的 10 名要求。 請參閱下圖的圖形化表示法`replicas`和`poolsize`:

![Poolsize 和複本](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

如果已建立的 ReplicaSet，和 pod 已開始之後，建立 cron 作業`schedule`中設定的`spec.yaml`檔案。 最後，Kubernetes 服務會建立可用來管理和執行應用程式 （如下所示）。

應用程式執行時，應用程式 proxy 的要求的複本，然後傳回結果的 Kubernetes 服務。

## <a name="how-to-work-with-application-deployment"></a>如何使用應用程式部署

應用程式部署的兩個主要的介面包括： 
- [命令列介面 `mssqlctl`](big-data-cluster-create-apps.md)
- [Visual Studio Code 和 Azure Data Studio 擴充功能](app-deployment-extension.md)

您也可讓應用程式以使用 RESTful web 服務來執行。 如需詳細資訊，請參閱 <<c0> [ 巨量資料叢集上的應用程式會耗用](big-data-cluster-consume-apps.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解如何建立和 SQL Server 的巨量資料叢集上執行應用程式，請參閱下列各項：

- [使用 mssqlctl 部署應用程式](big-data-cluster-create-apps.md)
- [使用應用程式部署的延伸模組部署應用程式](app-deployment-extension.md)
- [使用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)

若要深入了解 SQL Server 巨量資料叢集，請參閱下列概觀：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
