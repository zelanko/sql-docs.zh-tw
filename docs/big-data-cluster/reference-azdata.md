---
title: azdata 參考
titleSuffix: SQL Server big data clusters
description: azdata 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 33cc3070647c58e6ae57c8bff3d587a76ae0a28d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653092"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供適用[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]于 (預覽)](big-data-cluster-overview.md)之**azdata**工具的參考。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]manage ](deploy-install-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | 建立、刪除、執行和管理應用程式。 |
|[azdata bdc](reference-azdata-bdc.md) | 選取、管理和操作 SQL Server 巨量資料叢集。 |
|[azdata login](#azdata-login) | 登入叢集的控制器端點。
|[azdata logout](#azdata-logout) | 登出叢集。

## <a name="azdata-login"></a>azdata login
當您部署叢集時, 它會在部署期間列出控制器端點, 您應該使用這種方式來登入。  如果您不知道控制器端點, 您可以登入, 方法是在系統上將叢集的 kube 設定設為預設位置<user home>/.kube/config, 或使用 KUBECONFIG env var, 也就是 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>範例
以互動方式登入。 如果沒有提供叢集名稱作為參數，系統一律會提示您輸入。 如果您已經在系統上設定 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 環境變數，則系統不會提示您輸入這些項目。 如果您的系統上有 Kube 組態，或您使用 KUBECONFIG 環境變數來指定該組態路徑，則互動式體驗會先嘗試使用組態，如果組態失敗系統會再提示您。
```bash
azdata login
```
登入 (非互動)。 將叢集名稱、控制器使用者名稱、控制器端點和 EULA 接受設定為引數來登入。 必須設定環境變數 CONTROLLER_PASSWORD。  如果您不想要指定控制器端點, 請在您的電腦上, 將 kube 設定置於預設位置<user home>/.kube/config, 或使用 KUBECONFIG env var, 也就是 export KUBECONFIG = path/to/. kube/config。
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
使用機器上的 Kube 組態和設定環境變數 CONTROLLER_USERNAME、CONTROLLER_PASSWORD 和 ACCEPT_EULA 來登入。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>選擇性參數
#### `--cluster-name -n`
叢集名稱。
#### `--controller-username -u`
帳戶使用者。 如果不想要使用此引數，您可以設定環境變數 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
叢集控制器端點 "https://host:port"。 如果不想要使用此引數，您可以使用您機器上的 Kube 組態。 請確定設定位於<user home>/.kube/config 的預設位置, 或使用 KUBECONFIG env var。
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊, [http://jmespath.org/](http://jmespath.org/])請參閱, 以取得詳細資訊和範例。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-logout"></a>azdata logout
登出叢集。
```bash
azdata logout 
```
### <a name="examples"></a>範例
登出此使用者。
```bash
azdata logout
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊, [http://jmespath.org/](http://jmespath.org/])請參閱, 以取得詳細資訊和範例。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]manage ](deploy-install-azdata.md)。
