---
title: mssqlctl 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5567b46376acc5aee6c42cdae19eef133c7af506
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957893"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**mssqlctl**工具[SQL Server 2019 巨量資料叢集 （預覽）](big-data-cluster-overview.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[mssqlctl 應用程式](reference-mssqlctl-app.md) | 建立、 刪除、 執行和管理應用程式。 |
|[mssqlctl bdc](reference-mssqlctl-bdc.md) | 選取、 管理及操作 SQL Server 巨量資料叢集。 |
|[mssqlctl hdfs](reference-mssqlctl-hdfs.md) | HDFS 模組提供命令，以存取 HDFS 檔案系統。 |
[mssqlctl 登入](#mssqlctl-login) | 登入叢集的控制站的端點。
[mssqlctl 登出](#mssqlctl-logout) | 記錄移出叢集。
|[mssqlctl sql](reference-mssqlctl-sql.md) | SQL DB CLI 可讓使用者透過 T-SQL 的 SQL 伺服器互動。 |
## <a name="mssqlctl-login"></a>mssqlctl 登入
部署您的叢集時，它會列出控制器端點在部署期間，您應該用來登入。  如果您不知道控制器端點，您可能會讓您的叢集 kube 設定您的系統中的預設位置上的登入<user home>/.kube/config 或使用 KUBECONFIG 環境變數，也就是匯出 KUBECONFIG=path/to/.kube/config。
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>範例
以互動方式登入。 叢集名稱將一律會提示您輸入若未指定做為引數。 如果您有 CONTROLLER_USERNAME、 CONTROLLER_PASSWORD 和 ACCEPT_EULA 環境變數設定在您的系統上，這些不會提示的。 如果您 kube 設定您的系統上，或使用指定的路徑設定 KUBECONFIG 環境變數，互動式的體驗會先嘗試使用組態檔，然後提示您，如果組態失敗。
```bash
mssqlctl login
```
（非互動方式），登入。 叢集名稱、 控制器的使用者名稱、 控制器端點和設定做為引數接受登入。 CONTROLLER_PASSWORD 必須設定環境變數。  如果您不要指定控制器的端點，請對 kube 設定您的電腦中的預設位置<user home>/.kube/config 或使用 KUBECONFIG 環境變數，也就是匯出 KUBECONFIG=path/to/.kube/config。
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
登入機器，然後設定 CONTROLLER_USERNAME、 CONTROLLER_PASSWORD，和 ACCEPT_EULA 環境變數上的 kube 組態。
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>選擇性參數
#### `--cluster-name -n`
叢集名稱。
#### `--controller-username -u`
帳戶的使用者。 如果您不要使用這個引數，您可以設定環境變數 CONTROLLER_USERNAME。
#### `--controller-endpoint -e`
叢集控制器端點 」 https://host:port"。 如果您不要使用這個引數，您可以使用 kube 設定您的電腦上。 請確定 組態的預設位置位於<user home>/.kube/config 或 使用 KUBECONFIG 環境變數。
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不要使用這個引數，您可以設定為 'yes' ACCEPT_EULA 環境變數
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
## <a name="mssqlctl-logout"></a>mssqlctl 登出
記錄移出叢集。
```bash
mssqlctl logout 
```
### <a name="examples"></a>範例
登出這位使用者。
```bash
mssqlctl logout
```
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

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。