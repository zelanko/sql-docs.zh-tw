---
title: 建立的 SQL Server Always On 可用性群組在 Kubernetes 上部署指令碼
description: 這篇文章說明如何建立 SQL Server Always On 可用性群組在 Kubernetes 上部署指令碼
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dfee5188c6fe54ed91172f9d83de7af6395c8956
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833644"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>建立部署指令碼以 SQL Server Always On 可用性群組

本文說明如何部署上的範例部署指令碼的單一命令中的 Kubernetes 叢集的可用性群組。 `deploy-ag.py` 建立 Python 指令碼`.yaml`可以將它們套用到 Kubernetes 叢集和檔案叢集。

從檔案的檔案下載[sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)。

## <a name="before-you-start"></a>開始之前

在您的工作站上安裝下列工具。

* [Python](https://www.python.org/downloads/) （3.5 或 3.6）
* [PyYAML](https://pyyaml.org/) -Python 套件
* [Kubernetes 用戶端](https://github.com/kubernetes-client/python)-Python 套件

將 python 路徑新增至環境變數中，（適用於 Windows)。

### <a name="install-the-required-components"></a>安裝必要的元件

上述的下列範例會安裝 Python PyYAML 和 Kubernetes 用戶端套件。

安裝 Python 之後，請下載並解壓縮範例資料夾。 

若要設定所需的檔案，請執行下列命令。 取代`<path>`解壓縮的範例檔案的位置。

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>建立叢集，並下載設定檔

下列範例會建立在 Azure Kubernetes Service (AKS) 叢集。

執行指令碼之前，請更新的值，在角括號- `<>`。

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>可用性群組需要 Kubernetes 版本 1.11.0 或更高版本。 此範例會指定 1.11.1。

## <a name="run-the-deployment-script"></a>執行部署指令碼

下列範例示範如何執行`deploy-ag.py`。

### <a name="help"></a>Help

```cmd
python ./deploy-ag.py --help
```

* **使用量**: `deploy-ag.py [-h] {deploy | failover} ...`
* **選擇性引數**:
  * `-h, --help` 顯示此說明訊息並結束
* **子命令**:
  * K8s 代理程式上的動作 {部署 | 容錯移轉}

  `deploy`

   將 SQL Server 可用性群組中一組部署

  `failover`

   容錯移轉至目標複本。

### <a name="deploy-help"></a>部署說明

```cmd
python ./deploy-ag.py deploy --help
```

* **使用量**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  部署 SQL Server 和 namespace(AG name) k8s 代理程式

* **選擇性引數**:
  
  `-h, --help`
  
  顯示此說明訊息並結束
  
  `--verbose, -v`
  
  輸出的詳細資訊
  
  `--ag AG`
  
  可用性群組的名稱。 預設 = ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 命名空間名稱。 如果未指定，則預設為 AG 名稱。

  `--dry-run`
  
  建立資訊清單中，但不是套用它們。
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 執行個體的名稱 （最多 5，並以空格分隔)，預設值 = ['mssql1'、 'mssql2'、 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 密碼。 預設值 = 'SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  略過建立命名空間。

### <a name="failover-help"></a>容錯移轉說明

```cmd
python ./deploy-ag.py failover --help
```
* **使用量**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  手動容錯移轉

* **位置引數**: `target_replica`

  容錯移轉的目標 SQL Server 複本名稱

* **選擇性引數**:

  `-h, --help`
  
  顯示此說明訊息並結束

  `--verbose, -v`
  
  輸出的詳細資訊

  `--ag AG`
  
  可用性群組的名稱。 預設 = ag1

  `--namespace NAMESPACE`

  k8s 命名空間名稱。 如果未指定的 AG 名稱的預設值

  `--dry-run`
  
  建立，但不是會套用資訊清單。

### <a name="create-the-manifests---dont-apply"></a>建立資訊清單-不適用

下列指令碼會建立資訊清單檔案，但不會套用。

```cmd
python ./deploy-ag.py deploy --dry-run
```

下列範例會建立命名空間下的可用性群組的資訊清單`AG1`含三個複本。 執行指令碼之前，請取代`<MyC0m91exP@55w0r!>`使用的複雜密碼。

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

前一個命令會產生範例 yaml 檔案目錄。

在此情況下，命令輸出會顯示建立資訊清單檔案的位置。

![指令碼輸出](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>建立資訊清單，並套用

下列範例會建立命名空間下的可用性群組的資訊清單`ag1`含三個複本並將其套用到 Kubernetes 叢集。 接著，叢集會建立可用性群組。 執行指令碼之前，請取代`<MyC0m91exP@55w0r!>`使用的複雜密碼。

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

指令碼完成之後，Kubernetes 運算子會建立儲存體、 SQL Server 執行個體、 負載平衡器服務。 您可以監視與部署[Kubernetes 儀表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)。

在 Kubernetes 之後建立的 SQL Server 容器：

1. [連接](sql-server-linux-kubernetes-connect.md)叢集中的 SQL Server 執行個體。

1. 建立資料庫。

1. 進行完整備份的資料庫，以便啟動記錄鏈結。

1. 您可以將資料庫加入可用性群組。

使用自動植入讓 SQL Server 會自動建立次要資料庫上適當的複本建立可用性群組。

### <a name="manually-failover"></a>手動容錯移轉

下列範例會容錯移轉主要複本。

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>後續步驟

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
