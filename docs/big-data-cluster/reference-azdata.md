---
title: azdata 參考
titleSuffix: SQL Server big data clusters
description: Azdata 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425988"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供適用于[SQL Server 2019 big data 叢集 (預覽)](big-data-cluster-overview.md)之**azdata**工具的參考。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata 應用程式](reference-azdata-app.md) | 建立、刪除、執行及管理應用程式。 |
|[azdata bdc](reference-azdata-bdc.md) | 選取、管理和操作 SQL Server Big Data 叢集。 |
|[azdata 筆記本](reference-azdata-notebook.md) | 用來從終端機查看、執行和管理筆記本的命令。 |
[azdata 登入](#azdata-login) | 登入叢集的控制器端點。
[azdata 登出](#azdata-logout) | 登出叢集。
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI 可讓使用者透過 T-sql 與 SQL Server 進行互動。 |
## <a name="azdata-login"></a>azdata 登入
當您部署叢集時, 它會在部署期間列出控制器端點, 您應該用它來登入。  如果您不知道控制器端點, 您可以藉由在系統上將叢集的 kube 設定設為預設位置<user home>/.kube/config, 或使用 KUBECONFIG env var (例如 export KUBECONFIG = path/to/. kube/config) 來登入。
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>範例
以互動方式登入。 如果未指定為引數, 則一律會提示您輸入叢集名稱。 如果您的系統上已設定 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA env 變數, 則不會提示您輸入。 如果您的系統上有 kube 設定, 或使用 KUBECONFIG env var 來指定 config 的路徑, 則互動式體驗會先嘗試使用此配置, 然後在設定失敗時提示您。
```bash
azdata login
```
登入 (非互動)。 以 [叢集名稱]、[控制器使用者名稱]、[控制器端點] 和 [EULA 接受] 設定做為引數登入。 必須設定環境變數 CONTROLLER_PASSWORD。  如果您不想要指定控制器端點, 請在您的電腦上將 kube 設定設為預設位置<user home>/.kube/config, 或使用 KUBECONFIG env var, 亦即 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
使用電腦上的 kube config 和針對 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 設定的 env var 進行登入。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>選擇性參數
#### `--cluster-name -n`
叢集名稱。
#### `--controller-username -u`
帳戶使用者。 如果您不想要使用這個 arg, 您可以設定環境變數 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
叢集控制器端點 "https://host:port "。 如果您不想要使用這個 arg, 可以在您的電腦上使用 kube 設定。 請確定設定位於<user home>/.kube/config 的預設位置, 或使用 KUBECONFIG env var。
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不想要使用這個 arg, 您可以將環境變數 ACCEPT_EULA 設定為 [是]。 此產品的授權條款可于 https://aka.ms/azdata-eula 查看。
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
## <a name="azdata-logout"></a>azdata 登出
登出叢集。
```bash
azdata logout 
```
### <a name="examples"></a>範例
登出這個使用者。
```bash
azdata logout
```
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

如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
