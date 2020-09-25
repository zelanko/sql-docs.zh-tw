---
title: azdata arc dc reference
titleSuffix: SQL Server big data clusters
description: azdata arc dc 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79798b8818a028edbe372e2a8cb341c5296582ba
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942368"
---
# <a name="azdata-arc-dc"></a>azdata arc dc

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc dc create](#azdata-arc-dc-create) | 建立資料控制器。
[azdata arc dc delete](#azdata-arc-dc-delete) | 刪除資料控制器。
[azdata arc dc endpoint](reference-azdata-arc-dc-endpoint.md) | 端點命令。
[azdata arc dc status](reference-azdata-arc-dc-status.md) | 狀態命令。
[azdata arc dc config](reference-azdata-arc-dc-config.md) | 組態命令。
[azdata arc dc debug](reference-azdata-arc-dc-debug.md) | 偵錯命令。
[azdata arc dc export](#azdata-arc-dc-export) | 匯出計量、記錄或使用量。
[azdata arc dc upload](#azdata-arc-dc-upload) | 上傳已匯出的資料檔案。
## <a name="azdata-arc-dc-create"></a>azdata arc dc create
建立資料控制器 - 您的系統需要 Kube 組態，以及下列環境變數 ['AZDATA_USERNAME', 'AZDATA_PASSWORD']。
```bash
azdata arc dc create --namespace -ns 
                     --name -n  
                     
--connectivity-mode  
                     
--resource-group -g  
                     
--location -l  
                     
--subscription -s  
                     
[--profile-name]  
                     
[--path -p]  
                     
[--storage-class -sc]
```
### <a name="examples"></a>範例
資料控制器部署。
```bash
azdata arc dc create
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
要在其中部署資料控制器的 Kubernetes 命名空間。 如果已存在，就會加以使用。 如果不存在，則會先嘗試加以建立。
#### `--name -n`
資料控制器的名稱。
#### `--connectivity-mode`
資料控制器據以運作的 Azure 連線 (間接或直接)。
#### `--resource-group -g`
應新增資料控制器資源的 Azure 資源群組。
#### `--location -l`
將用來儲存資料控制器中繼資料的 Azure 位置 (例如 eastus)。
#### `--subscription -s`
應新增資料控制器資源的 Azure 訂用帳戶識別碼。
### <a name="optional-parameters"></a>選擇性參數
#### `--profile-name`
現有組態設定檔的名稱。 執行 `azdata arc dc config list` 以查看可用的選項。 下列其中一項：['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-kubeadm', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci']。
#### `--path -p`
要使用的自訂組態設定檔所在目錄的路徑。 執行 `azdata arc dc config init` 以建立自訂組態檔。
#### `--storage-class -sc`
要用於所有資料的儲存類別，會針對需要永續性磁碟區的所有資料控制器 Pod 記錄這類磁碟區。
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
## <a name="azdata-arc-dc-delete"></a>azdata arc dc delete
刪除資料控制器 - 您的系統需要 Kube 組態。
```bash
azdata arc dc delete --name -n 
                     --namespace -ns  
                     
[--force -f]
```
### <a name="examples"></a>範例
資料控制器部署。
```bash
azdata arc dc delete
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
資料控制器名稱。
#### `--namespace -ns`
資料控制器所在的 Kubernetes 命名空間。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除資料控制器。
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
## <a name="azdata-arc-dc-export"></a>azdata arc dc export
將計量、記錄或使用量匯出至檔案。
```bash
azdata arc dc export --type -t 
                     --path -p  
                     
[--force -f]
```
### <a name="required-parameters"></a>必要參數
#### `--type -t`
要匯出的資料類型。 選項：記錄、計量和使用量。
#### `--path -p`
完整或相對路徑，包括要匯出之檔案的檔案名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制建立輸出檔案。 覆寫位於相同路徑的任何現有檔案。
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
## <a name="azdata-arc-dc-upload"></a>azdata arc dc upload
將從資料控制器匯出的資料檔案上傳至 Azure。
```bash
azdata arc dc upload --path -p 
                     
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
完整或相對路徑，包括要上傳之檔案的檔案名稱。
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

如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata](..\install\deploy-install-azdata.md)。

