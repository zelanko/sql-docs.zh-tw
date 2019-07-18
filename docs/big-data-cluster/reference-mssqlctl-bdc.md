---
title: mssqlctl bdc 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a9da2de60248246bee3daeeaee40d3071da69c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957950"
---
# <a name="mssqlctl-bdc"></a>mssqlctl bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**bdc**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 建立](#mssqlctl-bdc-create) | 建立巨量資料叢集。
[mssqlctl bdc delete](#mssqlctl-bdc-delete) | 刪除巨量資料叢集。
[mssqlctl bdc 組態](reference-mssqlctl-bdc-config.md) | 組態命令。
[mssqlctl bdc 端點](reference-mssqlctl-bdc-endpoint.md) | 端點的命令。
[mssqlctl bdc 狀態](reference-mssqlctl-bdc-status.md) | 狀態的命令。
[mssqlctl bdc 偵錯](reference-mssqlctl-bdc-debug.md) | 偵錯命令。
[mssqlctl bdc storage-pool](reference-mssqlctl-bdc-storage-pool.md) | 儲存體集區的命令。
[mssqlctl bdc 控制項](reference-mssqlctl-bdc-control.md) | 控制命令。
[mssqlctl bdc 集區](reference-mssqlctl-bdc-pool.md) | 集區的命令。
## <a name="mssqlctl-bdc-create"></a>mssqlctl bdc 建立
建立 SQL Server 巨量資料叢集-kube 設定需要您的系統，以及下列環境變數 ['CONTROLLER_USERNAME'、 'CONTROLLER_PASSWORD'、 'DOCKER_USERNAME'、 'DOCKER_PASSWORD'、 'MSSQL_SA_PASSWORD'、 'KNOX_PASSWORD']。
```bash
mssqlctl bdc create [--config-profile -c] 
                    [--accept-eula -a]  
                    [--node-label -l]  
                    [--force -f]
```
### <a name="examples"></a>範例
引導式的 BDC 部署體驗-您會收到提示所需的值。
```bash
mssqlctl bdc create
```
使用引數的 BDC 部署。
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test
```
BDC 部署使用的引數---force 旗標用做將會不提供任何提示。
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-profile -c`
BDC 組態設定檔，用來部署叢集: ['aks-開發 / 測試 '、 'kubeadm-開發 / 測試 '、' minikube-開發 / 測試 ']
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不要使用這個引數，您可以設定為 'yes' ACCEPT_EULA 環境變數
#### `--node-label -l`
BDC 節點標籤，用來指定要部署到哪些節點。
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
## <a name="mssqlctl-bdc-delete"></a>mssqlctl bdc delete
刪除 SQL Server 巨量資料叢集-kube 設定需要您的系統，以及下列環境變數 ['CONTROLLER_USERNAME'，'CONTROLLER_PASSWORD']。
```bash
mssqlctl bdc delete --name -n 
                    [--force -f]
```
### <a name="examples"></a>範例
BDC 刪除其中的控制器的使用者名稱和密碼已設定系統環境中。
```bash
mssqlctl bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
Kubernetes 命名空間所使用的 BDC 名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除 BDC。
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
