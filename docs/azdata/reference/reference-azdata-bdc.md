---
title: azdata bdc 參考
titleSuffix: SQL Server big data clusters
description: 使用此參考文章了解 azdata 工具中的 SQL 命令，特別是許多 bdc 命令。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dee94bc76f1a59940a753eec6944ccdab8bfc943
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733571"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 命令可讓使用者透過建立和管理工作階段、陳述式和批次，與 Spark 系統進行互動。
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
透過 `azdata bdc config init` 初始化，包含引數的 BDC 部署和自訂組態設定檔。
```bash
azdata bdc create --accept-eula yes --config-profile ./path/to/config/profile
```
包含指定自訂叢集名稱，以及預設組態設定檔 aks-dev-test 的 BDC 部署。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test
```
包含引數的 BDC 部署 - 使用 --force 旗標時，不會提供任何提示。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
#### `--config-profile -c`
巨量資料叢集組態設定檔，用來部署叢集：['openshift-dev-test', 'aro-dev-test-ha', 'aks-dev-test', 'openshift-prod', 'aks-dev-test-ha', 'kubeadm-prod', 'aro-dev-test', 'kubeadm-dev-test']
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 您可在 https://aka.ms/eula-azdata-en 檢視 azdata 的授權條款。
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
更新 SQL Server 巨量資料叢集中每個容器所部署的映像。 更新的映像是以所傳入 Docker 映像為基礎。 如果已更新映像來自於目前所部署映像以外的不同 Docker 映像存放庫，則也需要 "repository" 參數。
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   
[--repository -r]  
                   
[--controller-timeout -k]  
                   
[--stability-threshold -s]  
                   
[--component-timeout -p]
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
BDC 會從相同的存放庫升級到包含標籤 "cu2" 的新映像。升級將會等待控制器升級 30 分鐘，並等待控制器資料庫升級 30 分鐘。 然後，其接著會等待控制器和控制器資料庫執行三分鐘，而不會損毀升級叢集的其餘部分。 每個後續的升級階段將需四十分鐘來完成。
```bash
azdata bdc upgrade -t cu2 --controller-timeout=30 --component-timeout=40 --stability-threshold=3
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
#### `--tag -t`
要升級叢集中所有容器的目標 Docker 映像標籤。
### <a name="optional-parameters"></a>選擇性參數
#### `--repository -r`
要讓叢集中所有容器提取其映像的 Docker 存放庫。
#### `--controller-timeout -k`
在復原升級前等待控制器或控制器資料庫升級的分鐘數。
#### `--stability-threshold -s`
在將升級標記為穩定前，於升級後等待的分鐘數。
#### `--component-timeout -p`
在暫停升級前，於升級的每個階段 (控制器升級後) 等待升級完成的分鐘數。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](../install/deploy-install-azdata.md)。
