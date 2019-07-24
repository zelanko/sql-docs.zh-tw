---
title: azdata 應用程式參考
titleSuffix: SQL Server big data clusters
description: Azdata 應用程式命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 793edde26ebebf9e55c5751adbedf662142280de
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426278"
---
# <a name="azdata-app"></a>azdata 應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**應用程式**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 應用程式範本](reference-azdata-app-template.md) | 範本.
[azdata 應用程式初始化](#azdata-app-init) | Kickstart 新的應用程式基本架構。
[azdata 應用程式建立](#azdata-app-create) | 建立應用程式。
[azdata 應用程式更新](#azdata-app-update) | 更新應用程式。
[azdata 應用程式清單](#azdata-app-list) | 列出應用程式。
[azdata 應用程式刪除](#azdata-app-delete) | 刪除應用程式。
[azdata 應用程式執行](#azdata-app-run) | 執行應用程式。
[azdata 應用程式描述](#azdata-app-describe) | 描述應用程式。
## <a name="azdata-app-init"></a>azdata 應用程式初始化
協助您根據執行時間環境來 kickstart 新的應用程式基本架構和 (或) 規格檔案。
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>範例
僅 Scaffold 新的`spec.yaml`應用程式。
```bash
azdata app init --spec
```
Scaffold 以`r`範本為基礎的新 R 應用程式基本架構。
```bash
azdata app init --name reduce --template r
```
根據`python`範本 Scaffold 新的 Python 應用程式基本架構。
```bash
azdata app init --name reduce --template python
```
Scaffold 以`ssis`範本為基礎的新 SSIS 應用程式基本架構。
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
只產生應用程式規格. yaml。
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
#### `--template -t`
範本名稱。 如需完整清單, 請從支援的範本名稱執行`azdata app template list`
#### `--destination -d`
應用程式基本架構的放置位置。 預設值: 目前的工作目錄。
#### `--url -u`
指定不同的範本存放庫位置。 預設 https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>azdata 應用程式建立
建立應用程式。
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>範例
從包含有效 yaml 部署規格的目錄建立新的應用程式。
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>必要參數
#### `--spec -s`
目錄的路徑, 其中包含描述應用程式的 YAML 規格檔案。
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
## <a name="azdata-app-update"></a>azdata 應用程式更新
更新應用程式。
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>範例
從包含有效 yaml 部署規格的目錄更新現有的應用程式。
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
目錄的路徑, 其中包含描述應用程式的 YAML 規格檔案。
#### `--yes -y`
從 CWD 的 yaml 檔案更新應用程式時, 不會提示您進行確認。
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
## <a name="azdata-app-list"></a>azdata 應用程式清單
列出應用程式。
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>範例
依名稱和版本列出應用程式。
```bash
azdata app list --name reduce  --version v1
```
依名稱列出所有應用程式版本。
```bash
azdata app list --name reduce
```
依名稱列出所有應用程式版本。
```bash
azdata app list
```
### <a name="optional-parameters"></a>選擇性參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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
## <a name="azdata-app-delete"></a>azdata 應用程式刪除
刪除應用程式。
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>範例
依名稱和版本刪除應用程式。
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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
## <a name="azdata-app-run"></a>azdata 應用程式執行
執行應用程式。
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>範例
執行沒有輸入參數的應用程式。
```bash
azdata app run --name reduce --version v1
```
執行具有1個輸入參數的應用程式。
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
執行具有多個輸入參數的應用程式。
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
### <a name="optional-parameters"></a>選擇性參數
#### `--inputs`
CSV `name=value`格式的應用程式輸入參數。
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
## <a name="azdata-app-describe"></a>azdata 應用程式描述
描述應用程式。
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>範例
描述應用程式。
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>選擇性參數
#### `--spec -s`
目錄的路徑, 其中包含描述應用程式的 YAML 規格檔案。
#### `--name -n`
應用程式名稱
#### `--version -v`
應用程式版本。
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

如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
