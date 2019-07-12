---
title: 管理 SQL Server Always On 可用性群組 Kubernetes
description: 這篇文章說明如何管理 SQL Server Always On 可用性群組在 Kubernetes 中。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6264666009e39706741369b5a4df87ef5564c974
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833236"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>管理 SQL Server Always On 可用性群組 Kubernetes

若要管理 Alwayson 可用性群組在 Kubernetes 上，建立資訊清單，並將它套用到叢集。 資訊清單是`.yaml`檔案。  

這篇文章中的範例適用於所有的 Kubernetes 叢集。 這些範例中的狀況會套用針對在 Azure Kubernetes 服務叢集。

請參閱完整的部署中的範例[部署 SQL Server Always On 可用性群組上的 Kubernetes 叢集](sql-server-linux-kubernetes-deploy.md)。

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>容錯移轉-在 Kubernetes 上的 SQL Server 可用性群組

若要容錯移轉或移動至另一個節點在可用性群組主要複本，完成下列步驟：

1. 資訊清單檔中定義作業。

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -在[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)github 存放庫說明容錯移轉作業。

  將資訊清單檔案複製到您管理終端機中。

  更新您環境的檔案。

  - 取代`<containerName>`預期的可用性群組目標的 pod 名稱 (例如 mssql2-0)。
  - 如果可用性群組不在`ag1`命名空間中，取代`ag1`與命名空間。

  這個檔案會定義名為的容錯移轉作業`manual-failover`。

1. 若要部署作業，使用`kubectl apply`。 下列指令碼會部署作業。

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  部署工作之後，kubernetes，使用 SQL Server 運算子，就會執行下列工作：
  
  - 降級至次要資料庫的主要複本
  
  - 將指定的複本為主要升階
  
  套用資訊清單檔案之後，Kubernetes 會執行作業。 作業會監督員選取新的領導者，並將主要複本移至 SQL Server 執行個體的領導者。

1. 確認作業已完成。
  
  Kubernetes 執行作業之後，您可以檢閱記錄檔。
  
  下列範例會傳回名為作業的狀態`manual-failover`。

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. 刪除手動容錯移轉作業。 

  >[!IMPORTANT]
  >發出另一個的手動容錯移轉之前，您必須手動刪除作業。
  > 
  >在 Kubernetes 中的工作物件保持在完成後，讓您可以檢視其狀態。 您需要注意的是他們的狀態後，手動刪除舊工作。 刪除作業時，也會刪除 Kubernetes 記錄檔。 如果您未刪除作業，未來的容錯移轉作業將會失敗，除非您變更的作業名稱與 pod 選取器。 如需詳細資訊，請參閱 <<c0> [ 執行到完成的工作-](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)。

  下列命令會刪除作業。

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>替換認證

替換認證的密碼重設為 SQL Server`sa`帳戶和 SQL Server[服務主要金鑰](../relational-databases/security/encryption/service-master-key.md)。 

若要完成這項工作中，您會在 Kubernetes 叢集中建立新的密碼，然後再建立 要替換認證的工作。

之前替換認證，請在密碼和主要金鑰的新密碼。

下列指令碼會建立名為祕密`new-sql-secrets`。 執行指令碼之前，請取代`<>`複雜密碼`sapassword`而`masterkeypassword`。 每個個別的值，請使用不同的密碼。

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

每個執行個體的 SQL Server 需要主要金鑰，請完成下列步驟或`sa`密碼。

1. 複製[ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml)終端機您系統管理。

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) 在  [sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/)github 存放庫是這項作業的資訊清單的範例。

  套用此資訊清單之前，請更新您的環境的資訊清單。 檢閱並變更下列設定，視需要。

  - 確認命名空間。 視需要更新。 下列範例資訊清單中的會套用到名為命名空間`ag1`。

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - 請確認 SQL Server 執行個體的名稱。 視需要更新。 下列範例資訊清單規格中的會套用至名為 SQL Server 執行個體`mssql1`。

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  將更新的資訊清單檔案儲存到您的工作站。

1. 使用`kubectl`部署作業。

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes 更新主要金鑰和`sa`一個的執行個體的 SQL Server 可用性群組中的密碼。

1. 確認作業已完成。 執行下列命令：若要確認作業已完成，請執行 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  作業成功，主要金鑰之後和`sa`會更新一個 SQL Server 執行個體的密碼。


1. 再次執行該工作之前，刪除作業。 每個工作名稱必須是唯一的。

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

若要設定為相同`sa`密碼的 SQL Server 的所有執行個體的每個 SQL Server 執行個體重複上述步驟。

## <a name="next-steps"></a>後續步驟

[存取 Kubernetes 儀表板與 Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
