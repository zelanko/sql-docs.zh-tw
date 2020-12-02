---
title: 在 OpenShift 上部署
titleSuffix: SQL Server Big Data Cluster
description: 了解如何在 OpenShift 上升級 SQL Server 巨量資料叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 91c491facec15ea50ee93641ff9482b20e5bbf1a
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "96123983"
---
# <a name="deploy-big-data-clusters-2019-on-openshift-on-premises-and-azure-red-hat-openshift"></a>在 OpenShift 內部部署與 Azure Red Hat OpenShift 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文說明如何在 OpenShift 環境 (內部部署或 Azure Red Hat OpenShift (ARO)) 上部署 SQL Server 巨量資料叢集 (BDC)。

> [!TIP]
> 若要快速啟動使用 ARO 的範例環境，再將 BDC 部署到此平台，則可使用[這裡](quickstart-big-data-cluster-deploy-aro.md)提供的 Python 指令碼。


SQL Server 2019 CU5 引進 OpenShift 的 SQL Server 巨量資料叢集支援。 您可將巨量資料叢集部署至內部部署 OpenShift 或 Azure Red Hat OpenShift (ARO)。 部署所需最低版本為 OpenShift 叢集 4.3 版。 雖然部署工作流程類似其他 Kubernetes 平台 ([kubeadm](deploy-with-kubeadm.md) 和 [AKS](deploy-on-aks.md)) 中的部署，但還是有一些差異。 此差異主要在於以非根使用者身分執行應用程式，以及命名空間 BDC 部署所在的安全性內容。

若要將 OpenShift 叢集部署在內部部署，請參閱 [Red Hat OpenShift 文件](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-installation-and-upgrade)。 如需 ARO 部署資訊，請參閱 [Azure Red Hat OpenShift](/azure/openshift/intro-openshift)。

本文概述 OpenShift 平台特定的部署步驟，並指出存取目標環境及正在用來部署巨量資料叢集的命名空間其可用選項。

## <a name="pre-requisites"></a>必要條件

> [!IMPORTANT]
> 下列必要條件其執行者必須是有足夠權限可建立這些叢集層級物件的 OpenShift 叢集系統管理員 (叢集系統管理員叢集角色)。 如需 OpenShift 中叢集角色的詳細資訊，請參閱 [Using RBAC to define and apply permissions](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html) (使用 RBAC 定義與套用權限)。

1. 請確定 OpenShift 上的 `pidsLimit` 設定已更新，可容納 SQL Server 的工作負載。 OpenShift 中的預設值對工作負載等生產環境而言太低。 一開始至少使用 `4096`，但最佳值取決於 SQL Server 中的 `max worker threads` 設定，以及 OpenShift 主機節點上的 CPU 處理器數目。 
    - 若要了解如何更新 OpenShift 叢集的 `pidsLimit`，請使用[這些指示]( https://github.com/openshift/machine-config-operator/blob/master/docs/ContainerRuntimeConfigDesign.md)。 請注意，`4.3.5` 之前的 OpenShift 版本有瑕疵，會導致更新的值無法生效。 請務必將 OpenShift 升級至最新版本。 
    - 為協助根據環境和規劃的 SQL Server 工作負載計算出最佳值，您可使用以下評估和範例：

    |處理器數目|預設最大背景工作角色執行緒|每個處理器的預設背景工作角色數目|最小 pidsLimit 值|
    |--------------------|--------------------------|-----------------------------|-----------------------|
    |          64        |           512            |             16              | 512 + (64 *16) = 1536 |
    |         128        |           512            |             32              | 512 + (128*32) = 4608 |

    > [!NOTE]
    > 其他程序 (例如備份、CLR、全文檢索、SQLAgent) 也會新增額外負荷，所以請將緩衝區新增至估計值。

1. 下載自訂資訊安全內容限制式 (SCC) [`bdc-scc.yaml`](#bdc-sccyaml-file)：

    ```console
    curl https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml -o bdc-scc.yaml
    ```

1. 將 SCC 套用至叢集。

    ```console
    oc apply -f bdc-scc.yaml
    ```

    > [!NOTE]
    > BDC 的自訂 SCC 是以具有其他權限的 OpenShift 中內建 `nonroot` SCC 為基礎。 若要深入了解 OpenShift 中的安全性內容條件約束，請參閱 [Managing Security Context Constraints](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html) (管理安全性內容條件約束)。 如需 `nonroot` SCC 上層巨量資料叢集所需額外權限的詳細資訊，請下載[這裡](https://aka.ms/sql-bdc-openshift-security)的白皮書。

3. 建立命名空間/專案：

   ```console
   oc new-project <namespaceName>
   ```

4. 針對 BDC 部署所在命名空間中的使用者，將自訂 SCC 指派給其服務帳戶：

   ```console
   oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:<namespaceName>
   ```

5. 將適當權限指派給部署 BDC 的使用者。 執行下列其中一項動作。 

   - 如果部署 BDC 的使用者具有叢集系統管理員角色，請繼續[部署巨量資料叢集](#deploy-big-data-cluster)。

   - 如果部署 BDC 的使用者是命名空間系統管理員，請指派已建立命名空間的使用者叢集系統管理員本機角色。 這是讓部署和管理巨量資料叢集其使用者具有命名空間層級系統管理員權限的慣用選項。

   ```console
   oc adm policy add-role-to-user cluster-admin <deployingUser> -n <namespaceName>
   ```

   接著，部署巨量資料叢集的使用者必須登入 OpenShift 主控台：

   ```console
   oc login -u <deployingUser> -p <password>
   ```

## <a name="deploy-big-data-cluster"></a>部署巨量資料叢集

1. 安裝最新的 [azdata](../azdata/install/deploy-install-azdata.md)。

1. 根據目標環境 (OpenShift 內部部署或 ARO) 和部署案例，複製其中一個 OpenShift 內建組態檔。 請參閱以下＜部署組態檔中的 OpenShift 特定設定＞一節，以了解內建組態檔中 OpenShift 特定設定。 如需可用組態檔的詳細資料，請參閱[部署指引](deployment-guidance.md)。

   列出所有可用的內建組態檔。

   ```console
   azdata bdc config list
   ```

   若要複製其中一個內建組態檔，請執行以下命令 (或者，可根據目標平台/案例更換設定檔)：

   ```console
   azdata bdc config init --source openshift-dev-test --target custom-openshift
   ```

   針對 ARO 上的部署，建議從其中一個 `aro-` 設定檔開始，其包含適合此環境的 `serviceType` 與 `storageClass` 預設值。 例如：

   ```console
   azdata bdc config init --source aro-dev-test --target custom-openshift
   ```

1. 自訂組態檔 control.json 和 bdc.json。 以下是一些額外的資源，其可引導完成支援各種使用案例的自訂內容：

   - [Storage](concept-data-persistence.md)
   - [AD 相關設定](active-directory-deploy.md)
   - [其他自訂內容](deployment-custom-configuration.md)

   > [!NOTE]
   > 不支援整合適用於 BDC 的 Azure Active Directory，因此在 ARO 上部署時，無法使用此驗證方法。

1. 設定[環境變數](deployment-guidance.md#env)

1. 部署巨量資料叢集

   ```console
   azdata bdc create --config custom-openshift --accept-eula yes
   ```

1. 部署成功後，即可登入並列出外部叢集端點：

   ```console
      azdata login -n mssql-cluster
      azdata bdc endpoint list
   ```

## <a name="openshift-specific-settings-in-the-deployment-configuration-files"></a>部署組態檔中的 OpenShift 特定設定

SQL Server 2019 CU5 引進兩個功能參數，以控制 Pod 與節點計量的集合。 在 OpenShift 的內建設定檔中，這些參數預設為 `false`，因為監視容器需要[特殊權限的安全性內容](https://www.openshift.com/blog/managing-sccs-in-openshift)，這會放寬 BDC 部署所在命名空間的部分安全性條件約束。

```json
    "security": {
      "allowNodeMetricsCollection": false,
      "allowPodMetricsCollection": false
}
```

ARO 的預設儲存類別名稱是 managed-premium (相對於 AKS 的預設儲存類別名稱 default)。 您會在 `control.json` 中找到對應 `aro-dev-test` 和 `aro-dev-test-ha` 的此項目：

```json
    },
    "storage": {
      "data": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
      }
```

## <a name="bdc-sccyaml-file"></a>`bdc-scc.yaml` 檔案

此部署的 SCC 檔案為：

:::code language="yaml" source="../../sql-server-samples/samples/features/sql-big-data-cluster/deployment/openshift/bdc-scc.yaml":::

## <a name="next-steps"></a>後續步驟

[教學課程：將範例資料載入 SQL Server 巨量資料叢集](tutorial-load-sample-data.md)
