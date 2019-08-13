---
title: 連線到 Kubernetes 叢集上的 SQL Server Always On 可用性群組
description: 本文說明如何連線到 Always On 可用性群組
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952608"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>連線到 Kubernetes 上的 SQL Server Always On 可用性群組

若要連線到 Kubernetes 叢集上容器中的 SQL Server 執行個體，請建立[負載平衡器服務](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 負載平衡器是一個端點。 它包含一個 IP 位址，並會將 IP 位址的要求轉送到執行 SQL Server 執行個體的 Pod。

若要連線到可用性群組複本，請為不同的複本類型建立服務。 您可以在 [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 中查看不同複本類型的服務範例。

* `ag1-primary` 指向主要複本。
* `ag1-secondary` 指向任何次要複本。

如果有多個次要複本，Kubernetes 會以循環配置資源的方式，將您的連線路由至不同的複本。

## <a name="create-a-load-balancer-service"></a>建立負載平衡器服務

若要建立主要和其他複本的負載平衡器服務，請從 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) 複製 [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)，並針對您的可用性群組加以更新。

下列命令會將 `.yaml` 檔案中的組態套用至叢集：

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>取得負載平衡器服務的 IP 位址

若要取得負載平衡器服務的負載平衡器 IP 位址，請執行

```kubectl
kubectl get services
```

識別您要連線的服務 IP 位址。

## <a name="connect-to-primary-replica"></a>連線到主要複本

若要使用 SQL 驗證連線到主要複本，請使用 `sa` 帳戶、您所建立祕密中的 `sapassword` 值，以及此 IP 位址。

例如：

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>後續步驟

[管理 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-manage.md)

[Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
