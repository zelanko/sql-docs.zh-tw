---
title: 連線到 SQL Server Always On 可用性群組上的 Kubernetes 叢集
description: 這篇文章說明如何連接到 Alwayson 可用性群組
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d13f89a1297d21c882075821a681886dc95c4c76
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049588"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>連接到 SQL Server Always On 可用性群組在 Kubernetes 上

若要連線到 Kubernetes 叢集上的容器中的 SQL Server 執行個體，建立[負載平衡器服務](http://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)。 負載平衡器會將轉送到執行 SQL Server 執行個體的 pod 的 IP 位址的要求。

若要連接到可用性群組複本，建立不同的複本類型的服務。 您可以看到服務中的複本不同類型的範例[sql server 範例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)。

* `ag1-primary` 指向主要複本。
* `ag1-secondary-sync` 要同步的次要複本的點。
* `ag1-secondary-async` 以非同步的次要複本的點。

有相同類型的多個次要複本時，Kubernetes 會將您的連線路由到不同的複本，以循環配置資源的方式。

## <a name="create-a-load-balancer-service"></a>建立負載平衡器服務

若要建立主要複本的負載平衡器服務，請將複製`ag1-primary.yaml`從[sql server 範例]()並更新您的可用性群組。

下列命令適用於您的叢集.yaml 檔案：

```kubectl
kubectl apply -f ag1-primary.yaml
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