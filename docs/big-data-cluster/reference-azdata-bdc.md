---
title: azdata bdc 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5d5cb5256f4a1b8389d882300a89f0ee0012a99
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74820981"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下文提供 `bdc` 工具中 `azdata` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | 建立巨量資料叢集。
[azdata bdc delete](#azdata-bdc-delete) | 刪除巨量資料叢集。
[azdata bdc upgrade](#azdata-bdc-upgrade) | 更新 SQL Server 巨量資料叢集中每個容器所部署的映像。
[azdata bdc config](reference-azdata-bdc-config.md) | 組態命令。
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | 端點命令。
[azdata bdc debug](reference-azdata-bdc-debug.md) | 偵錯命令。
[azdata bdc status](reference-azdata-bdc-status.md) | BDC 狀態命令。
[azdata bdc control](reference-azdata-bdc-control.md) | 控制服務命令。
[azdata bdc sql](reference-azdata-bdc-sql.md) | SQL 服務命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 服務命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 服務命令。
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | 閘道服務命令。
[azdata bdc app](reference-azdata-bdc-app.md) | 應用程式服務命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 命令可讓使用者透過建立和管理工作階段、陳述式和批次，與 Spark 系統進行互動。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 模組提供用來存取 HDFS 檔案系統的命令。
## <a name="azdata-bdc-create"></a>azdata bdc create
建立 SQL Server 巨量資料叢集 - 系統上必須有 Kubernetes 設定，以及下列環境變數 ['AZDATA_USERNAME', 'AZDATA_PASSWORD']。
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>範例
引導式 BDC 部署體驗；您將會接收到所需值的提示。
```bash
azdata bdc create
```
包含引數的 BDC 部署。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
設定檔中具有指定名稱 (而不是預設名稱) 的 BDC 部署。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
包含引數的 BDC 部署 - 使用 --force 旗標時，不會提供任何提示。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
#### `--config-profile -c`
巨量資料叢集組態設定檔，用於部署叢集：['kubeadm-dev-test', 'kubeadm-prod', 'aks-dev-test', 'aks-dev-test-ha']
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 您可以在 https://aka.ms/eula-azdata-en 中查看 azdata 的授權條款，而巨量資料叢集的授權條款則位於下列位置 - Enterprise： https://go.microsoft.com/fwlink/?linkid=2104292 、Standard： https://go.microsoft.com/fwlink/?linkid=2104294 、Developer： https://go.microsoft.com/fwlink/?linkid=2104079 。
#### `--node-label -l`
巨量資料叢集節點標籤，用來指定要部署至的目標節點。
#### `--force -f`
強制建立，系統不會提示使用者輸入任何值，而且所有問題都會列印成標準錯誤輸出的一部分。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-delete"></a>azdata bdc delete
刪除 SQL Server 巨量資料叢集 - 系統上必須有 Kubernete 設定。
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>範例
BDC 刪除。
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除巨量資料叢集。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
更新 SQL Server 巨量資料叢集中每個容器所部署的映像。 更新的映像是以所傳入 Docker 映像為基礎。 如果已更新映像來自於目前所部署映像以外的不同 Docker 映像存放庫，則也需要 "repository" 參數。
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   [--repository -r]
```
### <a name="examples"></a>範例
BDC 會從相同存放庫升級至新的映像標籤 "cu2"。
```bash
azdata bdc upgrade -t cu2
```
BDC 會從新存放庫 "foo/bar/baz" 升級至標籤為 "cu2" 的新映像。
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
#### `--tag -t`
要升級叢集中所有容器的目標 Docker 映像標籤。
### <a name="optional-parameters"></a>選擇性參數
#### `--repository -r`
要讓叢集中所有容器提取其映像的 Docker 存放庫。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
