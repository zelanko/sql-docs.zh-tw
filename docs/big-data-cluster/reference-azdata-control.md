---
title: azdata 控制項參考
titleSuffix: SQL Server big data clusters
description: Azdata 控制命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2ce02ef0b212070b4a52944e055404137c78c98b
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304727"
---
# <a name="azdata-control"></a>azdata 控制項

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的參考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 控制項建立](#azdata-control-create) | 建立控制平面。
[azdata 控制項刪除](#azdata-control-delete) | 刪除控制平面。
## <a name="azdata-control-create"></a>azdata 控制項建立
建立控制平面-您的系統上必須有 kube 設定，以及下列環境變數 [' CONTROLLER_USERNAME '、' CONTROLLER_PASSWORD '、' MSSQL_SA_PASSWORD '、' KNOX_PASSWORD ']。
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>範例
控制項部署。
```bash
azdata control create
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
用於 kubernetes 命名空間的控制項平面名稱。
#### `--config-profile -c`
叢集設定檔，用於部署叢集： [' aks-開發/測試 '，' kubeadm-生產」，' minikube-開發/測試 '，' kubeadm-開發/測試 ']
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 
#### `--node-label -l`
節點標籤，用來指定要部署的目標節點。
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
## <a name="azdata-control-delete"></a>azdata 控制項刪除
刪除控制平面-您的系統上必須有 kube 設定。
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>範例
控制項部署。
```bash
azdata control delete
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
用於 kubernetes 命名空間的控制平面名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--force -f`
強制刪除控制平面。
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
