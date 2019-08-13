---
title: 管理 Kubernetes 中的 SQL Server Always On 可用性群組
description: 本文說明如何管理 Kubernetes 中的 SQL Server Always On 可用性群組。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952547"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 Kubernetes 中的 SQL Server Always On 可用性群組

若要管理 Kubernetes 上的 Always On 可用性群組，請建立資訊清單並套用至叢集。 此資訊清單是 `.yaml` 檔案。  

本文中的範例適合所有 Kubernetes 叢集。 這些範例中的案例適用於 Azure Kubernetes Service 上的叢集。

如需完整的部署範例，請參閱[在 Kubernetes 叢集上部署 SQL Server Always On 可用性群組](sql-server-linux-kubernetes-deploy.md)。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>容錯移轉 - Kubernetes 上的 SQL Server 可用性群組

若要將主要複本容錯移轉或移至可用性群組中的不同節點，請完成下列步驟：

1. 在資訊清單檔中定義作業。

  [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 存放庫中的 [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) 描述容錯移轉作業。

  將資訊清單檔複製到您的管理終端。

  更新您環境的檔案。

  - 以預期可用性群組目標的 Pod 名稱 (例如 mssql2-0) 取代 `<containerName>`。
  - 如果可用性群組不在 `ag1` 命名空間中，請以其他命名空間取代 `ag1`。

  此檔案會定義名為 `manual-failover` 的容錯移轉作業。

1. 若要部署作業，請使用 `kubectl apply`。 下列指令碼會部署作業。

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  部署作業之後，Kubernetes 與 SQL Server 運算子會執行下列工作：
  
  - 將主要複本降階為次要複本
  
  - 將指定的複本升階為主要複本
  
  套用資訊清單檔之後，Kubernetes 會執行作業。 此作業會讓監督員選取新的領導者，並將主要複本移至領導者的 SQL Server 執行個體。

1. 確認作業已完成。
  
  在 Kubernetes 執行作業之後，您可以檢閱記錄。
  
  下列範例會傳回名為 `manual-failover` 作業的狀態。

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 刪除手動容錯移轉作業。 

  >[!IMPORTANT]
  >您必須手動刪除作業，才能發出另一個手動容錯移轉。
  > 
  >Kubernetes 中的作業物件會在完成後保留，以便檢視狀態。 查看狀態之後，您必須手動刪除舊的作業。 刪除作業也會刪除 Kubernetes 記錄。 如果您沒有刪除作業，除非變更作業名稱和 Pod 選取器，否則未來的容錯移轉作業將會失敗。 如需詳細資訊，請參閱 [Jobs - Run to Completion](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) (作業 - 執行到完成)。

  下列命令會刪除作業。

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>輪替認證

輪替認證以重設 SQL Server `sa` 帳戶的密碼和 SQL Server [服務主要金鑰](../relational-databases/security/encryption/service-master-key.md)。 

為完成此工作，您要在 Kubernetes 叢集中建立新的祕密，然後建立作業來輪替認證。

輪替認證之前，請建立密碼和主要金鑰的新祕密。

下列指令碼會建立名為 `new-sql-secrets` 的祕密。 執行指令碼之前，請以 `sapassword` 和 `masterkeypassword` 的複雜密碼取代 `<>`。 針對每個值使用不同的密碼。

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

對每個需要主要金鑰或 `sa` 密碼的 SQL Server 執行個體完成下列步驟。

1. 將 [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 複製到您的管理終端。

  [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) GitHub 存放庫中的 [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 即為此作業的資訊清單範例。

  套用此資訊清單之前，請更新您環境的資訊清單。 視需要檢查並變更下列設定。

  - 驗證命名空間。 如果需要，請予以更新。 下列資訊清單中的範例會套用至名為 `ag1` 的命名空間。

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - 確認 SQL Server 執行個體的名稱。 如果需要，請予以更新。 下列資訊清單規格中的範例會套用至名為 `mssql1` 的 SQL Server 執行個體。

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  將更新的資訊清單檔儲存至您的工作站。

1. 使用 `kubectl` 部署作業。

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes 會更新可用性群組中一個 SQL Server 執行個體的主要金鑰和 `sa` 密碼。

1. 確認作業已完成。 執行下列命令：若要確認作業已完成，請執行 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  作業成功之後，即會更新一個 SQL Server 執行個體的主要金鑰和 `sa` 密碼。


1. 在您重新執行作業之前，請先刪除作業。 每個作業名稱必須是唯一的。

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

若要為所有 SQL Server 執行個體設定相同的 `sa` 密碼，請對每個 SQL Server 執行個體重複上述步驟。

## <a name="next-steps"></a>後續步驟

[存取 Azure Kubernetes Service (AKS) 隨附的 Kubernetes 儀表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
