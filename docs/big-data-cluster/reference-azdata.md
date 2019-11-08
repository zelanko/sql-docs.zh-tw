---
title: azdata 參考
titleSuffix: SQL Server big data clusters
description: azdata 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4ef2ba9c68f3586e159c326863ef76ba231f01b9
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531654"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[azdata bdc](reference-azdata-bdc.md) | 選取、管理和操作 SQL Server 巨量資料叢集。 |
|[azdata app](reference-azdata-app.md) | 建立、刪除、執行和管理應用程式。 |
[azdata login](#azdata-login) | 登入叢集的控制器端點，並將其命名空間設定為使用中內容。 若要在登入時使用密碼，您必須設定 AZDATA_PASSWORD 環境變數。
[azdata logout](#azdata-logout) | 登出叢集。
|[azdata context](reference-azdata-context.md) | 內容管理命令。 |
|[azdata control](reference-azdata-control.md) | 建立、刪除及管理控制平面。 |
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI 可讓使用者透過 T-SQL 與 SQL Server 互動。 |
|[azdata notebook](reference-azdata-notebook.md) | 用來從終端機查看、執行和管理筆記本的命令。 |
## <a name="azdata-login"></a>azdata login
當叢集已部署時，它會在部署期間列出控制器端點，您應該使用此端點來登入。  如果您不知道控制器端點，您可以藉由將您叢集的 Kube 組態放在您系統的預設位置 <user home>/.kube/config 來登入，或使用 KUBECONFIG 環境變數，也就是 export KUBECONFIG=路徑/至/.kube/config。當您登入時，此叢集的命名空間將會設定為使用中內容。
```bash
azdata login [--auth] 
             [--endpoint -e]  
             [--accept-eula -a]  
             [--namespace -n]  
             [--username -u]  
             [--principal -p]
```
### <a name="examples"></a>範例
使用基本驗證登入。
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
使用 Active Directory 登入。
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
使用具有明確主體的 Active Directory 登入。
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
以互動方式登入。 如果沒有提供叢集名稱作為參數，系統一律會提示您輸入。 如果您已經在系統上設定 AZDATA_USERNAME、AZDATA_PASSWORD 和 ACCEPT_EULA 環境變數，則系統不會提示您輸入這些項目。 如果您的系統上有 Kube 組態，或您使用 KUBECONFIG 環境變數來指定該組態路徑，則互動式體驗會先嘗試使用組態，如果組態失敗系統會再提示您。
```bash
azdata login
```
登入 (非互動)。 將叢集名稱、控制器使用者名稱、控制器端點和 EULA 接受設定為引數來登入。 必須設定環境變數 AZDATA_PASSWORD。  如果您不想要指定控制器端點，請將 Kube 組態放在您機器上的預設位置 <user home>/.kube/config，或使用 KUBECONFIG 環境變數，也就是 export KUBECONFIG=路徑/至/.kube/config。
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
使用機器上的 Kube 設定和環境變數設定 AZDATA_USERNAME、AZDATA_PASSWORD 和 ACCEPT_EULA 來登入。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>選擇性參數
#### `--auth`
驗證策略。 基本或 Active Directory 驗證。 預設為「基本」驗證。
#### `--endpoint -e`
叢集控制器端點 "https://host:port"。 如果不想要使用此引數，您可以使用您機器上的 Kube 組態。 請確定組態位於預設位置 <user home>/.kube/config，或使用 KUBECONFIG 環境變數。
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 此產品的授權條款可在 https://aka.ms/eula-azdata-en 檢視。
#### `--namespace -n`
叢集控制平面的命名空間。
#### `--username -u`
帳戶使用者。 如果不想要使用此引數，您可以設定環境變數 AZDATA_USERNAME。
#### `--principal -p`
您的 Kerberos 領域。 在大部分情況下，您的 Kerberos 領域是您的網域名稱，以大寫字母表示。
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
