---
title: 在 Kubernetes 上建立 SQL Server Always On 可用性群組的部署指令碼
description: 本文說明如何在 Kubernetes 上建立 SQL Server Always On 可用性群組的部署指令碼
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000137"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>建立 SQL Server Always On 可用性群組的部署指令碼

本文描述如何以包含範例部署指令碼的單一命令，在 Kubernetes 叢集上部署可用性群組。 `deploy-ag.py` 是 Python 指令碼，它會為叢集建立 `.yaml` 檔案，並可將其套用至 Kubernetes 叢集。

請從 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) 下載檔案。

## <a name="before-you-start"></a>開始之前

在您的工作站上安裝下列工具。

* [Python](https://www.python.org/downloads/) (3.5 或 3.6)
* [PyYAML](https://pyyaml.org/) - Python 套件
* [Kubernetes 用戶端](https://github.com/kubernetes-client/python) - Python 套件

將 python 路徑新增至環境變數 (適用於 Windows)。

### <a name="install-the-required-components"></a>安裝必要的元件

下列範例會安裝適用於 Python 的 PyYAML 和 Kubernetes 用戶端套件。

安裝 Python 之後，請下載並解壓縮範例資料夾。 

若要設定必要的檔案，請執行下列命令。 請以解壓縮範例檔案的位置取代 `<path>`。

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>建立叢集並下載設定檔

下列範例會在 Azure Kubernetes Service (AKS) 中建立叢集。

執行指令碼之前，請先更新角括弧 (`<>`) 中的值。

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>可用性群組需要 Kubernetes 1.11.0 版或更高版本。 此範例會指定 1.11.1。

## <a name="run-the-deployment-script"></a>執行部署指令碼

下列範例示範如何執行 `deploy-ag.py`。

### <a name="help"></a>說明

```cmd
python ./deploy-ag.py --help
```

* **使用方式**：`deploy-ag.py [-h] {deploy | failover} ...`
* **選擇性引數**：
  * `-h, --help` 顯示此說明訊息並結束
* **子命令**：
  * 對 k8s 代理程式的動作 {deploy | failover}

  `deploy`

   在可用性群組中部署一組 SQL Server

  `failover`

   容錯移轉至目標複本。

### <a name="deploy-help"></a>Deploy 說明

```cmd
python ./deploy-ag.py deploy --help
```

* **使用方式**：

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  在命名空間 (AG 名稱) 中部署 SQL Server 和 k8s 代理程式

* **選擇性引數**：
  
  `-h, --help`
  
  顯示此說明訊息並結束
  
  `--verbose, -v`
  
  輸出的詳細資訊
  
  `--ag AG`
  
  可用性群組的名稱。 預設=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 命名空間的名稱。 若未指定，則預設為 AG 名稱。

  `--dry-run`
  
  建立資訊清單，但不要套用這些資訊清單。
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 執行個體的名稱 (最多 5個，以空格分隔) 預設=['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 密碼。 預設='SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  略過命名空間建立作業。

### <a name="failover-help"></a>Failover 說明

```cmd
python ./deploy-ag.py failover --help
```
* **使用方式**： 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  手動容錯移轉

* **位置引數**：`target_replica`

  用於容錯移轉的目標 SQL Server 複本名稱

* **選擇性引數**：

  `-h, --help`
  
  顯示此說明訊息並結束

  `--verbose, -v`
  
  輸出的詳細資訊

  `--ag AG`
  
  可用性群組的名稱。 預設=ag1

  `--namespace NAMESPACE`

  k8s 命名空間的名稱。 若未指定，則預設為 AG 名稱

  `--dry-run`
  
  建立但不要套用資訊清單。

### <a name="create-the-manifests---dont-apply"></a>建立資訊清單 - 不套用

下列指令碼會建立資訊清單檔案，但不會套用這些檔案。

```cmd
python ./deploy-ag.py deploy --dry-run
```

下列範例會在具有三個複本的命名空間 `AG1` 下建立可用性群組資訊清單。 執行指令碼之前，請以複雜密碼取代 `<MyC0m91exP@55w0r!>`。

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

上一個命令會產生範例 YAML 檔案目錄。

在此情況下，命令輸出會顯示資訊清單檔案的建立位置。

![指令碼輸出](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>建立資訊清單並套用

下列範例會在具有三個複本的命名空間 `ag1` 下建立可用性群組資訊清單，並將其套用至您的 Kubernetes 叢集。 叢集接著會建立可用性群組。 執行指令碼之前，請以複雜密碼取代 `<MyC0m91exP@55w0r!>`。

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

指令碼完成之後，Kubernetes 運算子會建立儲存體、SQL Server 執行個體、負載平衡器服務。 您可以使用 [Kubernetes 儀表板](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)來監視部署。

Kubernetes 建立 SQL Server 容器之後：

1. [連線](sql-server-linux-kubernetes-connect.md)到叢集中的 SQL Server 執行個體。

1. 建立資料庫。

1. 完整備份資料庫以利啟動記錄鏈結。

1. 將資料庫新增至可用性群組。

使用自動植入建立可用性群組，因此 SQL Server 會在適當的複本上自動建立次要資料庫。

### <a name="manually-failover"></a>手動容錯移轉

下列範例會為主要複本進行容錯移轉。

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>後續步驟

[Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)
