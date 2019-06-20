---
title: 連線到 SQL Server Always On 可用性群組上的 Kubernetes 叢集
description: 這篇文章說明如何連接到 Alwayson 可用性群組
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1afe2f33ec49f734e97a24a98d62c17b638e38cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713321"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>連接到 SQL Server Always On 可用性群組在 Kubernetes 上

若要連線到 Kubernetes 叢集上的容器中的 SQL Server 執行個體，建立[負載平衡器服務](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 負載平衡器端點。 它會保留的 IP 位址，並轉送到執行 SQL Server 執行個體的 pod 的 IP 位址的要求。

若要連接到可用性群組複本，建立不同的複本類型的服務。 您可以看到服務中的複本不同類型的範例[sql-server-範例/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)。

* `ag1-primary` 指向主要複本。
* `ag1-secondary` 指向任何次要複本。

如果多個有一個次要複本，Kubernetes 會將您的連線路由到不同的複本，以循環配置資源的方式。

## <a name="create-a-load-balancer-service"></a>建立負載平衡器服務

若要建立的主要和複本的負載平衡器服務，請將複製[ `ag1-services.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)從[sql server 範例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file)並更新您的可用性群組。

下列命令會將組態從`.yaml`到叢集的檔案：

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>取得您的負載平衡器服務的 IP 位址

若要取得您的負載平衡器服務的負載平衡器 IP 位址，執行

```kubectl
kubectl get services
```

找出您想要連接到服務的 IP 位址。

## <a name="connect-to-primary-replica"></a>連接到主要複本

若要連線到 SQL 驗證的主要複本，請使用`sa`帳戶、 值`sapassword`您所建立的密碼與此 IP 位址。

例如：

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>後續步驟

[管理 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-linux-kubernetes-manage.md)

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
