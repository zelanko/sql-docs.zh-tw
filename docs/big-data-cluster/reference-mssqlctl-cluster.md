---
title: mssqlctl 叢集參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集命令的參考文件。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779262"
---
# <a name="mssqlctl-cluster"></a>mssqlctl cluster

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 叢集建立](#mssqlctl-cluster-create) | 建立叢集。
[mssqlctl 叢集刪除](#mssqlctl-cluster-delete) | 刪除叢集。
[mssqlctl 叢集組態](reference-mssqlctl-cluster-config.md) | 叢集組態命令。
[mssqlctl 叢集端點](reference-mssqlctl-cluster-endpoint.md) | 端點的命令。
[mssqlctl 叢集狀態](reference-mssqlctl-cluster-status.md) | 狀態的命令。
[mssqlctl 叢集偵錯](reference-mssqlctl-cluster-debug.md) | 偵錯命令。
[mssqlctl cluster storage-pool](reference-mssqlctl-cluster-storage-pool.md) | 管理叢集的存放集區。
## <a name="mssqlctl-cluster-create"></a>mssqlctl 叢集建立
建立 SQL Server 巨量資料叢集-kube 設定需要您的系統，以及下列環境變數 ['CONTROLLER_USERNAME'、 'CONTROLLER_PASSWORD'、 'DOCKER_USERNAME'、 'DOCKER_PASSWORD'、 'MSSQL_SA_PASSWORD'、 'KNOX_PASSWORD']。
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>範例
引導式叢集的部署體驗-您將收到提示所需的值。
```bash
mssqlctl cluster create
```
使用引數的叢集部署。
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
使用引數-沒有提示的叢集部署將會被授與--force 旗標用為。
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-file -c`
叢集組態設定檔，用來部署叢集: ['aks-dev-test.json'，' kubeadm-dev-test.json'，' minikube-dev-test.json']
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不要使用這個引數，您可以設定為 'yes' ACCEPT_EULA 環境變數
#### `--node-label -l`
叢集節點的標籤，用來指定要部署到哪些節點。
#### `--force -f`
強制建立的任何值，不提示使用者，所有的問題會列印為 stderr 的一部分。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。
## <a name="mssqlctl-cluster-delete"></a>mssqlctl 叢集刪除
刪除 SQL Server 巨量資料叢集-kube 設定需要您的系統，以及下列環境變數 ['CONTROLLER_USERNAME'，'CONTROLLER_PASSWORD']。
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>範例
其中的控制器的使用者名稱和密碼已設定系統環境中的叢集刪除。
```bash
mssqlctl cluster delete --name <cluster_name>
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
Kubernetes 命名空間所使用的叢集名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除叢集。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。
