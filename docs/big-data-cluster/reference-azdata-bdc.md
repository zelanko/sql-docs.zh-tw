---
title: azdata bdc 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408b3c2d55d5e2515a2df979cd54b380a0d54704
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155134"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的參考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | 建立巨量資料叢集。
[azdata bdc delete](#azdata-bdc-delete) | 刪除巨量資料叢集。
[azdata bdc config](reference-azdata-bdc-config.md) | 組態命令。
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | 端點命令。
[azdata bdc debug](reference-azdata-bdc-debug.md) | 偵錯命令。
[azdata bdc status](reference-azdata-bdc-status.md) | BDC 狀態命令。
[azdata bdc control](reference-azdata-bdc-control.md) | 控制服務命令。
[azdata bdc sql](reference-azdata-bdc-sql.md) | Sql 服務命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Hdfs 服務命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 服務命令。
[azdata bdc 閘道](reference-azdata-bdc-gateway.md) | 閘道服務命令。
[azdata bdc 應用程式](reference-azdata-bdc-app.md) | App service 命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 模組提供用來存取 HDFS 檔案系統的命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 命令可讓使用者透過建立和管理工作階段、陳述式和批次，與 Spark 系統進行互動。
## <a name="azdata-bdc-create"></a>azdata bdc create
建立 SQL Server Big Data 叢集-您的系統上必須有 Kubernetes 設定, 以及下列環境變數 [' CONTROLLER_USERNAME '、' CONTROLLER_PASSWORD '、' MSSQL_SA_PASSWORD '、' KNOX_PASSWORD ']。
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
用於部署叢集的大型資料叢集設定設定檔: [' aks-開發/測試 ', ' kubeadm-生產」, ' minikube-開發/測試 ', ' kubeadm-開發/測試 ']
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 此產品的授權條款可在 https://aka.ms/azdata-eula 與 https://go.microsoft.com/fwlink/?LinkId=2002534 檢視。
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-delete"></a>azdata bdc delete
刪除 SQL Server Big Data 叢集-您的系統上必須有 Kubernetes 設定。
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

- 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

- 如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
