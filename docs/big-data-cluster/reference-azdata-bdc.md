---
title: azdata bdc 參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426038"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令

|     |     |
| --- | --- |
[azdata bdc 建立](#azdata-bdc-create) | 建立 Big Data Cluster。
[azdata bdc 刪除](#azdata-bdc-delete) | 刪除 Big Data Cluster。
[azdata bdc 設定](reference-azdata-bdc-config.md) | 設定命令。
[azdata bdc 端點](reference-azdata-bdc-endpoint.md) | 端點命令。
[azdata bdc 狀態](reference-azdata-bdc-status.md) | 狀態命令。
[azdata bdc debug](reference-azdata-bdc-debug.md) | Debug 命令。
[azdata bdc 控制項](reference-azdata-bdc-control.md) | 控制命令。
[azdata bdc 集區](reference-azdata-bdc-pool.md) | 集區命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 模組提供用來存取 HDFS 檔案系統的命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 命令可讓使用者建立和管理會話、語句和批次, 以與 Spark 系統進行互動。
## <a name="azdata-bdc-create"></a>azdata bdc 建立
建立 SQL Server Big Data 叢集-您的系統上必須有 kube 設定, 以及下列環境變數 [' CONTROLLER_USERNAME '、' CONTROLLER_PASSWORD '、' MSSQL_SA_PASSWORD '、' KNOX_PASSWORD ']。
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>範例

引導式 BDC 部署經驗-您會收到所需值的提示。

```bash
azdata bdc create
```

具有引數的 BDC 部署。

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
設定檔中具有指定名稱的 BDC 部署, 而不是預設名稱。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

具有引數的 BDC 部署-使用--force 旗標時, 不會提供任何提示。

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
Big data cluster name, 用於 kubernetes 命名空間。
#### `--config-profile -c`
大型資料叢集設定設定檔, 用於部署叢集: [' aks-開發/測試 ', ' kubeadm-開發/測試 ', ' minikube-開發/測試 ']
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不想要使用這個 arg, 您可以將環境變數 ACCEPT_EULA 設定為 [是]。 此產品的授權條款可以在 https://aka.ms/azdata-eula 和 https://go.microsoft.com/fwlink/?LinkId=2002534 中查看。
#### `--node-label -l`
海量資料叢集節點標籤, 用來指定要部署的目標節點。
#### `--force -f`
強制建立時, 系統不會提示使用者輸入任何值, 而且所有問題都會列印成 stderr 的一部分。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。
## <a name="azdata-bdc-delete"></a>azdata bdc 刪除
刪除 SQL Server Big Data 叢集-您的系統上必須有 kube 設定, 以及下列環境變數 [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ']。
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>範例
BDC 刪除, 其中的控制器使用者名稱和密碼已設定在您的系統內容中。
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
Big data cluster name, 用於 kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除海量資料叢集。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。

## <a name="next-steps"></a>後續步驟

如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
