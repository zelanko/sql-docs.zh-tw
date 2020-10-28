---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 巨量資料叢集如何搭配 Kubernetes 使用 RBAC。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 315752ffc775aa1db1970e3fef5c807e0f8e1708
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257129"
---
# <a name="kubernetes-rbac-model--impact-on-users-and-service-accounts-managing-bdc"></a>Kubernetes RBAC 模型與其對管理 BDC 之使用者和服務帳戶的影響

此文章描述管理巨量資料叢集之使用者所需的權限需求，以及有關巨量資料叢集中，預設服務帳戶與 Kubernetes 存取的語法。

> [!NOTE]
> 如需 Kubernetes RBAC 模型的其他資源，請參閱 [Using RBAC Authorization - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) (使用 RBAC 授權 - Kubernetes) 和 [Using RBAC to define and apply permissions - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html) (使用 RBAC 來定義與套用權限 - OpenShift)。

## <a name="role-required-for-deployment"></a>部署所需的角色

BDC 使用服務帳戶 (例如 `sa-mssql-controller` 或 `master`) 來協調叢集 Pod、服務、高可用性、監視等的佈建。當 BDC 部署啟動時 (例如 `azdata bdc create`)，[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 會執行下列動作：

1. 檢查提供的命名空間是否存在。
2. 如果不存在，則其會建立一個，並套用 `MSSQL_CLUSTER` 標籤。
3. 建立 `sa-mssql-controller` 服務帳戶。
4. 建立具有命名空間或專案完整權限 (而不是叢集層級權限) 的 `<namespaced>-admin` 角色。
5. 建立該服務帳戶對角色的角色指派。

完成這些步驟之後，就會佈建控制平面 Pod，且服務帳戶會部署大型資料叢集的其餘部分。  

因此，部署的使用者必須具有權限可執行下列動作：

- 列出叢集中的命名空間 (1)。
- 以標籤修補新的或現有命名空間 (2)。
- 建立服務帳戶 `sa-mssql-controller`、`<namespaced>-admin` 角色和角色繫結 (3-5)。

預設的 `admin` 角色沒有這些權限，因此部署巨量資料叢集的使用者必須至少具有命名空間層級系統管理員權限。

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>收集 Pod 和節點計量所需的叢集角色

從 SQL Server 2019 CU5 開始，Telegraf 需要具有叢集範圍角色權限的服務帳戶才能收集 Pod 和節點計量。 在部署 (或升級現有部署) 期間，我們會嘗試建立必要的服務帳戶和叢集角色，但如果部署叢集或執行升級的使用者沒有足夠的權限，部署或升級仍會繼續進行 (且出現警告) 並成功。 在此情況下，將不會收集 Pod 與節點計量。 部署叢集的使用者必須要求叢集系統管理員建立角色和服務帳戶 (在部署或升級前後)。 在建立角色和服務帳戶之後，BDC 就會使用這些項目。 

以下是說明如何建立所需成品的步驟：

1. 使用下列內容建立 *metrics-role.yaml* 檔案。 請務必將 *<clusterName>* 預留位置取代為巨量資料叢集的名稱。

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: <clusterName>:cr-mssql-metricsdc-reader
   rules:
   - apiGroups:
     - '*'
     resources:
     - pods
     - nodes/stats
     verbs:
     - get
   ---
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     name: <clusterName>:crb-mssql-metricsdc-reader
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: <clusterName>:cr-mssql-metricsdc-reader
   subjects:
   - kind: ServiceAccount
     name: sa-mssql-metricsdc-reader
     namespace: <clusterName>
   ```

2. 建立叢集角色與叢集角色繫結：

   ```bash
   kubectl create -f metrics-role.yaml
   ```

您可在 BDC 部署前後建立服務帳戶、叢集角色和叢集角色繫結。 Kubernetes 會自動更新 Telegraf 服務帳戶的權限。 如果在 Pod 部署過程中建立這些項目，則會在收集 Pod 和節點計量時看到幾分鐘的延遲。

> [!NOTE]
> SQL Server 2019 CU5 引進兩個功能參數，以控制 Pod 和節點計量的收集。 根據預設，這些參數會在所有環境目標中設定為 true，但會在其中覆寫預設值的 OpenShift 除外。 

您可在 `control.json` 部署組態檔的安全性區段中自訂這些設定：

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

如果將這些設定設為 `false`，則 BDC 部署工作流程將不會嘗試建立 Telegraf 的服務帳戶、叢集角色和繫結。

## <a name="default-service-account-usage-from-within-a-bdc-pod"></a>BDC Pod 內的預設服務帳戶使用狀況

如需更緊密的安全性模型，SQL Server 2019 CU5 預設會針對 BDC Pod 內預設 Kubernetes 服務帳戶的認證停用掛接。 這同時適用於 CU5 或更新版本中的新部署與升級的部署。
Pod 內的認證權杖可用來存取 Kubernetes API 伺服器，而權限層級則取決於 Kubernetes 授權原則設定。 如果您有需要還原成先前 CU5 行為的特定使用案例，在 CU6 中，我們將引進新的功能開關，因此您只能在部署時開啟自動掛接。 您可以使用 control.json 設定部署檔案，並將 *automountServiceAccountToken* 設定為 *true* ，以達到這個目的。 執行此命令，以使用 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 更新您 *control.json* 自訂設定檔中的此設定： 

``` bash
azdata bdc config replace -c custom-bdc/control.json -j "$.security.automountServiceAccountToken=true"
```
